---
title: Formatação XML do lado do cliente (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- FOR XML clause, formatting
- middle tier XML formatting [SQLXML]
- client-side XML formatting
- client-side-xml attribute
ms.assetid: 9630a21d-a93b-4d3b-8a25-c4b32399f993
author: rothja
ms.author: jroth
ms.openlocfilehash: 9ac825cf6fa86e6a1f4970cffafc20d2873558b2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "84996053"
---
# <a name="client-side-xml-formatting-sqlxml-40"></a>Formatação XML do lado do cliente (SQLXML 4.0)
  Este tópico fornece informações sobre formatação de XML do lado do cliente. A formatação do lado do cliente refere-se à formatação de XML na camada intermediária.  
  
> [!NOTE]  
>  Este tópico fornece informações adicionais sobre como usar a cláusula FOR XML no lado do cliente e supõe que você já esteja familiarizado com a cláusula FOR XML. Para obter mais informações sobre o FOR XML, consulte [construindo XML Using for XML](../../xml/for-xml-sql-server.md).  
  
 **Importante** Para usar a funcionalidade para XML do lado do cliente com o novo `xml` tipo de dados, os clientes sempre devem usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de dados do Native Client (SQLNCLI11) em vez do provedor SQLOLEDB. SQLNCLI11 é a última versão do provedor do SQL Server e compreende plenamente os tipos de dados introduzidos no [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. O comportamento da cláusula FOR XML do lado do cliente com o provedor SQLOLEDB tratará os tipos de dados `xml` como cadeias de caracteres.  
  
## <a name="formatting-xml-documents-on-the-client-side"></a>Formatando documentos XML no lado do cliente  
 Quando um aplicativo cliente executa a seguinte consulta:  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
FOR XML RAW  
```  
  
 ...só esta parte da consulta é enviada ao servidor:  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
```  
  
 O servidor executa a consulta e retorna um conjunto de linhas (que contém FirstName e LastNamecolumns) para o cliente. A camada intermediária aplica as informações de FOR XML ao conjunto de linhas e retorna a formatação XML ao cliente.  
  
 De maneira similar, quando você executa uma consulta XPath, o servidor retorna o conjunto de linhas ao cliente e a transformação FOR XML EXPLICIT é aplicada ao conjunto de linhas no cliente, gerando a formatação XML desejada.  
  
 A tabela a seguir mostra os modos que você pode especificar com a cláusula FOR XML do lado do cliente.  
  
|Modo FOR XML do lado do cliente|Comentário|  
|-------------------------------|-------------|  
|RAW|Gera resultados idênticos quando especificado em FOR XML do lado do cliente ou do lado do servidor.|  
|NESTED|É semelhante ao modo FOR XML AUTO no lado do servidor.|  
|EXPLICIT|É semelhante ao modo FOR XML EXPLICIT do lado do servidor.|  
  
> [!NOTE]  
>  Se você especificar o modo AUTO e solicitar a formatação XML do lado do cliente, toda a consulta será enviada ao servidor, isto é, a formatação XML ocorrerá no servidor. Isto será feito por conveniência, mas observe que o modo NESTED retorna os nomes das tabelas base como nomes de elemento no documento XML gerado. Alguns dos aplicativos que você grava podem exigir nomes de tabela base. Por exemplo, você pode executar um procedimento armazenado e carregar os dados resultantes em um Dataset (no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework) e gerar posteriormente um DiffGram para atualizar dados nas tabelas. Em tal caso, você precisará das informações da tabela base e precisará usar o modo NESTED.  
  
## <a name="benefits-of-client-side-xml-formatting"></a>Benefícios da formatação XML do lado do cliente  
 A seguir, são descritos alguns benefícios da formatação XML no cliente.  
  
### <a name="if-you-have-stored-procedures-on-the-server-that-return-a-single-rowset-you-can-request-client-side-for-xml-transformation-to-generate-an-xml"></a>Se você tiver procedimentos armazenados no servidor que retornem um único conjunto de linhas, poderá solicitar que a transformação FOR XML do lado do cliente gere um XML.  
 Por exemplo, considere o procedimento armazenado a seguir. Esse procedimento retorna o nome e o sobrenome dos funcionários da tabela Person.Contact no banco de dados AdventureWorks:  
  
```  
IF EXISTS (SELECT name FROM sysobjects  
   WHERE name = 'GetContacts' AND type = 'P')  
   DROP PROCEDURE GetContacts  
GO  
CREATE PROCEDURE GetContacts  
AS  
    SELECT   FirstName, LastName  
    FROM     Person.Contact  
```  
  
 O exemplo de modelo XML a seguir executa o procedimento armazenado. A cláusula FOR XML é especificada depois do nome de procedimento armazenado.  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query client-side-xml="1">  
    EXEC GetContacts FOR XML NESTED  
  </sql:query>  
</ROOT>  
```  
  
 Como o atributo **XML do lado do cliente** é definido como 1 (true) no modelo, o procedimento armazenado é executado no servidor e o conjunto de linhas de duas colunas que é retornado pelo servidor é transformado em XML na camada intermediária e retornado ao cliente. (Somente um resultado parcial é mostrado aqui.)  
  
```  
 <ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Person.Contact FirstName="Gustavo" LastName="Achong" />   
  <Person.Contact FirstName="Catherine" LastName="Abel" />  
</ROOT>  
```  
  
> [!NOTE]  
>  Quando estiver usando o Provedor SQLXMLOLEDB ou as Classes Gerenciadas por SQLXML, você poderá usar a propriedade `ClientSideXml` para solicitar a formatação XML do lado do cliente.  
  
### <a name="the-workload-is-more-balanced"></a>A carga de trabalho é mais equilibrada.  
 Como o cliente executa a formatação XML, a carga de trabalho é equilibrada entre o servidor e o cliente, liberando o servidor para fazer outras coisas.  
  
## <a name="supporting-client-side-xml-formatting"></a>Dando suporte à formatação XML do lado do cliente  
 Para dar suporte à funcionalidade de formatação XML do lado do cliente, o SQLXML fornece:  
  
-   Provedor SQLXMLOLEDB  
  
-   Classes gerenciadas SQLXML  
  
-   Suporte de modelo XML avançado  
  
-   Propriedade SqlXmlCommand. ClientSideXml  
  
     Você pode especificar a formatação do lado do cliente definindo essa propriedade das classes gerenciadas SQLXML como true.  
  
## <a name="enhanced-xml-template-support"></a>Suporte a modelos XML aprimorados  
 A partir do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] , o modelo XML no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] foi aprimorado com a adição do atributo **XML do lado do cliente** . Se esse atributo for definido como true, XML será formatado no cliente. Observe que esse atributo de modelo é idêntico em funcionalidade para a propriedade ClientSideXML específica do provedor SQLXMLOLEDB.  
  
> [!NOTE]  
>  Se você executar um modelo XML em um aplicativo ADO que está usando o provedor SQLXMLOLEDB e especificar tanto o atributo **XML do lado do cliente** no modelo quanto a propriedade ClientSideXML do provedor, o valor especificado no modelo terá precedência.  
  
## <a name="see-also"></a>Consulte Também  
 [Arquitetura da formatação XML do lado do cliente e do servidor &#40;SQLXML 4,0&#41;](server-side-xml-formatting-sqlxml-4-0.md)   
 [FOR XML &#40;SQL Server&#41;](../../xml/for-xml-sql-server.md)   
 [Considerações sobre segurança de FOR XML &#40;SQLXML 4,0&#41;](../../sqlxml-annotated-xsd-schemas-xpath-queries/security/for-xml-security-considerations-sqlxml-4-0.md)   
 [Suporte a tipo de dados XML no SQLXML 4,0](../xml-data-type-support-in-sqlxml-4-0.md)   
 [Classes gerenciadas SQLXML](../../sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-4-0-net-framework-support-managed-classes.md)   
 [Formatação XML do lado do cliente versus do servidor &#40;SQLXML 4,0&#41;](client-side-vs-server-side-xml-formatting-sqlxml-4-0.md)   
 [Objeto SqlXmlCommand &#40;classes gerenciadas SQLXML&#41;](../../sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmlcommand-object.md)   
 [Dados XML &#40;SQL Server&#41;](../../xml/xml-data-sql-server.md)  
  
  
