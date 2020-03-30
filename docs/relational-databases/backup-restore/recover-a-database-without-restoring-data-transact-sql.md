---
title: Recuperar banco de dados – sem restauração (Transact-SQL)
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- restoring [SQL Server], recovery-only
- recovery-only scenario [SQL Server]
- restoring databases [SQL Server], recovery-only
- recovery [SQL Server], recovery-only
- database recovery [SQL Server]
- database restores [SQL Server], recovery-only
- recovery [SQL Server], without restoring data
ms.assetid: 7e8fa620-315d-4e10-a718-23fa5171c09e
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 1d5c0fbb11b7ec3aaed4ac48a7334f790f3fd9b3
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75255851"
---
# <a name="recover-a-database-without-restoring-data-transact-sql"></a>Recuperar um banco de dados sem restaurar dados (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Normalmente, todos os dados em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são restaurados antes de o banco de dados ser recuperado. Porém, uma operação de restauração pode recuperar um banco de dados sem de fato restaurar um backup; por exemplo, ao recuperar um arquivo somente leitura que seja consistente com o banco de dados. Isso é chamado de uma *restauração somente recuperação*. Quando dados offline já são consistentes com o banco de dados e só precisam ser disponibilizados, uma operação de restauração somente recuperação conclui a recuperação do banco de dados e coloca os dados online.  
  
 Uma restauração somente recuperação pode ocorrer para um banco de dados inteiro ou para um ou mais arquivos ou grupos de arquivos.  
  
## <a name="recovery-only-database-restore"></a>Restauração de banco de dados somente recuperação  
 Uma restauração somente recuperação de banco de dados pode ser útil nas seguintes situações:  
  
-   Você não recuperou o banco de dados ao restaurar o último backup em uma sequência de restauração, e agora quer recuperar o banco de dados para colocá-lo online.  
  
-   O banco de dados está em modo de espera e você quer atualizá-lo sem aplicar outro backup de log.  
  
 A sintaxe [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) para a restauração de um banco de dados somente recuperação é a seguinte:  
  
 `RESTORE DATABASE *database_name* WITH RECOVERY`  
  
> [!NOTE]  
> A cláusula FFROM **=** \<*backup_device>* não é usada em restaurações somente recuperação porque nenhum backup é necessário.  
  
 **Exemplo**  
  
 O exemplo a seguir recupera o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] de amostra em uma operação de restauração sem restaurar dados.  
  
```sql  
-- Restore database using WITH RECOVERY.  
RESTORE DATABASE AdventureWorks2012  
   WITH RECOVERY  
```  
  
## <a name="recovery-only-file-restore"></a>Restauração de arquivo somente recuperação  
 Uma restauração somente recuperação pode ser útil na situação seguinte:  
  
 Um banco de dados é restaurado por etapas. Depois da conclusão da restauração do grupo de arquivos primário, um ou mais dos arquivos não restaurados estão consistentes com o novo estado do banco de dados, talvez porque tenham sido somente leitura por algum tempo. Esses arquivos só precisam ser recuperados; a cópia de dados é desnecessária.  
  
 Uma operação de restauração somente recuperação coloca os dados do grupo de arquivos offline online; nenhuma fase de cópia de dados, refazer ou desfazer acontece. Para obter informações sobre as fases de restauração, confira [Visão geral da restauração e recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md#TlogAndRecovery).  
  
 A sintaxe [RESTORE](../../t-sql/statements/restore-statements-transact-sql.md) para a restauração de um arquivo somente recuperação é:  
  
 `RESTORE DATABASE *database_name* { FILE **=**_logical_file_name_ | FILEGROUP **=**_logical_filegroup_name_ }[ **,**...*n* ] WITH RECOVERY`  
  
 **Exemplo**  
  
 O exemplo a seguir ilustra uma restauração de arquivos somente recuperação de um grupo de arquivos secundário, `SalesGroup2`, no banco de dados `Sales` . O grupo de arquivos primário já foi restaurado como a etapa inicial de uma restauração por etapas e `SalesGroup2` está consistente com o grupo de arquivos primário restaurado. Recuperar esse grupo de arquivos e colocá-lo online requer somente uma única instrução.  
  
```sql  
RESTORE DATABASE Sales FILEGROUP=SalesGroup2 WITH RECOVERY;  
```  
  
## <a name="examples-of-completing-a-piecemeal-restore-scenario-with-a-recovery-only-restore"></a>Exemplos de conclusão de um cenário de restauração por etapas com uma restauração somente recuperação  
 **Modelo de recuperação simples**  
  
-   [Exemplo: restauração por etapas de banco de dados &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-simple-recovery-model.md)  
  
-   [Exemplo: restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-simple-recovery-model.md)  
  
 **Modelo de recuperação completa**  
  
-   [Exemplo: restauração por etapas de banco de dados &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-database-full-recovery-model.md)  
  
-   [Exemplo: restauração por etapas de apenas alguns grupos de arquivos &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/example-piecemeal-restore-of-only-some-filegroups-full-recovery-model.md)  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.SqlRestore%2A>  
  
## <a name="see-also"></a>Consulte Também  
 [Restauração online &#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)   
 [Restaurações por etapas &#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)   
 [Restaurações de arquivos &#40;Modelo de recuperação simples&#41;](../../relational-databases/backup-restore/file-restores-simple-recovery-model.md)   
 [Restaurações de arquivo &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/file-restores-full-recovery-model.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
 [Visão geral da restauração e recuperação (SQL Server)](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md) 
  
