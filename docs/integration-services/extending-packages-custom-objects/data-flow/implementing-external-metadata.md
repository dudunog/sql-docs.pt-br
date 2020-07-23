---
title: Implementando metadados externos | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- disconnected validation [Integration Services]
- connected validation [Integration Services]
- custom data flow components [Integration Services], validating
- validation [Integration Services], components
- metadata [Integration Services]
- data flow components [Integration Services], validating
- data flow components [Integration Services], external metadata
- custom data flow components [Integration Services], external metadata
- external metadata [Integration Services]
ms.assetid: 8f5bd3ed-3e79-43a4-b6c1-435e4c2cc8cc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 65757d974c6deb690248343140a157e81e083a70
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86919643"
---
# <a name="implementing-external-metadata"></a>Implementando metadados externos

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  Quando um componente é desconectado de sua fonte de dados, você pode validar as colunas nas coleções de colunas de entrada e saída com base nas colunas da fonte de dados externa por meio da interface <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100>. Essa interface permite que você mantenha um instantâneo das colunas na fonte de dados externa e as mapeie para as colunas da coleção de colunas de entrada e saída do componente.  
  
 A implementação de colunas de metadados externos adiciona uma camada de sobrecarga e complexidade ao desenvolvimento do componente, já que você deve fazer a manutenção e a validação em uma coleção de colunas adicionais. Entretanto, a capacidade de evitar viagens dispendiosas de ida e volta ao servidor para validação pode tornar esse trabalho de desenvolvimento compensador.  
  
## <a name="populating-external-metadata-columns"></a>Preenchendo colunas de metadados externos  
 Normalmente, colunas de metadados externas são adicionadas à coleção quando a coluna de entrada ou de saída correspondente é criada. Novas colunas são criadas chamando-se o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.New%2A>. As propriedades da coluna são definidas para corresponder à fonte de dados externa.  
  
 A coluna de metadados externos é mapeada para a coluna de entrada e saída correspondente atribuindo-se a ID da coluna de metadados externos à propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.ExternalMetadataColumnID%2A> da coluna de entrada e saída. Isto permite que você localize com facilidade a coluna de metadados externos para uma coluna de entrada ou saída específica usando o método <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.GetObjectByID%2A> da coleção.  
  
 O exemplo a seguir mostra como criar uma coluna de metadados externos e mapear a coluna para uma coluna de saída ao definir a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSOutputColumn100.ExternalMetadataColumnID%2A>.  
  
```csharp  
public void CreateExternalMetaDataColumn(IDTSOutput100 output, int outputColumnID )  
{  
    IDTSOutputColumn100 oColumn = output.OutputColumnCollection.GetObjectByID(outputColumnID);  
    IDTSExternalMetadataColumn100 eColumn = output.ExternalMetadataColumnCollection.New();  
  
    eColumn.DataType = oColumn.DataType;  
    eColumn.Precision = oColumn.Precision;  
    eColumn.Scale = oColumn.Scale;  
    eColumn.Length = oColumn.Length;  
    eColumn.CodePage = oColumn.CodePage;  
  
    oColumn.ExternalMetadataColumnID = eColumn.ID;  
}  
```  
  
```vb  
Public Sub CreateExternalMetaDataColumn(ByVal output As IDTSOutput100, ByVal outputColumnID As Integer)   
 Dim oColumn As IDTSOutputColumn100 = output.OutputColumnCollection.GetObjectByID(outputColumnID)   
 Dim eColumn As IDTSExternalMetadataColumn100 = output.ExternalMetadataColumnCollection.New   
 eColumn.DataType = oColumn.DataType   
 eColumn.Precision = oColumn.Precision   
 eColumn.Scale = oColumn.Scale   
 eColumn.Length = oColumn.Length   
 eColumn.CodePage = oColumn.CodePage   
 oColumn.ExternalMetadataColumnID = eColumn.ID   
End Sub  
```  
  
## <a name="validating-with-external-metadata-columns"></a>Validando com colunas de metadados externos  
 A validação requer etapas adicionais para componentes que mantêm uma coleção de colunas de metadados externos, porque você deve validar com base em uma coleção adicional de colunas. A validação pode ser dividida em validação conectada ou desconectada.  
  
### <a name="connected-validation"></a>Validação conectada  
 Quando um componente é conectado a uma fonte de dados externa, as colunas nas coleções de entrada ou saída são verificadas diretamente na fonte de dados externa. Adicionalmente, as colunas na coleção de metadados externos devem ser validadas. Isso é necessário porque a coleção de metadados externos pode ser modificada por meio do **Editor Avançado** no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] e as alterações feitas à coleção não são detectáveis. Portanto, quando conectados, os componentes devem verificar se as colunas da coleção de colunas de metadados externos continuam refletindo as colunas da fonte de dados externa.  
  
 Você pode optar por ocultar a coleção de metadados externos no **Editor Avançado**, configurando a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSExternalMetadataColumnCollection100.IsUsed%2A> da coleção como **false**. Entretanto, esse procedimento também oculta a guia **Mapeamento de Coluna** do editor, a qual permite que os usuários mapeiem as colunas da coleção de entrada ou saída para as colunas da coleção de colunas de metadados externos. Configurar esta propriedade como **false** não impede que os desenvolvedores modifiquem programaticamente a coleção, mas fornece efetivamente um nível de proteção para a coleção de colunas de metadados externos de um componente que é utilizado exclusivamente no [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
### <a name="disconnected-validation"></a>Validação desconectada  
 Quando um componente é desconectado de uma fonte de dados externa, a validação é simplificada porque as colunas da coleção de entrada ou saída são verificadas diretamente com base nas colunas da coleção de metadados externos e não com base na fonte externa. Um componente deverá executar a validação desconectada quando a conexão com sua fonte de dados externa não tiver sido estabelecida ou quando a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100.ValidateExternalMetadata%2A> for **false**.  
  
 O exemplo de código a seguir demonstra uma implementação de um componente que executa validação com base em sua coleção de colunas de metadados externos.  
  
```csharp  
public override DTSValidationStatus Validate()  
{  
    if( this.isConnected && ComponentMetaData.ValidateExternalMetaData )  
    {  
        // TODO: Perform connected validation.  
    }  
    else  
    {  
        // TODO: Perform disconnected validation.  
    }  
}  
```  
  
```vb  
Public  Overrides Function Validate() As DTSValidationStatus   
 If Me.isConnected AndAlso ComponentMetaData.ValidateExternalMetaData Then   
  ' TODO: Perform connected validation.  
 Else   
  ' TODO: Perform disconnected validation.  
 End If   
End Function  
```  

## <a name="see-also"></a>Consulte Também  
 [Fluxo de Dados](../../../integration-services/data-flow/data-flow.md)  
  
  
