---
title: Criando, alterando e removendo tabelas
ms.custom: seo-dt-2019
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- tables [SMO]
ms.assetid: ff0bcfff-812f-4999-b0c7-736a97804c2b
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b90e081c86aaee9fda1363185263fd6e53d4378f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74095634"
---
# <a name="creating-altering-and-removing-tables"></a>Criando, alterando e removendo tabelas
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]
  No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO), as tabelas são representadas pelo objeto <xref:Microsoft.SqlServer.Management.Smo.Table>. Na hierarquia de objetos do SMO, o objeto <xref:Microsoft.SqlServer.Management.Smo.Table> está abaixo do objeto <xref:Microsoft.SqlServer.Management.Smo.Database>.  
  
## <a name="example"></a>Exemplo  
 Para usar qualquer exemplo de código fornecido, será necessário escolher o ambiente de programação, o modelo e a linguagem para criar o seu aplicativo. Para obter mais informações, consulte [criar um projeto do Visual C&#35; Smo no Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="creating-altering-and-removing-a-table-in-visual-basic"></a>Criando, alterando e removendo uma tabela no Visual Basic  
 Esse exemplo de código cria uma tabela que tem várias colunas com tipos e objetivos diferentes. O código também fornece exemplos de como criar um campo de identidade, como criar uma chave primária e como alterar propriedades da tabela.  
  
```VBNET
'Connect to the local, default instance of SQL Server.
Dim srv As Server
srv = New Server
'Reference the AdventureWorks2012 2008R2 database.
Dim db As Database
db = srv.Databases("AdventureWorks2012")
'Define a Table object variable by supplying the parent database and table name in the constructor. 
Dim tb As Table
tb = New Table(db, "Test_Table")
'Add various columns to the table.
Dim col1 As Column
col1 = New Column(tb, "Name", DataType.NChar(50))
col1.Collation = "Latin1_General_CI_AS"
col1.Nullable = True
tb.Columns.Add(col1)
Dim col2 As Column
col2 = New Column(tb, "ID", DataType.Int)
col2.Identity = True
col2.IdentitySeed = 1
col2.IdentityIncrement = 1
tb.Columns.Add(col2)
Dim col3 As Column
col3 = New Column(tb, "Value", DataType.Real)
tb.Columns.Add(col3)
Dim col4 As Column
col4 = New Column(tb, "Date", DataType.DateTime)
col4.Nullable = False
tb.Columns.Add(col4)
'Create the table on the instance of SQL Server.
tb.Create()
'Add another column.
Dim col5 As Column
col5 = New Column(tb, "ExpiryDate", DataType.DateTime)
col5.Nullable = False
tb.Columns.Add(col5)
'Run the Alter method to make the change on the instance of SQL Server.
tb.Alter()
'Remove the table from the database.

tb.Drop()
``` 
  
## <a name="creating-altering-and-removing-a-table-in-visual-c"></a>Criando, alterando e removendo uma tabela no Visual C#  
 Esse exemplo de código cria uma tabela que tem várias colunas com tipos e objetivos diferentes. O código também fornece exemplos de como criar um campo de identidade, como criar uma chave primária e como alterar propriedades da tabela.  
  
```csharp  
{  
            //Connect to the local, default instance of SQL Server.   
        Server srv;   
        srv = new Server();   
        //Reference the AdventureWorks2012 database.   
        Database db;   
        db = srv.Databases["AdventureWorks2012"];   
        //Define a Table object variable by supplying the parent database and table name in the constructor.   
        Table tb;   
        tb = new Table(db, "Test_Table");   
        //Add various columns to the table.   
        Column col1;   
        col1 = new Column(tb, "Name", DataType.NChar(50));   
        col1.Collation = "Latin1_General_CI_AS";   
        col1.Nullable = true;   
        tb.Columns.Add(col1);   
        Column col2;   
        col2 = new Column(tb, "ID", DataType.Int);   
        col2.Identity = true;   
        col2.IdentitySeed = 1;   
        col2.IdentityIncrement = 1;   
        tb.Columns.Add(col2);   
        Column col3;   
        col3 = new Column(tb, "Value", DataType.Real);   
        tb.Columns.Add(col3);   
        Column col4;   
        col4 = new Column(tb, "Date", DataType.DateTime);   
        col4.Nullable = false;   
        tb.Columns.Add(col4);   
        //Create the table on the instance of SQL Server.   
        tb.Create();   
        //Add another column.   
        Column col5;   
        col5 = new Column(tb, "ExpiryDate", DataType.DateTime);   
        col5.Nullable = false;   
        tb.Columns.Add(col5);   
        //Run the Alter method to make the change on the instance of SQL Server.   
        tb.Alter();   
        //Remove the table from the database.   
        tb.Drop();   
        }  
```  
  
## <a name="creating-altering-and-removing-a-table-in-powershell"></a>Criando, alterando e removendo uma tabela no PowerShell  
 Esse exemplo de código cria uma tabela que tem várias colunas com tipos e objetivos diferentes. O código também fornece exemplos de como criar um campo de identidade, como criar uma chave primária e como alterar propriedades da tabela.  
  
```powershell  
#Load the assembly containing the objects used in this example  
[reflection.assembly]::LoadWithPartialName("Microsoft.SqlServer.Types")  
  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default\Databases\  
  
#And the database object corresponding to AdventureWorks2012.  
$db = get-item AdventureWorks2012  
  
#Create a SMO Table  
$tb = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Table -argumentlist $db, "Test_Table"  
  
#Add various columns to the table.   
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::NChar(50)  
$col1 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"Name", $Type  
$col1.Collation = "Latin1_General_CI_AS"  
$col1.Nullable = $true  
$tb.Columns.Add($col1)  
  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::Int  
$col2 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"ID", $Type  
$col2.Identity = $true  
$col2.IdentitySeed = 1  
$col2.IdentityIncrement = 1  
$tb.Columns.Add($col2)   
  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::Real  
$col3 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"Value", $Type  
$tb.Columns.Add($col3)   
  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$col4 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"Date", $Type  
$col4.Nullable = $false  
$tb.Columns.Add($col4)   
  
#Create the table  
$tb.Create()  
  
$Type = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$col5 =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.Column -argumentlist $tb,"ExpiryDate", $Type  
$col5.Nullable = $false  
$tb.Columns.Add($col5)   
  
#Run the Alter method to make the change on the instance of SQL Server.   
$tb.Alter()  
  
#Remove the table from the database.   
$tb.Drop()  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 <xref:Microsoft.SqlServer.Management.Smo.Table>  
  
  
