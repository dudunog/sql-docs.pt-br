---
title: Exemplos de DiffGram (SQLXML)
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- DiffGrams [SQLXML], examples
- examples [SQLXML], DiffGram
- diffgr:parentID
- parentID annotation
ms.assetid: fc148583-dfd3-4efb-a413-f47b150b0975
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6fe05c49f44bc0e210687b63e0eb8878b479a07f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75257259"
---
# <a name="diffgram-examples-sqlxml-40"></a>Exemplos de DiffGram (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Os exemplos deste tópico consistem em DiffGrams que executam operações de inserção, atualização e exclusão no banco de dados. Antes de usar os exemplos, observe o seguinte:  
  
-   Os exemplos usarão duas tabelas (Cust e Ord) que devem ser criadas se você quiser testar os exemplos de DiffGram:  
  
    ```  
    Cust(CustomerID, CompanyName, ContactName)  
    Ord(OrderID, CustomerID)  
    ```  
  
-   A maioria dos exemplos deste tópico usa o seguinte Esquema XSD:  
  
    ```  
    <xsd:schema xmlns:xsd="http://www.w3.org/2001/XMLSchema"  
                xmlns:sql="urn:schemas-microsoft-com:mapping-schema">  
  
    <xsd:annotation>  
      <xsd:documentation>  
        Diffgram Customers/Orders Schema.  
      </xsd:documentation>  
      <xsd:appinfo>  
           <sql:relationship name="CustomersOrders"   
                      parent="Cust"  
                      parent-key="CustomerID"  
                      child-key="CustomerID"  
                      child="Ord"/>  
      </xsd:appinfo>  
    </xsd:annotation>  
  
    <xsd:element name="Customer" sql:relation="Cust">  
      <xsd:complexType>  
        <xsd:sequence>  
          <xsd:element name="CompanyName"    type="xsd:string"/>  
          <xsd:element name="ContactName"    type="xsd:string"/>  
           <xsd:element name="Order" sql:relation="Ord" sql:relationship="CustomersOrders">  
            <xsd:complexType>  
              <xsd:attribute name="OrderID" type="xsd:int" sql:field="OrderID"/>  
              <xsd:attribute name="CustomerID" type="xsd:string"/>  
            </xsd:complexType>  
          </xsd:element>  
        </xsd:sequence>  
        <xsd:attribute name="CustomerID" type="xsd:string" sql:field="CustomerID"/>  
      </xsd:complexType>  
    </xsd:element>  
  
    </xsd:schema>     
    ```  
  
     Salve este esquema como DiffGramSchema.xml na mesma pasta em que você salva outros arquivos usados nos exemplos.  
  
## <a name="a-deleting-a-record-by-using-a-diffgram"></a>A. Excluindo um registro usando um DiffGram  
 O DiffGram, neste exemplo, exclui um registro de cliente (com CustomerID ALFKI) da tabela Cust e exclui o registro de pedido correspondente (cuja OrderID é 1) da tabela Ord.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance/>  
  
    <diffgr:before>  
        <Order diffgr:id="Order1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI"   
               OrderID="1"/>  
        <Customer diffgr:id="Customer1"   
                  msdata:rowOrder="0"   
                  CustomerID="ALFKI">  
           <CompanyName>Alfreds Futterkiste</CompanyName>  
           <ContactName>Maria Anders</ContactName>  
        </Customer>  
    </diffgr:before>  
    <msdata:errors/>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 No bloco ** \<before>** , há um ** \<elemento Order>** (**diffgr: ID = "Order1"**) e um ** \<elemento Customer>** (**diffgr: ID = "Customer1"**). Esses elementos representam registros existentes no banco de dados. O elemento de ** \<>de DataInstance** não tem os registros correspondentes (com o mesmo **diffgr: ID**). Isso indica um operação de exclusão.  
  
#### <a name="to-test-the-diffgram"></a>Para testar o DiffGram  
  
1.  Crie essas tabelas no banco de dados **tempdb** .  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  Adicione estes dados de exemplo:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Copie o DiffGram acima e cole em um arquivo de texto. Salve o arquivo como MyDiffGram.xml na mesma pasta usada na etapa anterior.  
  
