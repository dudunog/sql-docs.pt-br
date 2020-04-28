---
title: Gerando e definindo eventos em um componente de fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow components [Integration Services], events
- events [Integration Services], custom
- custom events [Integration Services]
- custom data flow components [Integration Services], events
- events [Integration Services], raising
- predefined events [Integration Services]
ms.assetid: 1d8c5358-9384-47a8-b7cb-7b0650384119
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 774cb9a56fbe4e81df6a440c754c417ae90c16e0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176314"
---
# <a name="raising-and-defining-events-in-a-data-flow-component"></a>Gerando e definindo eventos em um componente de fluxo de dados
  Desenvolvedores de componente podem gerar um subconjunto dos eventos definidos na interface <xref:Microsoft.SqlServer.Dts.Runtime.IDTSComponentEvents> por meio de chamada dos métodos expostos na propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ComponentMetaData%2A>. Você também pode definir eventos personalizados usando a coleção <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.EventInfos%2A> e gerá-los durante a execução usando o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A>. Esta seção descreve como criar e gerar um evento, e fornece diretrizes sobre quando você deve gerar eventos em tempo de design.

## <a name="raising-events"></a>Acionar eventos
 Os componentes acionam eventos usando os métodos **Fire\<X>** da interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>. Você pode gerar eventos durante o design e a execução do componente. Em geral, durante o design do componente, os métodos <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireError%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireWarning%2A> são chamados durante a validação. Esses eventos exibem mensagens no painel **Lista de Erros** do [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] e fornecem comentários a usuários do componente quando um componente é configurado incorretamente.

 Os componentes também podem gerar eventos a qualquer momento durante a execução. Eventos permitem aos desenvolvedores de componentes fornecer comentários a usuários do componente durante sua execução. É provável que a chamada do método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireError%2A> durante a execução leve à falha do pacote.

## <a name="defining-and-raising-custom-events"></a>Definindo e gerando eventos personalizados

### <a name="defining-a-custom-event"></a>Definindo um evento personalizado
 Eventos personalizados são criados chamando o método <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSEventInfos100.Add%2A> da coleção <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.EventInfos%2A>. Esta coleção é definida pela tarefa de fluxo de dados e fornecida como uma propriedade para o desenvolvedor de componente através da classe base <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>. Esta classe contém eventos personalizados definidos pela tarefa de fluxo de dados e eventos personalizados definidos pelo componente durante o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A>.

 Os eventos personalizados de um componente não persistem no pacote XML. Portanto, o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A> é chamado durante o design e a execução para permitir que o componente defina os eventos gerados por ele.

 O parâmetro *allowEventHandlers* do método <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSEventInfos100.Add%2A> especifica se o componente permite criar objetos <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> para o evento. Observe que <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandlers> são síncronos. Portanto, o componente não retomará a execução até que um <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> anexado ao evento personalizado termine a execução. Se o parâmetro *AllowEventHandlers* for `true`, cada parâmetro do evento será disponibilizado automaticamente para todos os <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandler> objetos por meio de variáveis que são criadas e preenchidas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] automaticamente pelo tempo de execução.

### <a name="raising-a-custom-event"></a>Gerando um evento personalizado
 Componentes geram eventos personalizados chamando o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A> e fornecendo o nome, texto e parâmetros do evento. Se o parâmetro *AllowEventHandlers* for `true`, qualquer <xref:Microsoft.SqlServer.Dts.Runtime.DtsEventHandlers> um criado para o evento personalizado será executado pelo mecanismo de [!INCLUDE[ssIS](../../../includes/ssis-md.md)] tempo de execução.

### <a name="custom-event-sample"></a>Exemplo de evento personalizado
 O exemplo de código a seguir mostra um componente que define um texto personalizado durante o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterEvents%2A> e, depois, gera o evento em tempo de execução chamando o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireCustomEvent%2A>.

```csharp
public override void RegisterEvents()
{
    string [] parameterNames = new string[2]{"RowCount", "StartTime"};
    ushort [] parameterTypes = new ushort[2]{ DtsConvert.VarTypeFromTypeCode(TypeCode.Int32), DtsConvert.VarTypeFromTypeCode(TypeCode.DateTime)};
    string [] parameterDescriptions = new string[2]{"The number of rows to sort.", "The start time of the Sort operation."};
    EventInfos.Add("StartingSort","Fires when the component begins sorting the rows.",false,ref parameterNames, ref parameterTypes, ref parameterDescriptions);
}
public override void ProcessInput(int inputID, PipelineBuffer buffer)
{
    while (buffer.NextRow())
    {
       // Process buffer rows.
    }

    IDTSEventInfo100 eventInfo = EventInfos["StartingSort"];
    object []arguments = new object[2]{buffer.RowCount, DateTime.Now };
    ComponentMetaData.FireCustomEvent("StartingSort", "Beginning sort operation.", ref arguments, ComponentMetaData.Name, ref FireSortEventAgain);
}
```

```vb
Public  Overrides Sub RegisterEvents() 
  Dim parameterNames As String() = New String(2) {"RowCount", "StartTime"} 
  Dim parameterTypes As System.UInt16() = New System.UInt16(2) {DtsConvert.VarTypeFromTypeCode(TypeCode.Int32), DtsConvert.VarTypeFromTypeCode(TypeCode.DateTime)} 
  Dim parameterDescriptions As String() = New String(2) {"The number of rows to sort.", "The start time of the Sort operation."} 
  EventInfos.Add("StartingSort", "Fires when the component begins sorting the rows.", False, parameterNames, parameterTypes, parameterDescriptions) 
End Sub 

Public  Overrides Sub ProcessInput(ByVal inputID As Integer, ByVal buffer As PipelineBuffer) 
  While buffer.NextRow 
  End While 
  Dim eventInfo As IDTSEventInfo100 = EventInfos("StartingSort") 
  Dim arguments As Object() = New Object(2) {buffer.RowCount, DateTime.Now} 
  ComponentMetaData.FireCustomEvent("StartingSort", _
    "Beginning sort operation.", arguments, _
    ComponentMetaData.Name, FireSortEventAgain) 
End Sub
```

![Ícone de Integration Services (pequeno)](../../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.

## <a name="see-also"></a>Consulte Também
 [Integration Services &#40;do SSIS&#41; manipuladores de eventos](../../integration-services-ssis-event-handlers.md) [Adicionar um manipulador de eventos a um pacote](../../add-an-event-handler-to-a-package.md)


