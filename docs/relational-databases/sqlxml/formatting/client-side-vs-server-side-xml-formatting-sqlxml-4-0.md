---
title: Formatação XML do lado do cliente versus do servidor (SQLXML)
description: Aprenda as diferenças gerais entre a formatação XML do lado do cliente e do servidor no SQLXML 4,0.
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- NESTED mode
- FOR XML clause, formatting
- client-side XML formatting
- server-side XPath
- server-side XML formatting
- AUTO mode
- client-side XPath
ms.assetid: f807ab7a-c5f8-4e61-9b00-23aebfabc47e
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b80124c112f4a64044ea54040b8085b73f9ff83e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85666133"
---
# <a name="client-side-vs-server-side-xml-formatting-sqlxml-40"></a>Lado do cliente e Formatação XML do lado do servidor (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Este tópico descreve as diferenças gerais entre a formatação XML no lado cliente e no lado servidor no SQLXML.  
  
## <a name="multiple-rowset-queries-not-supported-in-client-side-formatting"></a>Várias consultas a conjuntos de linhas sem suporte na formatação no lado do cliente  
 Consultas que geram vários conjuntos de linha não têm suporte quando você usa a formatação XML no lado do cliente. Por exemplo, suponha que você tenha um diretório virtual em que a formatação no lado do cliente seja especificada. Considere este modelo de exemplo, que tem duas instruções SELECT em um **\<sql:query>** bloco:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>  
     SELECT FirstName FROM Person.Contact FOR XML Nested;   
     SELECT LastName FROM Person.Contact FOR XML Nested    
  </sql:query>  
</ROOT>  
```  
  
 Você pode executar este modelo em código do aplicativo e um erro será retornado, porque a formatação XML no lado do cliente não dá suporte à formatação de vários conjuntos de linha. Se você especificar as consultas em dois **\<sql:query>** blocos separados, obterá os resultados desejados.  
  
## <a name="timestamp-maps-differently-in-client--vs-server-side-formatting"></a>Carimbo de data e hora mapeia de forma diferente as formatações no lado do cliente e no lado do servidor  
 Na formatação XML do lado do servidor, a coluna do banco de dados do tipo de **carimbo de data/hora** é mapeada para o tipo de XDR de i8 (quando a opção XMLDATA é especificada na consulta).  
  
 Na formatação XML do lado do cliente, a coluna do banco de dados do tipo de **carimbo de data/hora** é mapeada para o tipo de XDR **URI** ou **bin. base64** (dependendo se a opção Binary Base64 está especificada na consulta). O tipo de XDR **bin. base64** será útil se você usar os recursos updategram e carregamento em massa, pois esse tipo é convertido para o tipo de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **carimbo de data/hora** . Deste modo, as operações de inserção, atualização ou exclusão são bem-sucedidas.  
  
## <a name="deep-variants-are-used-in-server-side-formatting"></a>VARIANTs profundas são usadas na formatação no lado do servidor  
 Na formatação no lado do servidor, os tipos profundos de um tipo VARIANT são usados. Se você usar uma formatação XML no lado do cliente, as variantes serão convertidas à cadeia de caracteres Unicode e os subtipos de VARIANT não serão usados.  
  
## <a name="nested-mode-vs-auto-mode"></a>Modo NESTED e modo AUTO  
 O modo NESTED de FOR XML do lado do cliente é semelhante ao modo AUTO de FOR XML do lado do servidor, com as seguintes exceções:  
  
### <a name="when-you-query-views-using-auto-mode-on-the-server-side-the-view-name-is-returned-as-the-element-name-in-the-resulting-xml"></a>Quando você consulta exibições usando o modo AUTO no lado do servidor, o nome da exibição é retornado como o nome do elemento no XML resultante.  
 Por exemplo, suponha que a exibição a seguir seja criada na tabela Person. Contact no AdventureWorksdatabase:  
  
```  
CREATE VIEW ContactView AS (SELECT ContactID as CID,  
                               FirstName  as FName,  
                               LastName  as LName  
                        FROM Person.Contact)  
```  
  
 O modelo a seguir especifica uma consulta na exibição ContactView e também uma formatação XML no lado do servidor.  
  
```  
 <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="0">  
    SELECT *  
    FROM   ContactView  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 Quando você executar o modelo, o seguinte XML será retornado: (Somente resultados parciais são mostrados.) Observe que os nomes de elemento são os nomes das exibições nas quais a consulta é executada.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <ContactView CID="1" FName="Gustavo" LName="Achong" />   
  <ContactView CID="2" FName="Catherine" LName="Abel" />   
...  
</ROOT>  
```  
  
 Quando você especifica a formatação XML no lado cliente usando o modo NESTED correspondente, o(s) nome(s) da tabela base são retornados como nome(s) do elemento no XML resultante. Por exemplo, o modelo revisado a seguir executa a mesma instrução SELECT, mas a formatação XML é executada no lado do cliente (ou seja, o **XML do lado do cliente** é definido como true no modelo):  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="1">  
    SELECT *  
    FROM   ContactView  
    FOR XML NESTED  
  </sql:query>  
</ROOT>  
```  
  
 A execução desse modelo produz o seguinte XML: Observe que o nome do elemento é o nome da tabela base, nesse caso.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact CID="1" FName="Gustavo" LName="Achong" />   
  <Person.Contact CID="2" FName="Catherine" LName="Abel" />   