4.  Copie o DiffGramSchema fornecido anteriormente neste tópico e cole-o em um arquivo de texto. Salve o arquivo como DiffGramSchema.xml.  
  
5.  Crie e use o Script de Teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o DiffGram.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="b-inserting-a-record-by-using-a-diffgram"></a>B. Inserindo um registro usando um DiffGram  
 Neste exemplo, o DiffGram insere um registro na tabela Cust e um registro na tabela Ord.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql"   
      sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
          xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
          xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
       <Customer diffgr:id="Customer1" msdata:rowOrder="0"    
                 diffgr:hasChanges="inserted" CustomerID="ALFKI">  
        <CompanyName>C3Company</CompanyName>  
        <ContactName>C3Contact</ContactName>  
        <Order diffgr:id="Order1"   
               msdata:rowOrder="0"  
               diffgr:hasChanges="inserted"   
               CustomerID="ALFKI" OrderID="1"/>  
      </Customer>  
    </DataInstance>  
  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 Neste DiffGram, o ** \<bloco before>** não é especificado (nenhum registro de banco de dados existente foi identificado). Há duas instâncias de registro (identificadas pelo ** \<cliente>** e ** \<Order>** elementos no bloco de ** \<>de DataInstance** ) que são mapeadas para as tabelas Cust e Ord, respectivamente. Ambos os elementos especificam o atributo **diffgr: hasChanges** (**HasChanges = "inserted"**). Isso indica uma operação de inserção. Nesse DiffGram, se você especificar **HasChanges = "Modified"**, você está indicando que deseja modificar um registro que não existe, o que resulta em um erro.  
  
#### <a name="to-test-the-diffgram"></a>Para testar o DiffGram  
  
1.  Crie essas tabelas no banco de dados **tempdb** .  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  Adicione estes dados de exemplo:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Copie o DiffGram acima e cole em um arquivo de texto. Salve o arquivo como MyDiffGram.xml na mesma pasta usada na etapa anterior.  
  
4.  Copie o DiffGramSchema fornecido anteriormente neste tópico e cole-o em um arquivo de texto. Salve o arquivo como DiffGramSchema.xml.  
  
5.  Crie e use o Script de Teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o DiffGram.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="c-updating-an-existing-record-by-using-a-diffgram"></a>C. Atualizando um registro existente usando um DiffGram  
 Neste exemplo, o DiffGram atualiza as informações do cliente (CompanyName e ContactName) de ALFKI do cliente.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
           xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
           xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer1"   
                msdata:rowOrder="0" diffgr:hasChanges="modified"   
                CustomerID="ALFKI">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Antonio Moreno</ContactName>  
      </Customer>  
    </DataInstance>  
  
    <diffgr:before>  
     <Customer diffgr:id="Customer1"   
               msdata:rowOrder="0"   
               CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
    </diffgr:before>  
  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 O ** \<bloco before>** inclui um ** \<elemento Customer>** (**diffgr: ID = "Customer1"**). O bloco de ** \<>de DataInstance** inclui o elemento de ** \<>do cliente** correspondente com a mesma **ID**. O ** \<elemento>do cliente** na ** \<>de NewDataSet** também especifica **diffgr: hasChanges = "Modified"**. Isso indica uma operação de atualização e o registro de cliente na tabela **cust** é atualizado de acordo. Observe que, se o atributo **diffgr: hasChanges** não for especificado, a lógica de processamento de DiffGram ignorará esse elemento e nenhuma atualização será executada.  
  
#### <a name="to-test-the-diffgram"></a>Para testar o DiffGram  
  
1.  Crie essas tabelas no banco de dados **tempdb** .  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  Adicione estes dados de exemplo:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Copie o DiffGram acima e cole em um arquivo de texto. Salve o arquivo como MyDiffGram.xml na mesma pasta usada na etapa anterior.  
  
4.  Copie o DiffGramSchema fornecido anteriormente neste tópico e cole-o em um arquivo de texto. Salve o arquivo como DiffGramSchema.xml.  
  
