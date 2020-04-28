---
title: Usando sinônimos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- synonyms [SMO]
ms.assetid: db0a9022-9549-43e5-b6b3-deb236f05fb8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a96f6ee89b920ec668af21ce625694fc31ce13bd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "72781867"
---
# <a name="using-synonyms"></a>Usando sinônimos
  Um sinônimo é um nome alternativo de um objeto com escopo de esquema. No SMO, os sinônimos são representados pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Synonym>. O objeto <xref:Microsoft.SqlServer.Management.Smo.Synonym> é um filho do objeto <xref:Microsoft.SqlServer.Management.Smo.Database>. Isso significa que sinônimos só são válidos dentro do escopo do banco de dados no qual eles são definidos. Porém, o sinônimo pode se referir a objetos em outro banco de dados, ou em uma instância remota do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 O objeto que recebe um nome alternativo é conhecido como o objeto base. A propriedade do nome do objeto <xref:Microsoft.SqlServer.Management.Smo.Synonym> é o nome alternativo fornecido ao objeto base.  
  
## <a name="example"></a>Exemplo  
 Para o exemplo de código a seguir, selecione o ambiente de programação, o modelo de programação e a linguagem de programação para criar seu aplicativo. Para obter mais informações, consulte [criar um projeto Visual Basic Smo no Visual Studio .net](../../../database-engine/dev-guide/create-a-visual-basic-smo-project-in-visual-studio-net.md) e [criar um projeto do Visual C&#35; Smo no Visual Studio .net](../how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-a-synonym-in-visual-basic"></a>Criando um sinônimo no Visual Basic  
 O exemplo de código mostra como criar um sinônimo ou um nome alternativo para um objeto com escopo de esquema. Aplicativos cliente podem usar uma única referência para o objeto base através de um sinônimo, em vez de usar um nome com várias partes para fazer referência ao objeto base.  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VBSynonyms1](SMO How to#SMO_VBSynonyms1)]  -->  
  
## <a name="creating-a-synonym-in-visual-c"></a>Criando um sinônimo no Visual C#  
 O exemplo de código mostra como criar um sinônimo ou um nome alternativo para um objeto com escopo de esquema. Aplicativos cliente podem usar uma única referência para o objeto base através de um sinônimo, em vez de usar um nome com várias partes para fazer referência ao objeto base.  
  
```csharp
{  
            //Connect to the local, default instance of SQL Server.   
            Server srv = new Server();  
  
            //Reference the AdventureWorks2012 database.   
            Database db = srv.Databases["AdventureWorks2012"];  
  
            //Define a Synonym object variable by supplying the   
            //parent database, name, and schema arguments in the constructor.   
            //The name is also a synonym of the name of the base object.   
            Synonym syn = new Synonym(db, "Shop", "Sales");  
  
            //Specify the base object, which is the object on which   
            //the synonym is based.   
            syn.BaseDatabase = "AdventureWorks2012";  
            syn.BaseSchema = "Sales";  
            syn.BaseObject = "Store";  
            syn.BaseServer = srv.Name;  
  
            //Create the synonym on the instance of SQL Server.   
            syn.Create();  
        }  
```  
  
## <a name="creating-a-synonym-in-powershell"></a>Criando um sinônimo no PowerShell  
 O exemplo de código mostra como criar um sinônimo ou um nome alternativo para um objeto com escopo de esquema. Aplicativos cliente podem usar uma única referência para o objeto base através de um sinônimo, em vez de usar um nome com várias partes para fazer referência ao objeto base.  
  
```powershell
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#And the database object corresponding to Adventureworks  
$db = $srv.Databases["AdventureWorks2012"]  
  
$syn = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Synonym -ArgumentList $db, "Shop", "Sales"  
  
#Specify the base object, which is the object on which the synonym is based.  
$syn.BaseDatabase = "AdventureWorks2012"  
$syn.BaseSchema = "Sales"  
$syn.BaseObject = "Store"  
$syn.BaseServer = $srv.Name  
  
#Create the synonym on the instance of SQL Server.  
$syn.Create()  
```  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE SYNONYM &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-synonym-transact-sql)  