...  
</ROOT>  
```  
  
### <a name="when-you-use-auto-mode-of-the-server-side-for-xml-the-table-aliases-specified-in-the-query-are-returned-as-element-names-in-the-resulting-xml"></a>Quando você usa o modo AUTO de FOR XML no lado do servidor, os aliases da tabela especificados na consulta são retornados como nomes de elemento no XML resultante.  
 Por exemplo, considere este modelo:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="0">  
    SELECT FirstName as fname,  
           LastName as lname  
    FROM   Person.Contact C  
    FOR XML AUTO  
  </sql:query>  
</ROOT>  
```  
  
 A execução do modelo produz o seguinte XML:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <C fname="Gustavo" lname="Achong" />   
  <C fname="Catherine" lname="Abel" />   
...  
</ROOT>   
```  
  
 Quando você usa o modo NESTED de FOR XML no lado do cliente, os nomes da tabela são retornados como nomes do elemento no XML resultante. (Os aliases de tabela especificados na consulta não são usados.) Por exemplo, considere este modelo:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="1">  
    SELECT FirstName as fname,  
           LastName as lname  
    FROM   Person.Contact C  
    FOR XML NESTED  
  </sql:query>  
</ROOT>  
```  
  
 A execução do modelo produz o seguinte XML:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact fname="Gustavo" lname="Achong" />   
  <Person.Contact fname="Catherine" lname="Abel" />   
...  
</ROOT>  
```  
  
### <a name="if-you-have-a-query-that-returns-columns-as-dbobject-queries-you-cannot-use-aliases-for-these-columns"></a>Se você tiver uma consulta que retorne colunas como consultas dbobject, não poderá usar aliases para essas colunas.  
 Por exemplo, considere o modelo a seguir, que executa uma consulta que retorna uma ID de funcionário e uma foto.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<sql:query client-side-xml="1">  
   SELECT ProductPhotoID, LargePhoto as P  
   FROM   Production.ProductPhoto  
   WHERE  ProductPhotoID=5  
   FOR XML NESTED, elements  
</sql:query>  
</ROOT>  
```  
  
 A execução desse modelo retorna a coluna Photo como consulta dbobject. Nessa consulta dbobject, `@P` se refere a um nome de coluna que não existe.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Production.ProductPhoto>  
    <ProductPhotoID>5</ProductPhotoID>  
    <LargePhoto>dbobject/Production.ProductPhoto[@ProductPhotoID='5']/@P</LargePhoto>  
  </Production.ProductPhoto>  
</ROOT>  
```  
  
 Se a formatação XML for feita no servidor (**cliente-XML = "0"**), você poderá usar o alias para as colunas que retornam consultas DBObject nas quais os nomes reais de tabela e coluna são retornados (mesmo que você tenha aliases especificados). Por exemplo, o modelo a seguir executa uma consulta e a formatação XML é feita no servidor (a opção de **XML do lado do cliente** não é especificada e a opção **executar no cliente** não é selecionada para a raiz virtual). A consulta também especifica o modo AUTO (não o modo NESTED do lado do cliente).  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
<sql:query   
   SELECT ProductPhotoID, LargePhoto as P  
   FROM   Production.ProductPhoto  
   WHERE  ProductPhotoID=5  
   FOR XML AUTO, elements  
</sql:query>  
</ROOT>  
```  
  
 Quando esse modelo é executado, o seguinte documento XML é retornado (observe que os aliases não são usados na consulta dbobject para a coluna LargePhoto):  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Production.ProductPhoto>  
    <ProductPhotoID>5</ProductPhotoID>  
    <LargePhoto>dbobject/Production.ProductPhoto[@ProductPhotoID='5']/@LargePhoto</LargePhoto>  
  </Production.ProductPhoto>  
</ROOT>  
```  
  
### <a name="client-side-vs-server-side-xpath"></a>XPath do lado do cliente e do lado do servidor  
 O XPath funciona da mesma forma no lado do cliente e no lado do servidor, exceto por estas diferenças:  
  
-   As conversões de dados que são aplicadas quando você usa consultas XPath no lado do cliente são diferentes das aplicadas quando você usa consultas XPath no lado do servidor. XPath no lado do cliente usa o modo CAST em vez de CONVERT mode 126.  
  
-   Ao especificar o **cliente-XML = "0"** (false) em um modelo, você está solicitando a formatação XML do lado do servidor. Portanto, você não pode especificar FOR XML NESTED porque o servidor não reconhece a opção ANINHADO. Isso gera um erro. Você deve usar os modos AUTO, RAW ou EXPLICIT, reconhecidos pelo servidor.  
  
-   Ao especificar o **cliente-XML = "1"** (verdadeiro) em um modelo, você está solicitando a formatação XML do lado do cliente. Nesse caso, você pode especificar FOR XML NESTED. Se você especificar FOR XML AUTO, a formatação XML ocorrerá no lado do servidor, embora o **lado do cliente-XML = "1"** seja especificado no modelo.  
  
## <a name="see-also"></a>Consulte Também  
 [Considerações sobre segurança de FOR XML &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/security/for-xml-security-considerations-sqlxml-4-0.md)   
 [Formatação XML do lado do cliente &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)   
 [Formatação XML do lado do servidor &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml/formatting/server-side-xml-formatting-sqlxml-4-0.md)  
  
  
