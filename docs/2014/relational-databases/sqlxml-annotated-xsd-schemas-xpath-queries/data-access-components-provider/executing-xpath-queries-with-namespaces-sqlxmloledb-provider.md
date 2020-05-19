---
title: Executando consultas XPath com namespaces (provedor SQLXMLOLEDB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, executing XPath queries
- namespaces property
- queries [SQLXML], SQLXMLOLEDB Provider
- XPath queries [SQLXML], namespaces
- XPath queries [SQLXML], SQLXMLOLEDB Provider
- namespaces [SQLXML], XPath queries
ms.assetid: 024a4b7d-435d-47ba-9e80-2c2f640108f5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: fa708c4b439e3a556ea7dac345cc04f32c59e2d6
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82703227"
---
# <a name="executing-xpath-queries-with-namespaces-sqlxmloledb-provider"></a>Executando consultas XPath com namespaces (provedor SQLXMLOLEDB)
  As consultas XPath podem incluir namespaces. Se os elementos de esquema forem qualificados por namespace (ou seja, se incluírem um namespace de destino), as consultas XPath com relação ao esquema precisarão especificar esse namespace.  
  
 Como não há suporte ao uso do caractere curinga (*) no SQLXML 4.0, você precisa especificar a consulta XPath usando um prefixo de namespace. Para resolver esse prefixo, use a propriedade namespaces para especificar a associação de namespace.  
  
 No exemplo a seguir, a consulta XPath especifica namespaces usando o caractere curinga ( \* ) e as funções XPath de nome local () e namespace-URI (). Essa consulta XPath retorna todos os elementos em que o nome local é `Contact` e o URI de namespace é `urn:myschema:Contacts`.  
  
```  
/*[local-name() = 'Contact' and namespace-uri() = 'urn:myschema:Contacts']  
```  
  
 No SQLXML 4.0, essa consulta XPath deve ser especificada com um prefixo de namespace. Um exemplo é `x:Contact`, em que `x` é o prefixo de namespace. Considere o esquema XSD a seguir:  
  
```  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
            xmlns:sql="urn:schemas-microsoft-com:mapping-schema"  
            xmlns:con="urn:myschema:Contacts"  
            targetNamespace="urn:myschema:Contacts">  
<complexType name="ContactType">  
  <attribute name="CID" sql:field="ContactID" type="ID"/>  
  <attribute name="FName" sql:field="FirstName" type="string"/>  
  <attribute name="LName" sql:field="LastName"/>   
</complexType>  
<element name="Contact" type="con:ContactType" sql:relation="Person.Contact"/>  
</schema>  
```  
  
 Como esse esquema define o namespace de destino, uma consulta XPath (como "Employee") com relação ao esquema precisa incluir o namespace.  
  
 Este é um aplicativo de exemplo do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic que executa uma consulta XPath (x:Employee) no esquema XSD anterior. Para resolver o prefixo, a associação de namespace é especificada usando a propriedade namespaces.  
  
> [!NOTE]  
>  No código, é necessário fornecer o nome da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na cadeia de conexão. Este exemplo também especifica o uso do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (SQLNCLI11) para o provedor de dados, o que requer a instalação adicional do software cliente da rede. Para obter mais informações, consulte [requisitos do sistema para SQL Server Native Client](../../native-client/system-requirements-for-sql-server-native-client.md).  
  
```  
Option Explicit  
Private Sub Form_Load()  
    Dim con As New ADODB.Connection  
    Dim cmd As New ADODB.Command  
    Dim stm As New ADODB.Stream  
    con.Open "provider=SQLXMLOLEDB.4.0;Data Provider=SQLNCLI11;Data Source=SqlServerName;Initial Catalog=AdventureWorks;Integrated Security=SSPI;"  
    Set cmd.ActiveConnection = con  
    stm.Open  
    cmd.Properties("Output Stream").Value = stm  
    cmd.Properties("Output Encoding") = "utf-8"  
    cmd.Properties("Mapping schema") = "C:\DirectoryPath\con-ex.xml"  
    cmd.Properties("namespaces") = "xmlns:x='urn:myschema:Contacts'"  
    '  Debug.Print "Set Command Dialect to DBGUID_XPATH"  
    cmd.Dialect = "{ec2a4293-e898-11d2-b1b7-00c04f680c56}"  
    cmd.CommandText = "x:Contact"  
    cmd.Execute , , adExecuteStream   
    stm.Position = 0  
    Debug.Print stm.ReadText(adReadAll)  
End Sub  
```  
  
### <a name="to-test-this-application"></a>Para testar esse aplicativo  
  
1.  Salve o esquema XSD do exemplo em uma pasta.  
  
2.  Crie um projeto executável do Visual Basic e copie o código nele. Altere o caminho de diretório especificado conforme apropriado.  
  
3.  Adicione a seguinte referência de projeto:  
  
    ```  
    "Microsoft ActiveX Data Objects 2.8 Library"  
    ```  
  
4.  Execute o aplicativo.  
  
 Este é o resultado parcial:  
  
```  
<y0:Employee xmlns:y0="urn:myschema:Contacts"   
             LName="Achong" CID="1" FName="Gustavo"/>  
<y0:Employee xmlns:y0="urn:myschema:Employees"   
             LName="Abel" CID="2" FName="Catherine"/>  
```  
  
 Os prefixos gerados no documento XML são arbitrários, mas são mapeados para o mesmo namespace.  
  
  