5.  Crie e use o Script de Teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o DiffGram.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="d-inserting-updating-and-deleting-records-by-using-a-diffgram"></a>D. Inserindo, atualizando e excluindo registros usando um DiffGram  
 Neste exemplo, um DiffGram relativamente complexo é usado para executar operações de inserção, atualização e exclusão.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql" sql:mapping-schema="DiffGramSchema.xml">  
  <diffgr:diffgram   
         xmlns:msdata="urn:schemas-microsoft-com:xml-msdata"   
         xmlns:diffgr="urn:schemas-microsoft-com:xml-diffgram-v1">  
    <DataInstance>  
      <Customer diffgr:id="Customer2" msdata:rowOrder="1"   
                diffgr:hasChanges="modified"   
                CustomerID="ANATR">  
          <CompanyName>Bottom Dollar Markets</CompanyName>  
          <ContactName>Elizabeth Lincoln</ContactName>  
          <Order diffgr:id="Order2" msdata:rowOrder="1"   
               msdata:hiddenCustomerID="ANATR"   
               CustomerID="ANATR" OrderID="2"/>  
      </Customer>  
  
      <Customer diffgr:id="Customer3" msdata:rowOrder="2"   
                CustomerID="ANTON">  
         <CompanyName>Chop-suey Chinese</CompanyName>  
         <ContactName>Yang Wang</ContactName>  
         <Order diffgr:id="Order3" msdata:rowOrder="2"   
               msdata:hiddenCustomerID="ANTON"   
               CustomerID="ANTON" OrderID="3"/>  
      </Customer>  
      <Customer diffgr:id="Customer4" msdata:rowOrder="3"   
                diffgr:hasChanges="inserted"   
                CustomerID="AROUT">  
         <CompanyName>Around the Horn</CompanyName>  
         <ContactName>Thomas Hardy</ContactName>  
         <Order diffgr:id="Order4" msdata:rowOrder="3"   
                diffgr:hasChanges="inserted"   
                msdata:hiddenCustomerID="AROUT"   
               CustomerID="AROUT" OrderID="4"/>  
      </Customer>  
    </DataInstance>  
    <diffgr:before>  
      <Order diffgr:id="Order1" msdata:rowOrder="0"   
             msdata:hiddenCustomerID="ALFKI"   
             CustomerID="ALFKI" OrderID="1"/>  
      <Customer diffgr:id="Customer1" msdata:rowOrder="0"   
                CustomerID="ALFKI">  
        <CompanyName>Alfreds Futterkiste</CompanyName>  
        <ContactName>Maria Anders</ContactName>  
      </Customer>  
      <Customer diffgr:id="Customer2" msdata:rowOrder="1"   
                CustomerID="ANATR">  
        <CompanyName>Ana Trujillo Emparedados y helados</CompanyName>  
        <ContactName>Ana Trujillo</ContactName>  
      </Customer>  
    </diffgr:before>  
  </diffgr:diffgram>  
