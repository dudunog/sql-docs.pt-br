---
title: Registrar em log e definir entradas de log em um componente de fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- logs [Integration Services], custom
- custom log entries [Integration Services]
- custom data flow components [Integration Services], logging
- data flow components [Integration Services], logging
ms.assetid: 2190dba9-59b5-480b-b8e9-21d5a54c5917
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1f8a82b02a7743362f3769725074501b584140a2
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916192"
---
# <a name="logging-and-defining-log-entries-in-a-data-flow-component"></a>Registrando em log e definindo entradas de log em um componente de fluxo de dados

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  Os componentes de fluxo de dados personalizados podem postar mensagens em uma entrada de log existente por meio do método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.PostLogMessage%2A> da interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>. Eles também podem apresentar informações ao usuário através do método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.FireInformation%2A> ou de métodos semelhantes da interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100>. Entretanto, essa abordagem leva à sobrecarga pois eventos adicionais são gerados e manipulados, e força o usuário a examinar mensagens informativas detalhadas em busca de mensagens que possam ser do seu interesse. Você pode usar uma entrada de log personalizada, conforme descrito a seguir, para fornecer informações de log personalizadas com rótulos distintos a usuários de seu componente.  
  
## <a name="registering-and-using-a-custom-log-entry"></a>Registrando e usando uma entrada de log personalizada  
  
### <a name="registering-a-custom-log-entry"></a>Registrar uma entrada de log personalizada  
 Para registrar uma entrada de log personalizada a ser usada por seu componente, substitua o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.RegisterLogEntries%2A> da classe base <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>. O exemplo a seguir registra uma entrada de log personalizada e fornece um nome e uma descrição.  
  
```csharp  
using Microsoft.SqlServer.Dts.Runtime;  
...  
private const string MyLogEntryName = "My Custom Component Log Entry";  
private const string MyLogEntryDescription = "Log entry from My Custom Component ";  
...  
    public override void RegisterLogEntries()  
    {  
      this.LogEntryInfos.Add(MyLogEntryName,  
        MyLogEntryDescription,  
        Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT);  
    }  
```  
  
```vb  
Imports Microsoft.SqlServer.Dts.Runtime  
...  
Private Const MyLogEntryName As String = "My Custom Component Log Entry"   
Private Const MyLogEntryDescription As String = "Log entry from My Custom Component "  
...  
Public  Overrides Sub RegisterLogEntries()   
  Me.LogEntryInfos.Add(MyLogEntryName, _  
    MyLogEntryDescription, _  
    Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT)   
End Sub  
```  
  
 A enumeração <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency> fornece uma dica ao runtime sobre a frequência com que o evento será registrado:  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_OCCASIONAL>: o evento só é registrado às vezes, mas não em toda execução.  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT>: o evento é registrado em um número constante de horas em toda execução.  
  
-   <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_PROPORTIONAL>: o evento é registrado um determinado número de vezes, que é proporcional à quantidade de trabalho concluído.  
  
 O exemplo anterior usa o <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSLogEntryFrequency.DTSLEF_CONSISTENT> pois o componente espera registrar uma só entrada em cada execução.  
  
 Depois de registrar a entrada de log personalizada e adicionar uma instância do seu componente personalizado na superfície do designer de fluxo de dados, a caixa de diálogo **Log** do designer exibe uma nova entrada de log com o nome "My Custom Component Log Entry" na lista de entradas de log disponíveis.  
  
### <a name="logging-to-a-custom-log-entry"></a>Registrando uma entrada de log personalizada  
 Depois do registro da entrada de log personalizada, o componente pode registrar mensagens personalizadas. O exemplo a seguir escreve uma entrada de log personalizada durante o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.PreExecute%2A> que contém o texto de uma instrução SQL usado pelo componente.  
  
```csharp  
public override void PreExecute()  
{  
  DateTime now = DateTime.Now;  
  byte[] additionalData = null;  
  this.ComponentMetaData.PostLogMessage(MyLogEntryName,  
    this.ComponentMetaData.Name,  
    "Command Sent was: " + myCommand.CommandText,  
    now, now, 0, ref additionalData);  
}  
```  
  
```vb  
Public  Overrides Sub PreExecute()   
  Dim now As DateTime = DateTime.Now   
  Dim additionalData As Byte() = Nothing   
  Me.ComponentMetaData.PostLogMessage(MyLogEntryName, _  
    Me.ComponentMetaData.Name, _  
    "Command Sent was: " + myCommand.CommandText, _  
    now, now, 0, additionalData)   
End Sub  
```  
  
 Agora, quando o usuário executar o pacote, depois de selecionar "My Custom Component Log Entry" na caixa de diálogo **Log**, o log conterá uma entrada claramente rotulada como "User::My Custom Component Log Entry". Essa nova entrada de log contém o texto da instrução SQL, o carimbo de data/hora e quaisquer dados adicionais registrados pelo desenvolvedor.  
  
## <a name="see-also"></a>Consulte Também  
 [Registro em Log do SSIS &#40;Integration Services&#41;](../../../integration-services/performance/integration-services-ssis-logging.md)  
  
  
