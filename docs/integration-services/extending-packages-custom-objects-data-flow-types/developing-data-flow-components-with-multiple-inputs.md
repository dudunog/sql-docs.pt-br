---
description: Desenvolvendo componentes de fluxo de dados com várias entradas
title: Desenvolvendo componentes de fluxo de dados com várias entradas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 3c7b50e8-2aa6-4f6a-8db4-e8293bc21027
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e73d9b4a6f23473e0dcb7600507dc29fd795679a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484291"
---
# <a name="developing-data-flow-components-with-multiple-inputs"></a>Desenvolvendo componentes de fluxo de dados com várias entradas

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Um componente de fluxo de dados com várias entradas poderá consumir memória excessiva se suas várias entradas gerarem dados em taxas desiguais. Ao desenvolver um componente de fluxo de dados personalizado que dá suporte a duas ou mais entradas, você pode gerenciar essa pressão de memória com o uso dos seguintes membros no namespace Microsoft.SqlServer.Dts.Pipeline:  
  
-   A propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> da classe <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>. Defina o valor dessa propriedade como **true** se desejar implementar o código necessário para seu componente de fluxo de dados personalizado para gerenciar dados que fluem em taxas desiguais.  
  
-   O método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> da classe <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>. Você deverá fornecer uma implementação desse método, se definir a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> como **true**. Se você não fornecer uma implementação, o mecanismo de fluxo de dados gerará uma exceção em tempo de execução.  
  
-   O método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> da classe <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>. Você também deverá fornecer uma implementação desse método, se definir a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> como **true** e seu componente personalizado der suporte a mais de duas entradas. Se você não fornecer uma implementação, o mecanismo de fluxo de dados gerará uma exceção em tempo de execução se o usuário anexar mais de duas entradas.  
  
 Juntos, esses membros permitem desenvolver uma solução para pressão de memória que é semelhante à solução que a Microsoft desenvolveu para as transformações de Mesclagem e Junção de Mesclagem.  
  
## <a name="setting-the-supportsbackpressure-property"></a>Definindo a propriedade SupportsBackPressure  
 A primeira etapa ao implementar um gerenciamento melhor de memória para um componente de fluxo de dados personalizado que dá suporte a várias entradas é definir o valor da propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> como **true** no <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>. Quando o valor de <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> for **true**, o mecanismo de fluxo de dados chamará o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> e, quando houver mais de duas entradas, também chamará o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> em tempo de execução.  
  
### <a name="example"></a>Exemplo  
 No exemplo a seguir, a implementação do <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> define o valor de <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> como **true**.  
  
```csharp  
[DtsPipelineComponent(ComponentType = ComponentType.Transform,  
        DisplayName = "Shuffler",  
        Description = "Shuffle the rows from input.",  
        SupportsBackPressure = true,  
        LocalizationType = typeof(Localized),  
        IconResource = "Microsoft.Samples.SqlServer.Dts.MIBPComponent.ico")  
]  
public class Shuffler : Microsoft.SqlServer.Dts.Pipeline.PipelineComponent  
        {  
          ...  
        }  
```  
  
## <a name="implementing-the-isinputready-method"></a>Implementando o método IsInputReady  
 Ao definir o valor da propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> como **true** no objeto <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>, você também deve fornecer uma implementação para o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> da classe <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>.  
  
> [!NOTE]  
>  Sua implementação do método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> não deve chamar as implementações na classe base. A implementação padrão desse método na classe base simplesmente gera uma **NotImplementedException**.  
  
 Ao implementar esse método, você define o status de um elemento na matriz Booliana *canProcess* para cada uma das entradas do componente. (As entradas são identificadas pelos valores de suas IDs na matriz *inputIDs*.) Quando você define o valor de um elemento na matriz *canProcess* como **true** para uma entrada, o mecanismo de fluxo de dados chama o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> do componente e fornece mais dados para a entrada especificada.  
  
 Embora mais dados de upstream estejam disponíveis, o valor do elemento da matriz *canProcess* de pelo menos uma entrada deve sempre ser **true**ou o processamento será interrompido.  
  
 O mecanismo de fluxo de dados chama o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> antes de enviar cada buffer de dados para determinar quais entradas estão esperando o recebimento de mais dados. Quando o valor de retorno indica que uma entrada está bloqueada, o mecanismo de fluxo de dados armazena buffers de dados adicionais em cache temporariamente para aquela entrada em vez de enviá-los ao componente.  
  
> [!NOTE]  
>  Você não chama os métodos <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> ou <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> em seu próprio código. O mecanismo de fluxo de dados chama esses métodos e os outros métodos da classe **PipelineComponent** que você substitui, quando o mecanismo de fluxo de dados executa seu componente.  
  
