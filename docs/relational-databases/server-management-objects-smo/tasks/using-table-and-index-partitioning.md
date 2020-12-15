---
description: Usando o particionamento de tabela e índice
title: Usando o particionamento de tabela e índice | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- partitions [SMO]
- storing data [SMO]
- partitioned tables [SQL Server], SMO
- partitioned indexes [SQL Server], SMO
ms.assetid: 0e682d7e-86c3-4d73-950d-aa692d46cb62
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8d44f6907e523a1627e42360f7afb7260e352ade
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480827"
---
# <a name="using-table-and-index-partitioning"></a>Usando o particionamento de tabela e índice
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  É possível armazenar dados usando os algoritmos de armazenamento fornecidos por [Partitioned Tables and Indexes](../../../relational-databases/partitions/partitioned-tables-and-indexes.md). O particionamento pode tornar as tabelas e os índices grandes mais gerenciáveis e escalonáveis.  
  
## <a name="index-and-table-partitioning"></a>Particionamento de tabela e índice  
 O recurso permite a difusão de dados de tabela e índice por vários grupos de arquivos em partições. Uma função de partição define como as linhas de uma tabela ou índice são mapeadas para um conjunto de partições, com base nos valores de certas colunas, chamadas de colunas de particionamento. Um esquema de partição mapeia cada partição especificada pela função de partição para um grupo de arquivos. Isso permite desenvolver estratégias de arquivamento que possibilitam o dimensionamento de tabelas em grupos de arquivos e, portanto, em dispositivos físicos.  
  
 O objeto <xref:Microsoft.SqlServer.Management.Smo.Database> contém uma coleção de objetos <xref:Microsoft.SqlServer.Management.Smo.PartitionFunction> que representam as funções de partição implementadas e uma coleção de objetos <xref:Microsoft.SqlServer.Management.Smo.PartitionScheme> que descrevem como dados são mapeados para grupos de arquivos.  
  
 Cada objeto <xref:Microsoft.SqlServer.Management.Smo.Table> e <xref:Microsoft.SqlServer.Management.Smo.Index> especifica o esquema de partição usado na propriedade <xref:Microsoft.SqlServer.Management.Smo.PartitionScheme> e especifica as colunas no <xref:Microsoft.SqlServer.Management.Smo.PartitionSchemeParameterCollection>.  
  
## <a name="example"></a>Exemplo  
 Para os exemplos de código a seguir, selecione o ambiente de programação, o modelo de programação e a linguagem de programação para criar seu aplicativo. Para obter mais informações, consulte [criar um projeto do Visual C&#35; Smo no Visual Studio .net](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md).  
  
## <a name="setting-up-a-partition-scheme-for-a-table-in-visual-c"></a>Configurando um esquema de partição para uma tabela no Visual C#  
 O exemplo de código mostra como criar uma função de partição e um esquema de partição para a tabela `TransactionHistory` no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . As partições são divididas por data com a intenção de separar registros antigos na tabela `TransactionHistoryArchive` .  
  
```csharp  
{   
//Connect to the local, default instance of SQL Server.   
Server srv;   
srv = new Server();   
//Reference the AdventureWorks2012 database.   
Database db;   
db = srv.Databases("AdventureWorks2012");   
//Define and create three new file groups on the database.   
FileGroup fg2;   
fg2 = new FileGroup(db, "Second");   
fg2.Create();   
FileGroup fg3;   
fg3 = new FileGroup(db, "Third");   
fg3.Create();   
FileGroup fg4;   
fg4 = new FileGroup(db, "Fourth");   
fg4.Create();   
//Define a partition function by supplying the parent database and name arguments in the constructor.   
PartitionFunction pf;   
pf = new PartitionFunction(db, "TransHistPF");   
//Add a partition function parameter that specifies the function uses a DateTime range type.   
PartitionFunctionParameter pfp;   
pfp = new PartitionFunctionParameter(pf, DataType.DateTime);   
pf.PartitionFunctionParameters.Add(pfp);   
//Specify the three dates that divide the data into four partitions.   
object[] val;   
val = new object[] {"1/1/2003", "1/1/2004", "1/1/2005"};   
pf.RangeValues = val;   
//Create the partition function.   
pf.Create();   
//Define a partition scheme by supplying the parent database and name arguments in the constructor.   
PartitionScheme ps;   
ps = new PartitionScheme(db, "TransHistPS");   
//Specify the partition function and the filegroups required by the partition scheme.   
ps.PartitionFunction = "TransHistPF";   
ps.FileGroups.Add("PRIMARY");   
ps.FileGroups.Add("second");   
ps.FileGroups.Add("Third");   
ps.FileGroups.Add("Fourth");   
//Create the partition scheme.   
ps.Create();   
}   
```  
  
## <a name="setting-up-a-partition-scheme-for-a-table-in-powershell"></a>Configurando um esquema de partição para uma tabela no PowerShell  
 O exemplo de código mostra como criar uma função de partição e um esquema de partição para a tabela `TransactionHistory` no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)] . As partições são divididas por data com a intenção de separar registros antigos na tabela `TransactionHistoryArchive` .  
  
```powershell  
# Set the path context to the local, default instance of SQL Server.  
CD \sql\localhost\default  
  
#Get a server object which corresponds to the default instance  
$srv = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
$db = $srv.Databases["AdventureWorks"]  
#Create four filegroups  
$fg1 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "First"  
$fg2 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Second"  
$fg3 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Third"  
$fg4 = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Filegroup -argumentlist $db, "Fourth"  
  
#Define a partition function by supplying the parent database and name arguments in the constructor.  
$pf =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionFunction -argumentlist $db, "TransHistPF"  
$T = [Microsoft.SqlServer.Management.SMO.DataType]::DateTime  
$T  
$T.GetType()  
#Add a partition function parameter that specifies the function uses a DateTime range type.  
$pfp =  New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionFunctionParameter -argumentlist $pf, $T  
  
#Specify the three dates that divide the data into four partitions.   
#Create an array of type object to hold the partition data  
$val = "1/1/2003"."1/1/2004","1/1/2005"  
$pf.RangeValues = $val  
$pf  
#Create the partition function  
$pf.Create()  
  
#Create partition scheme  
$ps = New-Object -TypeName Microsoft.SqlServer.Management.SMO.PartitionScheme -argumentlist $db, "TransHistPS"  
$ps.PartitionFunction = "TransHistPF"  
  
#add the filegroups to the scheme   
$ps.FileGroups.Add("PRIMARY")  
$ps.FileGroups.Add("Second")  
$ps.FileGroups.Add("Third")  
$ps.FileGroups.Add("Fourth")  
  
#Create it at the server  
$ps.Create()  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas e índices particionados](../../../relational-databases/partitions/partitioned-tables-and-indexes.md)  
  
  
