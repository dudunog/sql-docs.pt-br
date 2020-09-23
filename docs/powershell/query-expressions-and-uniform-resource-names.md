---
title: Expressões de consultas e nomes de recursos uniformes | Microsoft Docs
description: Saiba mais sobre expressões de consulta, que enumeram um ou mais objetos em uma hierarquia de modelo de objeto, e sobre os URNs (Uniform Resource Names), que identificam exclusivamente um só objeto.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: sql-server-powershell
ms.topic: conceptual
helpviewer_keywords:
- query expressions
- unique resource names
- URN
ms.assetid: e0d30dbe-7daf-47eb-8412-1b96792b6fb9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 26483454e805bf8dcaa780fed352cbe984c61f71
ms.sourcegitcommit: a9f16d7819ed0e2b7ad8f4a7d4d2397437b2bbb2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88714114"
---
# <a name="query-expressions-and-uniform-resource-names"></a>Expressões de consultas e nomes de recursos uniformes

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Os modelos SMO ( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Object) e os snap-ins do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell utilizam dois tipos de cadeia de caracteres de expressão semelhantes às expressões XPath. As expressões de consulta são cadeias de caracteres que especificam um conjunto de critérios para enumerar um ou mais objetos em uma hierarquia de modelo de objetos. Um URN (Uniform Resource Name) é um tipo específico de cadeia de caracteres de expressão de consulta que identifica exclusivamente um único objeto.  

> [!NOTE]
> Há dois módulos do SQL Server PowerShell; **SqlServer** e **SQLPS**. O módulo **SQLPS** está incluído na instalação do SQL Server (para compatibilidade com versões anteriores), mas não está sendo atualizado. O módulo do PowerShell mais atualizado é o módulo do **SqlServer**. O módulo do **SqlServer** contém versões atualizadas dos cmdlets no **SQLPS** e também inclui novos cmdlets para dar suporte aos recursos mais recentes do SQL.  
> As versões anteriores do módulo do **SqlServer** *foram* incluídas no SQL Server Management Studio (SSMS), mas apenas nas versões 16.x do SSMS. Para usar o PowerShell com o SSMS 17.0 e versões posteriores, o módulo do **SqlServer** deve ser instalado da Galeria do PowerShell.
> Para instalar o módulo do **SqlServer**, consulte [Instalar o SQL Server PowerShell](download-sql-server-ps-module.md).

  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Object1[<FilterExpression1>]/ ... /ObjectN[<FilterExpressionN>]  
  
<FilterExpression>::=  
<PropertyExpression> [and <PropertyExpression>][...n]  
  
<PropertyExpression>::=  
      @BooleanPropertyName=true()  
 | @BooleanPropertyName=false()  
 | contains(@StringPropertyName, 'PatternString')  
  | @StringPropertyName='String'  
 | @DatePropertyName=datetime('DateString')  
 | is_null(@PropertyName)  
 | not(<PropertyExpression>)  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *Objeto*  
 Especifica o tipo de objeto que é representado no nó da cadeia de caracteres de expressão. Cada objeto representa uma classe de coleção desses namespaces de modelos de objetos SMO:  
  
 <xref:Microsoft.SqlServer.Management.Smo>  
  
 <xref:Microsoft.SqlServer.Management.Smo.Agent>  
  
 <xref:Microsoft.SqlServer.Management.Smo.Broker>  
  
 <xref:Microsoft.SqlServer.Management.Smo.Mail>  
  
 <xref:Microsoft.SqlServer.Management.Dmf>  
  
 <xref:Microsoft.SqlServer.Management.Facets>  
  
 <xref:Microsoft.SqlServer.Management.RegisteredServers>  
  
 <xref:Microsoft.SqlServer.Management.Smo.RegSvrEnum>  
  
 Por exemplo, especifique o Servidor para a classe **ServerCollection** , o Banco de dados para a classe **DatabaseCollection** .  
  
 \@*PropertyName*  
 Especifica o nome de uma das propriedades da classe associada ao objeto especificado em *Objeto*. O nome da propriedade deve ser prefixado com o caractere \@. Por exemplo, especifique \@IsAnsiNull para a propriedade **IsAnsiNull** da classe **Database**.  
  
 \@*BooleanPropertyName*=true()  
 Enumera todos os objetos em que a propriedade booliana especificada está definida como TRUE.  
  
 \@*BooleanPropertyName*=false()  
 Enumera todos os objetos em que a propriedade booliana especificada está definida como FALSE.  
  
 contains(\@*StringPropertyName*, '*PatternString*')  
 Enumera todos os objetos em que a propriedade da cadeia de caracteres especificada contém pelo menos uma ocorrência do conjunto de caracteres especificado em “*PatternString*”.  
  
 \@*StringPropertyName*='*PatternString*'  
 Enumera todos os objetos em que o valor da propriedade da cadeia de caracteres especificada é exatamente igual ao padrão de caractere especificado em “*PatternString*”.  
  
 \@*DatePropertyName*= datetime('*DateString*')  
 Enumera todos os objetos em que o valor da propriedade de data especificada corresponde à data especificada em “*DateString*”. *DateString* deve seguir o formato aaaa-mm-dd hh:min:ss.mmm.  
  
