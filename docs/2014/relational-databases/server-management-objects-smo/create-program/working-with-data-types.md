---
title: Trabalhando com tipos de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- DataType object
- SQL Server Management Objects, data types
- data types [SMO]
- SMO [SQL Server], data types
ms.assetid: 1e0e736a-c709-4d89-aeb2-b32dcfd641fa
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d516901a3e44def9a0d6e19414bf0b972f9b37dc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63229088"
---
# <a name="working-with-data-types"></a>Trabalhando com tipos de dados
  Existem muitos tipos e tamanhos de dados, como uma cadeia de caracteres com comprimento definido, um número com uma precisão específica ou um tipo de dados definido pelo usuário que é um outro objeto com seu próprio conjunto de regras. O <xref:Microsoft.SqlServer.Management.Smo.DataType> objeto classifica o tipo de dados para que ele possa ser manipulado corretamente [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]pelo. O objeto <xref:Microsoft.SqlServer.Management.Smo.DataType> é associado a objetos que aceitam dados. Os objetos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO) a seguir aceitam dados que devem ser definidos por uma propriedade de objeto <xref:Microsoft.SqlServer.Management.Smo.DataType>:  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Column>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.StoredProcedureParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedFunctionParameter>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.UserDefinedAggregateParameter>  
  
 A propriedade `DataType` para objetos que aceitam dados pode ser definida de várias maneiras.  
  
-   Use o construtor padrão e especifique propriedades de objeto <xref:Microsoft.SqlServer.Management.Smo.DataType> explicitamente.  
  
-   Use um construtor sobrecarregado e especifique as propriedades <xref:Microsoft.SqlServer.Management.Smo.DataType> como parâmetros.  
  
-   Especifique o <xref:Microsoft.SqlServer.Management.Smo.DataType> embutido no construtor de objeto.  
  
-   Use um dos membros estáticos da classe <xref:Microsoft.SqlServer.Management.Smo.DataType>, por exemplo `Int`. Isso retornará, na realidade, uma instância de um objeto <xref:Microsoft.SqlServer.Management.Smo.DataType>.  
  
 O objeto <xref:Microsoft.SqlServer.Management.Smo.DataType> tem várias propriedades que definem o tipo de dados. Por exemplo, a propriedade <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> especifica o tipo de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os valores constantes que representam tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] são listados na enumeração <xref:Microsoft.SqlServer.Management.Smo.SqlDataType>. Isso se refere a tipos de dados como `varchar`, `nchar`, `currency`, `integer`, `float` e `datetime`.  
  
 Quando o tipo de dados for estabelecido, propriedades específicas deverão ser definidas para os dados. Por exemplo, se ele for um tipo `nchar`, o comprimento dos dados de cadeia de caracteres deverá ser definido na propriedade `Length`. O mesmo se aplica a valores numéricos, nos quais você teria que especificar a precisão e a escala.  
  
 Os tipos de dados<xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> e <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> se referem a objetos que contêm a definição do tipo de dados definido pelo usuário. O <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> se baseia em tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] da enumeração <xref:Microsoft.SqlServer.Management.Smo.SqlDataType>. O <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType> é baseado em [!INCLUDE[msCoName](../../../includes/msconame-md.md)] tipos de dados do .net. Normalmente, esses representariam dados de um tipo específico que é reutilizado com frequência pelo banco de dados por causa de regras comerciais definidas pela organização. Por exemplo, um tipo de dados que armazena uma quantia de dinheiro e um denominador monetário seria útil em uma empresa que trabalha com várias moedas.  
  
 A enumeração <xref:Microsoft.SqlServer.Management.Smo.SqlDataType> contém uma lista de todos os tipos de dados com suporte no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="examples"></a>Exemplos  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-basic"></a>Construindo um objeto DataType com a especificação do construtor no Visual Basic  
 Este exemplo de código mostra como usar o construtor para criar instâncias de tipos de dados baseadas em diferentes tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Todos os tipos <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> e XML exigem um valor de nome para identificação do objeto.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDataTypes1](SMO How to#SMO_VBDataTypes1)]  -->  
  
## <a name="constructing-a-datatype-object-with-the-specification-in-the-constructor-in-visual-c"></a>Construindo um objeto DataType com a especificação do construtor no Visual C#  
 Este exemplo de código mostra como usar o construtor para criar instâncias de tipos de dados baseadas em diferentes tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Todos os tipos <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>, <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType> e XML exigem um valor de nome para identificação do objeto.  
  
```  
{   
//Declare a DataType object variable and define the data type in the constructor.   
DataType dt;   
//For the decimal data type the following two arguments specify precision, and scale.   
dt = new DataType(SqlDataType.Decimal, 10, 2);   
}  
```  
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-basic"></a>Construindo um objeto DataType com o construtor padrão no Visual Basic  
 Este exemplo de código mostra como usar o construtor padrão para criar instâncias de tipos de dados baseadas em diferentes tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . As propriedades são, então, usadas para especificar o tipo de dados.  
  
 **Observação** Todos <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>os <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>tipos XML,, e exigem um valor Name para identificar o objeto.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBDataTypes2](SMO How to#SMO_VBDataTypes2)]  -->  
  
## <a name="constructing-a-datatype-object-by-using-the-default-constructor-in-visual-c"></a>Construindo um objeto DataType com o construtor padrão no Visual C#  
 Este exemplo de código mostra como usar o construtor padrão para criar instâncias de tipos de dados baseadas em diferentes tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . As propriedades são, então, usadas para especificar o tipo de dados.  
  
 **Observação** Todos <xref:Microsoft.SqlServer.Management.Smo.UserDefinedType>os <xref:Microsoft.SqlServer.Management.Smo.UserDefinedDataType>tipos XML,, e exigem um valor Name para identificar o objeto.  
  
```  
{   
//Declare and create a DataType object variable.   
DataType dt;   
dt = new DataType();   
//Define the data type by setting the SqlDataType property.   
dt.SqlDataType = SqlDataType.VarChar;   
//The VarChar data type requires a value for the MaximumLength property.   
dt.MaximumLength = 100;   
}  
```  
  
  
