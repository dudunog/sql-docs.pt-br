---
title: Mapeamentos XSD personalizados para tabelas/colunas (SQLXML)
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- explicit schema mapping [SQLXML]
- XPath queries [SQLXML], annotated XSD schemas in queries
- sql:field
- row mapping [SQLXML]
- attribute mapping [SQLXML], explicit mapping
- field annotation
- XSD schemas [SQLXML], mapping attributes and elements
- names [SQLXML]
- relation annotation
- table/view mapping [SQLXML], explicit mapping
- sql:relation
- mapping schema [SQLXML], explicit mapping
- annotated XSD schemas, mapping attributes and elements
- column mapping [SQLXML]
- element mapping [SQLXML], explicit mapping
- table mapping [SQLXML], explicit mapping
- element/attribute mapping [SQLXML]
ms.assetid: 7a5ebeb6-7322-4141-a307-ebcf95976146
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5fafcd918dda0001c316fd68cae3b19e6cd805a3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75257428"
---
# <a name="custom-xsd-mappings-to-tablescolumns-sqlxml"></a>Mapeamentos XSD personalizados para tabelas/colunas (SQLXML)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Ao usar um esquema XSD para fornecer uma exibição XML do banco de dados relacional, os elementos e atributos do esquema devem ser mapeados em tabelas e colunas do banco de dados. As linhas na tabela/exibição do banco de dados serão mapeadas em elementos no documento XML. Os valores de coluna no banco de dados são mapeados em atributos ou elementos.  
  
 Quando são especificadas consultas XPath com relação ao esquema XSD anotado, os dados dos elementos e atributos no esquema são recuperados das tabelas e colunas nas quais eles são mapeados. Para obter um único valor do banco de dados, o mapeamento especificado no esquema XSD deve ter especificação de campo e relação. Se o nome de um elemento/atributo não for o mesmo nome que o nome da tabela/exibição ou da coluna para o qual ele mapeia, as anotações **SQL: relation** e **SQL: Field** serão usadas para especificar o mapeamento entre um elemento ou atributo em um documento XML e a tabela (exibição) ou coluna em um banco de dados.  
  
## <a name="sql-relation"></a>sql-relation  
 A anotação **SQL: relation** é adicionada para mapear um nó XML no esquema XSD para uma tabela de banco de dados. O nome de uma tabela (exibição) é especificado como o valor da anotação **SQL: relation** .  
  
 Quando **SQL: relation** é especificado em um elemento, o escopo dessa anotação se aplica a todos os atributos e elementos filho que são descritos na definição de tipo complexo desse elemento, portanto, fornecendo um atalho em anotações de escrita.  
  
 A anotação **SQL: relation** também é útil quando os identificadores válidos no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não são válidos em XML. Por exemplo, "Pedido de Vendas" é um nome de tabela válido no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas não no XML. Nesses casos, a anotação **SQL: relation** pode ser usada para especificar o mapeamento, por exemplo:  
  
```  
<xsd:element name="OD" sql:relation="[Order Details]">  
```  
  
## <a name="sql-field"></a>sql-field  
 A anotação **SQL-Field** mapeia um elemento ou atributo para uma coluna de banco de dados. A anotação **SQL: Field** é adicionada para mapear um nó XML no esquema para uma coluna de banco de dados. Não é possível especificar **SQL: Field** em um elemento de conteúdo vazio.  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de funcionamento usando os exemplos a seguir, é necessário atender a determinados requisitos. Para obter mais informações, consulte [Requirements for running SQLXML examples](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-the-sqlrelation-and-sqlfield-annotations"></a>A. Especificando as anotações sql:relation e sql:field  
 Neste exemplo, o esquema XSD consiste em um ** \<elemento Contact>** de tipo complexo com ** \<fname>** e ** \<lname>** elementos filho e o atributo **ContactID** .  
  
 A anotação **SQL: relation** mapeia o ** \<elemento Contact>** para a tabela Person. Contact no banco de dados AdventureWorks. A anotação **SQL: Field** mapeia o ** \<elemento fname>** para a coluna FirstName e o ** \<elemento lname>** para a coluna LastName.  
  
 Nenhuma anotação foi especificada para o atributo **ContactID** . Isso resulta em um mapeamento padrão do atributo na coluna com o mesmo nome.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  <xsd:element name="Contact" sql:relation="Person.Contact" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="FName"  
                     sql:field="FirstName"   
                     type="xsd:string" />   
        <xsd:element name="LName"    
                     sql:field="LastName"    
                     type="xsd:string" />  
     </xsd:sequence>  
        <xsd:attribute name="ContactID"   
                       type="xsd:integer" />  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para testar uma consulta XPath de exemplo com relação ao esquema  
  
1.  Copie o código de esquema acima e cole-o em um arquivo de texto. Salve o arquivo como MySchema-annotated.xml.  
  
2.  Copie o seguinte modelo abaixo e cole-o em um arquivo de texto. Salve o arquivo como MySchema-annotatedT.xml no mesmo diretório em que você salvou MySchema-annotated.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="MySchema-annotated.xml">  
        /Contact  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho do diretório especificado para o esquema de mapeamento (MySchema-annotated.xml) é relativo ao diretório no qual o modelo foi salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\MySchema-annotated.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este é o conjunto de resultados parcial:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">   
 <Contact ContactID="1">   
    <FName>Gustavo</FName>   
    <LName>Achong</LName>   
 </Contact>   
  .....  
</ROOT>  
```  
  
  