|Componente DateString|Descrição|  
|-|-|  
|yyyy|Ano com quatro dígitos.|  
|MM|Mês com dois dígitos (01 a 12).|  
|dd|Dia com dois dígitos (01 a 31).|  
|hh|Hora com dois dígitos usando o formato de 24 horas (01 a 23).|  
|min|Minutos com dois dígitos (01 a 59).|  
|ss|Segundos com dois dígitos (01 a 59).|  
|mmm|Número de milissegundos (001 a 999).|  
  
 As datas especificadas nesse formato podem ser avaliadas em relação a qualquer formato de data armazenado no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 is_null(\@*PropertyName*)  
 Enumera todos os objetos em que a propriedade especificada tenha um valor NULL.  
  
 not(\<*PropertyExpression*>)  
 Nega o valor de avaliação de *PropertyExpression*, enumerando todos os objetos que não correspondem à condição especificada em *PropertyExpression*. Por exemplo, not(contains(\@Name, 'xyz')) enumera todos os objetos que não têm a cadeia de caracteres xyz em seus nomes.  
  
## <a name="remarks"></a>Comentários  
 Expressões de consulta são cadeias de caracteres que enumeram os nós em uma hierarquia de modelos SMO. Cada nó tem uma expressão de filtro que especifica os critérios de determinação dos objetos desse nó que são enumerados. As expressões de consultas são modeladas na linguagem de expressão XPath. As expressões de consulta implementam um pequeno subconjunto de expressões com suporte em XPath e também possuem algumas expressões que não são encontradas em XPath. As expressões Xpath são cadeias de caracteres que especificam um conjunto de critérios usados para enumerar uma ou mais marcas em um documento XML. Para obter mais informações sobre XPath, consulte [W3C XPath Language](http://www.w3.org/TR/xpath20/).  
  
 As expressões de consulta devem iniciar com uma referência absoluta ao objeto Servidor. Não são permitidas expressões relativas com uma / à esquerda. A sequência de objetos especificados em uma expressão de consulta deve seguir a hierarquia dos objetos de coleção do modelo de objetos associado. Por exemplo, uma expressão de consulta que faz referência a objetos no namespace Microsoft.SqlServer.Management.Smo deve começar com um nó Servidor, seguido por um nó Banco de Dados e assim por diante.  
  
 Se uma *\<FilterExpression>* não for especificada para um objeto, todos os objetos desse nó serão enumerados.  
  
## <a name="uniform-resource-names-urn"></a>URN (Uniform Resource Names)  
 URNs são um subconjunto de expressões de consulta. Cada URN forma uma referência totalmente qualificada a um único objeto. Um URN típico usa a propriedade Nome para identificar um único objeto em cada nó. Por exemplo, este URN faz referência a uma coluna específica:  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']/Table[@Name='SalesPerson' and @Schema='Sales']/Column[@Name='SalesPersonID']  
```  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-enumerating-objects-using-false"></a>a. Enumerando objetos usando false()  
 Esta expressão de consulta enumera todos os bancos de dados que têm o atributo **AutoClose** definido como false na instância padrão em **MyComputer**.  
  
```  
Server[@Name='MYCOMPUTER']/Database[@AutoClose=false()]  
```  
  
### <a name="b-enumerating-objects-using-contains"></a>B. Enumerando objetos usando contains  
 Esta expressão de consulta enumera todos os bancos de dados que não diferenciam maiúsculas de minúsculas e têm o caractere 'm' no nome.  
  
```  
Server[@Name='MYCOMPUTER']/Database[@CaseSensitive=false() and contains(@Name, 'm')]   
```  
  
### <a name="c-enumerating-objects-using-not"></a>C. Enumerando objetos usando not  
 Esta expressão de consulta enumera todas as tabelas [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] que não estão no esquema de **Produção** e que contêm a palavra Histórico no nome da tabela:  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012']/Table[not(@Schema='Production') and contains(@Name, 'History')]  
```  
  
### <a name="d-not-supplying-a-filter-expression-for-the-final-node"></a>D. Não fornecendo uma expressão de filtro para o nó final  
 Esta expressão de consulta enumera todas as colunas na tabela **AdventureWorks2012.Sales.SalesPerson** :  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012"]/Table[@Schema='Sales' and @Name='SalesPerson']/Columns  
```  
  
### <a name="e-enumerating-objects-using-datetime"></a>E. Enumerando objetos usando datetime  
 Esta expressão de consulta enumera todas as tabelas que são criadas no banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] em um momento específico:  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012"]/Table[@CreateDate=datetime('2008-03-21 19:49:32.647')]  
```  
  
### <a name="f-enumerating-objects-using-is_null"></a>F. Enumerando objetos usando is_null  
 Esta expressão de consulta enumera todas as tabelas do banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] que não têm o NULL para a última propriedade modificada:  
  
```  
Server[@Name='MYCOMPUTER']/Database[@Name='AdventureWorks2012"]/Table[Not(is_null(@DateLastModified))]  
```  
  
## <a name="see-also"></a>Consulte Também  
 [cmdlet Invoke-PolicyEvaluation](invoke-policyevaluation-cmdlet.md)   
 [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../relational-databases/security/auditing/sql-server-audit-database-engine.md)  
  
  