</ROOT>  
```  
  
 A lógica do DiffGram processa este DiffGram como a seguir:  
  
-   De acordo com a lógica de processamento DiffGram, todos os elementos de nível superior no bloco ** \<before>** são mapeados para tabelas correspondentes, conforme descrito no esquema de mapeamento.  
  
-   O ** \<bloco before>** tem um ** \<elemento Order>** (**dffgr: ID = "Order1"**) e um ** \<elemento Customer>** (**diffgr: ID = "Customer1"**) para o qual não há nenhum elemento correspondente no ** \<bloco DataInstance>** (com a mesma ID). Isto indica uma operação de exclusão e os registros são excluídos das tabelas Cust e Ord.  
  
-   O ** \<bloco before>** tem um ** \<** elemento de>de cliente (**diffgr: ID = "customer2"**) para o qual há um elemento ** \<>de cliente** correspondente no bloco de ** \<>de DataInstance** (com a mesma ID). O elemento no bloco de ** \<>de DataInstance** especifica **diffgr: hasChanges = "Modified"**. Esta é uma operação de atualização na qual para clientes ANATR, as informações CompanyName e ContactName são atualizadas na tabela Cust usando valores que são especificados no ** \<bloco>** de dados de instância.  
  
-   O bloco de ** \<>de DataInstance** tem um elemento de ** \<>de cliente** (**diffgr: ID = "Customer3"**) e um ** \<** elemento de>de ordem (**diffgr: ID = "Order3"**). Nenhum desses elementos especifica o atributo **diffgr: hasChanges** . Portanto, a lógica de processamento do DiffGram ignora esses elementos.  
  
-   O bloco de ** \<>de DataInstance** tem um elemento de ** \<>de cliente** (**diffgr: ID = "Customer4"**) e um ** \<** elemento de>de ordem (**diffgr: ID = "Order4"**) para o qual \<não há nenhum elemento correspondente no bloco before>. Esses elementos no bloco de ** \<>de DataInstance** especificam **diffgr: hasChanges = "inserted"**. Portanto, um registro novo é adicionado na tabela Cust e na tabela Ord.  
  
#### <a name="to-test-the-diffgram"></a>Para testar o DiffGram  
  
1.  Crie as tabelas a seguir no banco de dados **tempdb** .  
  
    ```  
    CREATE TABLE Cust(  
            CustomerID  nchar(5) Primary Key,  
            CompanyName nvarchar(40) NOT NULL ,  
            ContactName nvarchar(60) NULL)  
    GO  
  
    CREATE TABLE Ord(  
       OrderID    int Primary Key,  
       CustomerID nchar(5) Foreign Key REFERENCES Cust(CustomerID))  
    GO  
    ```  
  
2.  Adicione estes dados de exemplo:  
  
    ```  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ALFKI', N'Alfreds Futterkiste', N'Maria Anders')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANATR', N'Ana Trujillo Emparedados y helados', N'Ana Trujillo')  
    INSERT INTO Cust(CustomerID, CompanyName, ContactName) VALUES  
         (N'ANTON', N'Antonio Moreno Taquería', N'Antonio Moreno')  
  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(1, N'ALFKI')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(2, N'ANATR')  
    INSERT INTO Ord(OrderID, CustomerID) VALUES(3, N'ANTON')  
    ```  
  
3.  Copie o DiffGram acima e cole em um arquivo de texto. Salve o arquivo como MyDiffGram.xml na mesma pasta usada na etapa anterior.  
  
4.  Copie o DiffGramSchema fornecido anteriormente neste tópico e cole-o em um arquivo de texto. Salve o arquivo como DiffGramSchema.xml.  
  
5.  Crie e use o Script de Teste SQLXML 4.0 (Sqlxml4test.vbs) para executar o DiffGram.  
  
     Para obter mais informações, consulte [usando o ADO para executar consultas do SQLXML 4,0](../../../relational-databases/sqlxml/using-ado-to-execute-sqlxml-4-0-queries.md).  
  
## <a name="e-applying-updates-by-using-a-diffgram-with-the-diffgrparentid-annotation"></a>E. Aplicando atualizações usando um DiffGram com a anotação diffgr:parentID  
 Este exemplo ilustra como a anotação **parentID** especificada no bloco ** \<before>** do DiffGram é usada na aplicação das atualizações.  
  
```  
<NewDataSet />  
<diffgr:before>  
   <Order diffgr:id="Order1" msdata:rowOrder="0" OrderID="2" />  
   <Order diffgr:id="Order3" msdata:rowOrder="2" OrderID="4" />  
  
   <OrderDetail diffgr:id="OrderDetail1"   
                diffgr:parentId="Order1"   
                msdata:rowOrder="0"   
                ProductID="13"   
                OrderID="2" />  
   <OrderDetail diffgr:id="OrderDetail3"   
                diffgr:parentId="Order3"  
                ProductID="77"  
                OrderID="4"/>  
</diffgr:before>  
</diffgr:diffgram>  
```  
  
 Este DiffGram especifica uma operação de exclusão porque há apenas um ** \<bloco before>** . No DiffGram, a anotação **parentID** é usada para especificar uma relação pai-filho entre os pedidos e os detalhes do pedido. Quando SQLXML exclui os registros, ele exclui registros da tabela filho identificada por essa relação e, em seguida, exclui os registros da tabela pai correspondente.  
  
  
