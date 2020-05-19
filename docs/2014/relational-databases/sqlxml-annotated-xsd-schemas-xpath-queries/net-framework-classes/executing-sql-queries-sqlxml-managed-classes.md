---
title: Executando consultas SQL (classes gerenciadas SQLXML) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- queries [SQLXML], SQLXML Managed Classes
- SQLXML Managed Classes, executing SQL queries
- Managed Classes [SQLXML], executing SQL queries
- ExecuteToStream method
- SQL queries [SQLXML]
ms.assetid: a561ae83-a8b6-4b9b-a819-9b86839546b4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 07de51d3a5880b6b0d4ab6561fcf333a99387598
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718071"
---
# <a name="executing-sql-queries-sqlxml-managed-classes"></a>Executando consultas SQL (classes gerenciadas SQLXML)
  Este exemplo demonstra como:  
  
-   Criando parâmetros (objetos SqlXmlParameter).  
  
-   Atribuindo valores às propriedades (nome e valor) dos objetos SqlXmlParameter.  
  
 Neste exemplo, uma consulta SQL simples é executada para recuperar o nome, o sobrenome e a data de nascimento do funcionário cujo valor de sobrenome é passado como parâmetro. Ao especificar o parâmetro (*LastName*), somente a propriedade Value é definida. A propriedade Name não está definida, pois, nesta consulta, o parâmetro é posicional e nenhum nome é necessário.  
  
 A propriedade CommandType do objeto SqlXmlCommand, por padrão, é **SQL**. Portanto, a propriedade não é definida explicitamente.  
  
> [!NOTE]  
>  No código, é necessário fornecer o nome da instância do Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] na cadeia de conexão.  
  
 Este é o código C#:  
  
```  
using System;  
  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
      static string ConnString = "Provider=SQLOLEDB;Server=(local);database=AdventureWorks;Integrated Security=SSPI";  
      public static int testParams()  
      {  
         Stream strm;  
         SqlXmlParameter p;  
         SqlXmlCommand cmd = new SqlXmlCommand(ConnString);        
         cmd.CommandText = "SELECT FirstName, LastName FROM Person.Contact WHERE LastName=? For XML Auto";  
         p = cmd.CreateParameter();  
         p.Value = "Achong";  
         string strResult;  
         try   
         {  
            strm = cmd.ExecuteStream();  
            strm.Position = 0;  
            using(StreamReader sr = new StreamReader(strm))  
            {  
               Console.WriteLine(sr.ReadToEnd());  
            }  
         }  
         catch (SqlXmlException e)  
         {  
            //in case of an error, this prints error returned.  
            e.ErrorStream.Position=0;  
            strResult=new StreamReader(e.ErrorStream).ReadToEnd();  
            System.Console.WriteLine(strResult);  
         }  
  
         return 0;  
   }  
public static int Main(String[] args)  
{  
    testParams();  
    return 0;  
}  
}  
```  
  
### <a name="to-test-the-application"></a>Para testar o aplicativo  
  
1.  Salve o código C# (DocSample.cs) fornecido neste tópico em uma pasta.  
  
2.  Compile o código. Para compilar o código no prompt de comando, use:  
  
    ```  
    csc /reference:Microsoft.Data.SqlXML.dll DocSample.cs  
    ```  
  
     Isso cria um executável (DocSample.exe).  
  
3.  No prompt de comando, execute DocSample.exe.  
  
 Para testar este exemplo, é necessário ter o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework instalado no computador.  
  
 Em vez de especificar consultas SQL como o texto de comando, você pode especificar um modelo (conforme mostrado no fragmento de código a seguir) que executa um diagrama de atualização (que também é um modelo) para inserir um registro de cliente. Você pode especificar modelos e diagramas de atualização em arquivos e também executar arquivos. Para obter mais informações, consulte [executando arquivos de modelo usando a propriedade CommandText](executing-template-files-by-using-the-commandtext-property.md).  
  
```  
SqlXmlCommand cmd = new SqlXmlCommand("Provider=SQLOLEDB;Data Source=SqlServerName;Initial Catalog=Database; Integrated Security=SSPI;");  
Stream stm;  
cmd.CommandType = SqlXmlCommandType.UpdateGram;  
cmd.CommandText = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql' xmlns:updg='urn:schemas-microsoft-com:xml-updategram'>" +  
      "<updg:sync>" +  
       "<updg:before/>" +  
       "<updg:after>" +  
         "<Customer CustomerID='aaaaa' CustomerName='Some Name' CustomerTitle='SomeTitle' />" +  
       "</updg:after>" +  
       "</updg:sync>" +  
       "</ROOT>";  
  
stm = cmd.ExecuteStream();  
stm = null;  
cmd = null;  
```  
  
## <a name="using-executetostream"></a>Usando ExecuteToStream  
 Se você tiver um fluxo existente, poderá usar o método ExecuteToStream em vez de criar um objeto de fluxo e usar o método execute. O código do exemplo anterior é revisado aqui para usar o método ExecuteToStream:  
  
```  
using System;  
using Microsoft.Data.SqlXml;  
using System.IO;  
class Test  
{  
   static string ConnString = "Provider=SQLOLEDB;Server=SqlServerName;database=AdventureWorks;Integrated Security=SSPI;";  
   public static int testParams()  
   {  
      SqlXmlParameter p;  
      MemoryStream ms = new MemoryStream();  
      StreamReader sr = new StreamReader(ms);  
      ms.Position = 0;  
      SqlXmlCommand cmd = new SqlXmlCommand(ConnString);  
      cmd.CommandText = "select FirstName, LastName from Person.Contact where LastName = ? For XML Auto";  
      p = cmd.CreateParameter();  
      p.Value = "Achong";  
      cmd.ExecuteToStream(ms);  
      ms.Position = 0;  
      Console.WriteLine(sr.ReadToEnd());  
      return 0;        
   }  
   public static int Main(String[] args)  
   {  
      testParams();     
      return 0;  
   }  
}  
```  
  
> [!NOTE]  
>  Você também pode usar o ExecuteXMLReadermethod que retorna um objeto XmlReader. Para obter mais informações, consulte [executando consultas SQL usando o método ExecuteXMLReader](executing-sql-queries-by-using-the-executexmlreader-method.md).  
  
  