### <a name="example"></a>Exemplo  
 No exemplo a seguir, a implementação do método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> indica que uma entrada estará esperando receber mais dados se as seguintes condições forem verdadeiras:  
  
-   Mais dados upstream estão disponíveis para a entrada (`!inputEOR`).  
  
-   O componente não tem dados disponíveis no momento para processar a entrada nos buffers que o componente já recebeu (`inputBuffers[inputIndex].CurrentRow() == null`).  
  
 Se uma entrada estiver esperando receber mais dados, o componente de fluxo de dados indicará isso por meio da definição do valor do elemento como **true** na matriz *canProcess* correspondente àquela entrada.  
  
 De modo oposto, quando o componente ainda tem dados disponíveis para processar para a entrada, o exemplo suspende o processamento da entrada. O exemplo faz isso por meio da definição como **false** do valor do elemento na matriz *canProcess* correspondente àquela entrada.  
  
```csharp  
public override void IsInputReady(int[] inputIDs, ref bool[] canProcess)  
{  
    for (int i = 0; i < inputIDs.Length; i++)  
    {  
        int inputIndex = ComponentMetaData.InputCollection.GetObjectIndexByID(inputIDs[i]);  
  
        canProcess[i] = (inputBuffers[inputIndex].CurrentRow() == null)  
            && !inputEOR[inputIndex];  
    }  
}  
```  
  
 O exemplo anterior usa a matriz booliana `inputEOR` para indicar se dados upstream estão disponíveis para cada entrada. `EOR` no nome da matriz representa "término de conjunto de linhas" e faz referência à propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> de buffers de fluxo de dados. Em uma parte do exemplo que não é incluída aqui, o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> verifica o valor da propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> de cada buffer de dados que recebe. Quando um valor de **true** indica que não há mais dados upstream disponíveis para uma entrada, o exemplo define o valor do elemento da matriz `inputEOR` daquela entrada como **true**. Esse exemplo do método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> define o valor do elemento correspondente na matriz *canProcess* como **false** para uma entrada quando o valor do elemento da matriz `inputEOR` indica que não há mais dados upstream disponíveis para a entrada.  
  
## <a name="implementing-the-getdependentinputs-method"></a>Implementando o método GetDependentInputs  
 Quando o componente de fluxo de dados personalizado der suporte a mais de duas entradas, você também deve fornecer uma implementação do método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> da classe <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>.  
  
> [!NOTE]  
>  Sua implementação do método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> não deve chamar as implementações na classe base. A implementação padrão desse método na classe base simplesmente gera uma **NotImplementedException**.  
  
 O mecanismo de fluxo de dados chamará o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> apenas quando o usuário anexar mais de duas entradas ao componente. Quando um componente tiver apenas duas entradas e o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> indicar que uma entrada está bloqueada (*canProcess* = **false**), o mecanismo de fluxo de dados saberá que a outra entrada está esperando o recebimento de mais dados. No entanto, quando houver mais de duas entradas, e o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> indicar que uma entrada está bloqueada, o código adicional no <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> identificará quais entradas estão esperando o recebimento de mais dados.  
  
> [!NOTE]  
>  Você não chama os métodos <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> ou <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> em seu próprio código. O mecanismo de fluxo de dados chama esses métodos e os outros métodos da classe **PipelineComponent** que você substitui, quando o mecanismo de fluxo de dados executa seu componente.  
  
### <a name="example"></a>Exemplo  
 Para uma entrada específica que está bloqueada, a seguinte implementação do método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> retorna uma coleção das entradas que estão esperando o recebimento de mais dados e, portanto, estão bloqueando a entrada especificada. O componente identifica as entradas com bloqueio por meio da verificação de outras entradas além da entrada bloqueada que não tem dados disponíveis no momento para processamento nos buffers que o componente já recebeu (`inputBuffers[i].CurrentRow() == null`). Em seguida, o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> retorna a coleção de entradas com bloqueio como uma coleção de IDs de entrada.  
  
```csharp  
public override Collection<int> GetDependentInputs(int blockedInputID)  
{  
    Collection<int> currentDependencies = new Collection<int>();  
    for (int i = 0; i < ComponentMetaData.InputCollection.Count; i++)  
    {  
        if (ComponentMetaData.InputCollection[i].ID != blockedInputID  
            && inputBuffers[i].CurrentRow() == null)  
        {  
            currentDependencies.Add(ComponentMetaData.InputCollection[i].ID);  
        }  
    }  
  
    return currentDependencies;  
}  
```  
  
  
