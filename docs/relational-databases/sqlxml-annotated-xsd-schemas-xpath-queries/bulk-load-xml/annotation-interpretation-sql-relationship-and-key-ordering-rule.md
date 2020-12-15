---
title: 'SQL: relação e a regra de ordenação de chave (SQLXML)'
description: 'Saiba como usar o elemento SQL: relationship e as regras de ordenação de chave no SQLXML.'
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- sql:relationship
- key ordering rules [SQLXML]
- relationship annotation
ms.assetid: 914cb152-09f5-4b08-b35d-71940e4e9986
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1846a3db3194a81ce1d1522ac175e3988d3d3d23
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97462927"
---
# <a name="annotation-interpretation---sqlrelationship-and-key-ordering-rule"></a>Interpretação de anotação – sql:relationship e Regra de ordenação de chave
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Como o XML Bulk Load gera registro à medida que seus nós entram no escopo e envia esses registros para o Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] à medida que seus nós saem do escopo, os dados do registro devem estar presentes no escopo do nó.  
  
 Considere o seguinte esquema XSD, no qual a relação de um para muitos entre **\<Customer>** elementos e **\<Order>** (um cliente pode inserir muitos pedidos) é especificada usando o **\<sql:relationship>** elemento:  
  
```  
<xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"<>   
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
<xsd:annotation>  
  <xsd:appinfo>  
    <sql:relationship name="CustCustOrder"  
          parent="Cust"  
          parent-key="CustomerID"  
          child="CustOrder"  
          child-key="CustomerID" />  
  </xsd:appinfo>  
</xsd:annotation>  
  
  <xsd:element name="Customers" sql:relation="Cust" >  
   <xsd:complexType>  
     <xsd:sequence>  
       <xsd:element name="CustomerID"  type="xsd:integer" />  
       <xsd:element name="CompanyName" type="xsd:string" />  
       <xsd:element name="City"        type="xsd:string" />  
       <xsd:element name="Order"   
                          sql:relation="CustOrder"  
                          sql:relationship="CustCustOrder" >  
         <xsd:complexType>  
          <xsd:attribute name="OrderID" type="xsd:integer" />  
         </xsd:complexType>  
       </xsd:element>  
     </xsd:sequence>  
    </xsd:complexType>  
  </xsd:element>  
</xsd:schema>  
```  
  
 Como o **\<Customer>** nó de elemento entra no escopo, o carregamento em massa de XML gera um registro de cliente. Esse registro permanece até leituras de carregamento em massa de XML **\</Customer>** . Ao processar o **\<Order>** nó do elemento, o carregamento em massa do XML usa **\<sql:relationship>** para obter o valor da coluna de chave estrangeira CustomerID da tabela CustOrder do **\<Customer>** elemento pai, porque o **\<Order>** elemento não especifica o atributo **CustomerID** . Isso significa que, ao definir o **\<Customer>** elemento, você deve especificar o atributo **CustomerID** no esquema antes de especificar **\<sql:relationship>** . Caso contrário, quando um **\<Order>** elemento entra no escopo, o carregamento em massa de XML gera um registro para a tabela CustOrder e, quando o carregamento em massa de XML atinge a **\</Order>** marca de fim, ele envia o registro para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sem o valor da coluna de chave estrangeira CustomerID.  
  
 Salve o esquema fornecido neste exemplo como SampleSchema.xml.  
  
### <a name="to-test-a-working-sample"></a>Para testar um exemplo de funcionamento  
  
1.  Crie estas tabelas:  
  
    ```  
    CREATE TABLE Cust (  
                  CustomerID     int          PRIMARY KEY,  
               CompanyName    varchar(20)  NOT NULL,  
                  City           varchar(20)  DEFAULT 'Seattle')  
    GO  
    CREATE TABLE CustOrder (  
                  OrderID        varchar(10) PRIMARY KEY,  
               CustomerID     int         FOREIGN KEY REFERENCES                                          Cust(CustomerID))  
    GO  
    ```  
  
2.  Salve os dados de exemplo a seguir como SampleXMLData.xml:  
  
    ```  
    <ROOT>    
      <Customers>  
        <CompanyName>Hanari Carnes</CompanyName>  
        <City>NY</City>  
        <Order OrderID="1" />  
        <Order OrderID="2" />  
        <CustomerID>1111</CustomerID>  
      </Customers>  
      <Customers>  
        <CompanyName>Toms Spezialitten</CompanyName>  
         <City>LA</City>    
        <Order OrderID="3" />  
        <CustomerID>1112</CustomerID>  
      </Customers>  
      <Customers>  
        <CompanyName>Victuailles en stock</CompanyName>  
        <Order OrderID="4" />  
        <CustomerID>1113</CustomerID>  
      </Customers>  
    </ROOT>  
    ```  
  
3.  Para executar o XML Bulk Load, salve e execute o seguinte exemplo do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic Scripting Edition (VBScript) como MySample.vbs:  

    ```  
    set objBL = CreateObject("SQLXMLBulkLoad.SQLXMLBulkload.4.0")  
    objBL.ConnectionString = "provider=SQLOLEDB;data source=localhost;database=tempdb;integrated security=SSPI"  
    objBL.ErrorLogFile = "c:\error.log"  
    objBL.CheckConstraints = True  
    objBL.Transaction=True  
    objBL.Execute "c:\SampleSchema.xml", "c:\SampleXMLData.xml"  
    set objBL=Nothing  
    ```  
  
     O resultado é que o XML Bulk Load insere um valor NULL na coluna de chave estrangeira CustomerID da tabela CustOrder. Se você revisar os dados de exemplo XML para que o **\<CustomerID>** elemento filho apareça antes do **\<Order>** elemento filho, obterá o resultado esperado: o carregamento em massa de XML insere o valor de chave estrangeira especificado na coluna.  
  
 Este é o esquema XDR equivalente:  
  
```  
<?xml version="1.0" ?>  
<Schema xmlns="urn:schemas-microsoft-com:xml-data"   
        xmlns:dt="urn:schemas-microsoft-com:xml:datatypes"    
        xmlns:sql="urn:schemas-microsoft-com:xml-sql" >   
   <ElementType name="CustomerID"  />  
   <ElementType name="CompanyName" />  
   <ElementType name="City"        />  
  
   <ElementType name="root" sql:is-constant="1">  
      <element type="Customers" />  
   </ElementType>  
  
   <ElementType name="Customers" sql:relation="Cust" >  
      <element type="CustomerID" sql:field="CustomerID" />  
      <element type="CompanyName" sql:field="CompanyName" />  
      <element type="City" sql:field="City" />  
      <element type="Order" >  
                 <sql:relationship  
                        key-relation    ="Cust"  
                        key             ="CustomerID"  
                        foreign-key     ="CustomerID"  
                        foreign-relation="CustOrder" />  
      </element>  
   </ElementType>  
    <ElementType name="Order" sql:relation="CustOrder" >  
      <AttributeType name="OrderID" />  
      <AttributeType name="CustomerID" />  
      <attribute type="OrderID" />  
      <attribute type="CustomerID" />  
    </ElementType>  
</Schema>  
```  
  
  
