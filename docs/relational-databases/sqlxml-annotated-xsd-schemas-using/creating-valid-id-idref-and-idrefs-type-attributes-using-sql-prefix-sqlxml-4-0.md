---
title: 'Atributos de ID válidos usando SQL: prefix (SQLXML)'
description: 'Saiba como criar atributos de tipo ID, IDREF e IDREFS válidos usando SQL: prefix (SQLXML 4,0).'
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- IDREFS relationships [SQLXML]
- annotated XSD schemas, ID type attribute
- IDREF type attribute [SQLXML]
- annotated XSD schemas, IDREFS type attribute
- ID type attribute [SQLXML]
- sql:prefix
- prefix annotation
- IDREF relationships [SQLXML]
- IDREFS type attribute [SQLXML]
- annotated XSD schemas, IDREF type attribute
- ID relationships [SQLXML]
ms.assetid: 1c7f77d3-81f3-4820-bb63-c4aaa4ea9aa1
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 51e236b690c8523337b66d19a9b47755a6117f0c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97415716"
---
# <a name="creating-valid-id-idref-and-idrefs-type-attributes-using-sqlprefix-sqlxml-40"></a>Criando atributos de tipo ID, IDREF e IDREFS válidos usando sql:prefix (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Um atributo pode ser especificado como um atributo de tipo ID. Atributos especificados como IDREF ou IDREFS poderão, então, ser usados para fazer referência aos atributos de tipo ID, permitindo vínculos entre documentos.  
  
 ID, IDREF e IDREFS correspondem a relações CP/FK (chave primária/chave estrangeira) no banco de dados, com poucas diferenças. Em um documento XML, os valores de atributos de tipo ID devem ser distintos. Se os atributos **CustomerID** e **OrderID** forem especificados como tipo de ID em um documento XML, esses valores deverão ser distintos. No entanto, em um banco de dados, as colunas CustomerID e OrderID podem ter os mesmos valores. (Por exemplo, CustomerID = 1 e OrderID = 1 são válidos no banco de dados.)  
  
 Para que os atributos ID, IDREF e IDREFS sejam válidos:  
  
-   O valor de ID deve ser exclusivo dentro do documento XML.  
  
-   Para todos os atributos IDREF e IDREFS, os valores de ID referenciados devem estar no documento XML.  
  
-   O valor de um atributo ID, IDREF e IDREFS deve ser um token nomeado. (Por exemplo, o valor inteiro 101 não pode ser um valor de ID.)  
  
-   Os atributos de ID, IDREF e IDREFS não podem ser mapeados para colunas do tipo **Text**, **ntext** ou **Image** ou qualquer outro tipo de dados binary (por exemplo, **timestamp**).  
  
 Se um documento XML contiver várias IDs, use a anotação **SQL: prefix** para garantir que os valores sejam exclusivos.  
  
 Observe que **SQL:** a anotação de prefixo não pode ser usada com atributo xsd fixo.  
  
## <a name="examples"></a>Exemplos  
 Para criar exemplos de funcionamento usando os exemplos a seguir, é necessário atender a determinados requisitos. Para obter mais informações, consulte [Requirements for running SQLXML examples](../../relational-databases/sqlxml/requirements-for-running-sqlxml-examples.md).  
  
### <a name="a-specifying-id-and-idrefs-types"></a>a. Especificando os tipos ID e IDREFS  
 No esquema a seguir, o **\<Customer>** elemento consiste no **\<Order>** elemento filho. O **\<Order>** elemento também tem um elemento filho, o **\<OrderDetail>** elemento.  
  
 O atributo **OrderIDList** de **\<Customer>** é um atributo de tipo IDREFS que se refere ao atributo **OrderID** do **\<Order>** elemento.  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustOrders"  
                 parent="Sales.Customer"  
                 parent-key="CustomerID"  
                 child="Sales.SalesOrderHeader"  
                 child-key="CustomerID" />  
    <sql:relationship name="OrderOrderDetail"  
                 parent="Sales.SalesOrderHeader"  
                 parent-key="SalesOrderID"  
                 child="Sales.SalesOrderDetail"  
                 child-key="SalesOrderID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  <xsd:element name="Customer" sql:relation="Sales.Customer" >  
   <xsd:complexType>  
     <xsd:sequence>  
        <xsd:element name="Order" sql:relation="Sales.SalesOrderHeader"    
               sql:relationship="CustOrders" maxOccurs="unbounded" >  
          <xsd:complexType>  
              <xsd:sequence>  
                <xsd:element name="OrderDetail"   
                             sql:relation="Sales.SalesOrderDetail"   
                   sql:relationship="OrderOrderDetail"   
                   maxOccurs="unbounded" >  
                  <xsd:complexType>  
                   <xsd:attribute name="SalesOrderID" type="xsd:integer" />  
                   <xsd:attribute name="ProductID" type="xsd:string" />  
                   <xsd:attribute name="OrderQty" type="xsd:integer" />  
                  </xsd:complexType>  
               </xsd:element>  
             </xsd:sequence>  
             <xsd:attribute name="SalesOrderID"   
                            type="xsd:ID" sql:prefix="ord-" />  
             <xsd:attribute name="OrderDate" type="xsd:date" />  
             <xsd:attribute name="CustomerID" type="xsd:string" />  
          </xsd:complexType>  
      </xsd:element>  
    </xsd:sequence>  
    <xsd:attribute name="CustomerID" type="xsd:string" />  
    <xsd:attribute name="OrderIDList" type="xsd:IDREFS"   
                   sql:relation="Sales.SalesOrderHeader" sql:field="SalesOrderID"  
                   sql:relationship="CustOrders" sql:prefix="ord-">  
    </xsd:attribute>  
  </xsd:complexType>  
</xsd:element>  
</xsd:schema>  
```  
  
##### <a name="to-test-a-sample-xpath-query-against-the-schema"></a>Para testar uma consulta XPath de exemplo com relação ao esquema  
  
1.  Copie o código de esquema acima e cole-o em um arquivo de texto. Salve o arquivo como sqlPrefix.xml.  
  
2.  Copie o modelo a seguir e cole-o em um arquivo de texto. Salve o arquivo como sqlPrefixT.xml no mesmo diretório onde você salvou sqlPrefix.xml.  
  
    ```  
    <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
      <sql:xpath-query mapping-schema="sqlPrefix.xml">  
        /Customer[@CustomerID=1]  
      </sql:xpath-query>  
    </ROOT>  
    ```  
  
     O caminho de diretório especificado para o esquema de mapeamento (sqlPrefix.xml) é relativo ao diretório onde o modelo está salvo. Também é possível especificar um caminho absoluto, por exemplo:  
  
    ```  
    mapping-schema="C:\SqlXmlTest\sqlPrefix.xml"  
    ```  
  
3.  Crie e use o script de teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o modelo.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML](../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
 Este é o resultado parcial:  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Customer CustomerID="1" OrderIDList="ord-43860 ord-44501 ord-45283 ord-46042">  
    <Order SalesOrderID="ord-43860" OrderDate="2001-08-01" CustomerID="1">  
      <OrderDetail SalesOrderID="43860" ProductID="729" OrderQty="1" />   
      <OrderDetail SalesOrderID="43860" ProductID="732" OrderQty="1" />   
      <OrderDetail SalesOrderID="43860" ProductID="738" OrderQty="1" />   
      <OrderDetail SalesOrderID="43860" ProductID="753" OrderQty="2" />   
      ...  
    </Order>  
    ...  
 </Customer>  
</ROOT>  
```  
  
  
