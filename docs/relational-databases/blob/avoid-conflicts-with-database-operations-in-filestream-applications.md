---
title: Evitar conflitos – operações de banco de dados FILESTREAM | Microsoft Docs
description: Os aplicativos que leem ou gravam dados de blob FILESTREAM podem encontrar erros de conflito com instruções Transact-SQL. Saiba como evitar esses tipos de conflitos.
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], Win32 and Transact-SQL Conflicts
ms.assetid: 8b1ee196-69af-4f9b-9bf5-63d8ac2bc39b
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 3641401fbb2314bf4712cc524777a490ced01541
ms.sourcegitcommit: 4b5919e3ae5e252f8d6422e8e6fddac1319075a1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/09/2020
ms.locfileid: "83000105"
---
# <a name="avoid-conflicts-with-database-operations-in-filestream-applications"></a>Evitar conflitos com operações de banco de dados em aplicativos de FILESTREAM
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Os aplicativos que usam SqlOpenFilestream() para abrir identificadores de arquivo do Win32 para ler ou gravar dados BLOB FILESTREAM podem apresentar erros de conflito com instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] gerenciadas em uma transação em comum. Isso inclui consultas [!INCLUDE[tsql](../../includes/tsql-md.md)] ou MARS cuja execução demora muito tempo para ser concluída. Os aplicativos devem ser criados cautelosamente para evitar esses tipos de conflitos.  
  
 Quando o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ou os aplicativos tentam abrir FILESTREAM BLOBs, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verifica o contexto de transação associado. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] permite ou nega as solicitações, dependendo se a operação em aberto funciona com instruções DDL e DML, transações de recuperação de dados ou de gerenciamento. A tabela a seguir mostra como o [!INCLUDE[ssDE](../../includes/ssde-md.md)] determina se uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] será permitida ou negada com base no tipo de arquivos abertos na transação.  
  
|instruções Transact-SQL|Abertas para leitura|Abertas para gravação|  
|------------------------------|---------------------|----------------------|  
|Instruções de DDL que funcionam com metadados de banco de dados, como CREATE TABLE, CREATE INDEX, DROP TABLE e ALTER TABLE.|Permitido|São bloqueadas e falham devido ao tempo limite esgotado.|  
|Instruções DML que funcionam com os dados armazenados no banco de dados, como UPDATE, DELETE e INSERT.|Permitido|Negadas|  
|SELECT|Permitido|Permitido|  
|COMMIT TRANSACTION|Negadas*|Negadas*.|  
|SAVE TRANSACTION|Negadas*|Negadas*|  
|ROLLBACK|Permitidas*|Permitidas*|  
  
 \* A transação é cancelada e os identificadores em aberto do contexto da transação são invalidados. O aplicativo deve fechar todos os identificadores abertos.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir mostram como as instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] e o acesso de FILESTREAM do Win32 podem causar conflitos.  
  
### <a name="a-opening-a-filestream-blob-for-write-access"></a>a. Abrindo um BLOB FILESTREAM para acesso de gravação  
 O exemplo a seguir mostra o efeito de abrir um arquivo para acesso apenas de gravação.  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Write, 0,  
    transactionToken, cbTransactionToken, 0);  
  
//Write some date to the FILESTREAM BLOB.  
WriteFile(dstHandle, updateData, ...);  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed. The FILESTREAM BLOB is  
//returned without the modifications that are made by  
//WriteFile(dstHandle, updateData, ...).  
CloseHandle(dstHandle);  
  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed. The FILESTREAM BLOB  
//is returned with the updateData applied.  
```  
  
### <a name="b-opening-a-filestream-blob-for-read-access"></a>B. Abrindo um BLOB FILESTREAM para acesso de leitura  
 O exemplo a seguir mostra o efeito de abrir um arquivo para acesso apenas de leitura.  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Read, 0,  
    transactionToken, cbTransactionToken, 0);  
//DDL statements will be denied.  
//DML statements will be allowed. Any changes that are  
//made to the FILESTREAM BLOB will not be returned until  
//the dstHandle is closed.  
//SELECT statements will be allowed.  
CloseHandle(dstHandle);  
  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
```  
  
### <a name="c-opening-and-closing-multiple-filestream-blob-files"></a>C. Abrindo e fechando vários arquivos de BLOB FILESTREAM  
 Se vários arquivos estiverem abertos, será usada a regra mais restritiva. O exemplo a seguir abre dois arquivos. O primeiro é aberto para leitura e o segundo, para gravação. As instruções DML serão negadas até que o segundo arquivo seja aberto.  
  
```  
dstHandle =  OpenSqlFilestream(dstFilePath, Read, 0,  
    transactionToken, cbTransactionToken, 0);  
//DDL statements will be denied.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
  
dstHandle1 =  OpenSqlFilestream(dstFilePath1, Write, 0,  
    transactionToken, cbTransactionToken, 0);  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed.  
  
//Close the read handle. The write handle is still open.  
CloseHandle(dstHandle);  
//DML statements are still denied because the write handle is open.  
  
//DDL statements will be denied.  
//DML statements will be denied.  
//SELECT statements will be allowed.  
  
CloseHandle(dstHandle1);  
//DDL statements will be allowed.  
//DML statements will be allowed.  
//SELECT statements will be allowed.  
```  
  
### <a name="d-failing-to-close-a-cursor"></a>D. Falha ao fechar um cursor  
 O exemplo a seguir mostra como um cursor de instrução que não está fechado pode impedir `OpenSqlFilestream()` de abrir o BLOB para acesso de gravação.  
  
```  
TCHAR *sqlDBQuery =  
TEXT("SELECT GET_FILESTREAM_TRANSACTION_CONTEXT(),")  
TEXT("Chart.PathName() FROM Archive.dbo.Records");  
  
//Execute a long-running Transact-SQL statement. Do not allow  
//the statement to complete before trying to  
//open the file.  
  
SQLExecDirect(hstmt, sqlDBQuery, SQL_NTS);  
  
//Before you call OpenSqlFilestream() any open files  
//that the Cursor the Transact-SQL statement is using  
// must be closed. In this example,  
//SQLCloseCursor(hstmt) is not called so that  
//the transaction will indicate that there is a file  
//open for reading. This will cause the call to  
//OpenSqlFilestream() to fail because the file is  
//still open.  
  
HANDLE srcHandle =  OpenSqlFilestream(srcFilePath,  
     Write, 0,  transactionToken,  cbTransactionToken,  0);  
  
//srcHandle will == INVALID_HANDLE_VALUE because the  
//cursor is still open.  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Acessar dados do FILESTREAM com OpenSqlFilestream](../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)   
 [Usando MARS &#40;Multiple Active Result Sets&#41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)  
  
  
