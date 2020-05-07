---
title: 'Erros de mídia: Backup e restauração | Microsoft Docs'
description: No SQL Server 2019, você pode recuperar o banco de dados apesar dos erros detectados. Use RESTORE e RESTORE VERIFYONLY com uma soma de verificação de backup para verificar se há erros.
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- media errors [SQL Server]
- CONTINUE_AFTER_ERROR option
- errors [SQL Server], backups
- backups [SQL Server], errors
- RESTORE VERIFYONLY statement
- backup media [SQL Server], error management
- page checksums [SQL Server]
- backup checksums [SQL Server]
- backing up [SQL Server], media errors
- RESTORE statement, media errors
- NO_CHECKSUM option
- checksums [SQL Server]
ms.assetid: 83a27b29-1191-4f8d-9648-6e6be73a9b7c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 85b6077e5dfa2d70ecbbe6aead13fd02dbdf43b2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "82180145"
---
# <a name="possible-media-errors-during-backup-and-restore-sql-server"></a>Erros de mídia possíveis durante backup e restauração (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dá a você a opção de recuperar um banco de dados apesar dos erros detectados. Um novo mecanismo de detecção de erros importante é a criação opcional de uma soma de verificação do backup que pode ser criada por uma operação de backup e validada por uma operação de restauração. Você pode controlar se uma operação verifica os erros e se a operação é interrompida ou continua ao encontrar um erro. Se um backup contiver uma soma de verificação de backup, as instruções RESTORE e RESTORE VERIFYONLY poderão verificar os erros.  
  
> [!NOTE]  
>  Backups espelhados fornecem até quatro cópias (espelhos) de um conjunto de mídia, fornecendo cópias alternativas para a recuperação de erros causados por mídias danificadas. Para obter mais informações, veja [Conjuntos de mídias de backup espelhadas &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md).  
  
  
##  <a name="backup-checksums"></a><a name="BckChecksums"></a> Somas de verificação de backup  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a três tipos de somas de verificação: uma soma de verificação nas páginas, uma soma de verificação nos blocos de log e uma soma de verificação de backup. Ao gerar uma soma de verificação de backup, o BACKUP verifica se a leitura de dados do banco de dados é consistente com qualquer soma de verificação ou indicação da página interrompida que estejam presentes no banco de dados.  
  
 A instrução BACKUP computa opcionalmente uma soma de verificação de backup no fluxo de backup; se a soma de verificação de página ou as informações da página interrompida estiverem presentes em uma determinada página, ao fazer o backup da página, o BACKUP também verifica a soma de verificação, o estado da página interrompida e a ID da página, na página. Ao criar uma soma de verificação de backup, uma operação de backup não acrescenta nenhuma soma de verificação às páginas. O backup das páginas é feito enquanto as mesmas existirem no banco de dados, e as páginas não são alteradas pelo backup.  
  
 Devido a verificação de sobrecarga e a geração de soma de verificação de backup, usar somas de verificação de backup representa um possível impacto de desempenho. A carga de trabalho e a taxa de transferência de backup podem ser afetadas. Por isso, usar somas de verificação de backup é opcional. Ao decidir gerar somas de verificação durante um backup, monitore cuidadosamente a sobrecarga gerada da CPU, assim como o impacto em qualquer carga de trabalho simultânea no sistema.  
  
 O BACKUP nunca modifica a página de fonte em disco nem os conteúdos de uma página.  
  
 Quando as somas de verificação de backup estão habilitadas, uma operação de backup realiza as etapas seguintes:  
  
1.  Antes de gravar uma página na mídia de backup, a operação de backup verifica a informação do nível de página (soma de verificação de página ou detecção de página interrompida), ou se ela existe. Se não existir, o backup não poderá verificar a página. As páginas não verificadas são incluídas como estão, e seu conteúdo é adicionado à soma de verificação de backup geral.  
  
     Se a operação de backup encontrar um erro de página durante a verificação, o backup falhará.  
  
    > [!NOTE]  
    >  Para obter mais informações sobre somas de verificação de página e detecção de página interrompida, consulte a opção de PAGE_VERIFY da instrução ALTER DATABASE. Para obter mais informações, veja [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md).  
  
2.  Independentemente de somas de verificação de página estarem presentes, BACKUP gera uma soma de verificação de backup separada para os fluxos de backup. Operações de restauração podem usar opcionalmente a soma de verificação de backup para validar se o backup não está corrompido. A soma de verificação de backup é armazenada na mídia de backup, não nas páginas do banco de dados. A soma de verificação de backup pode ser usada opcionalmente na hora da restauração.  
  
3.  O conjunto de backup é sinalizado como contendo somas de verificação de backup (na coluna **has_backup_checksums** de **msdb..backupset)** . Para obter mais informações, veja [conjunto de backup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md).  

 Durante a operação de restauração, se as somas de verificação de backup estiverem presentes na mídia de backup, por padrão, ambas as instruções RESTORE e RESTORE VERIFYONLY verificarão as somas de verificação de backup e somas de verificação de página. Se não houver nenhuma soma de verificação de backup, cada operação de restauração prossegue sem qualquer verificação; porque sem uma soma de verificação de backup a restauração não pode verificar somas de verificação da página de modo confiável.  
  
## <a name="response-to-page-checksum-errors-during-a-backup-or-restore-operation"></a>Resposta para erros de soma de verificação de página durante uma operação de backup ou restauração  
 Por padrão, depois de encontrar um erro de soma de verificação de página, uma operação BACKUP ou RESTORE falha e uma operação RESTORE VERIFYONLY continua. No entanto, você pode controlar se uma determinada operação não consegue encontrar um erro ou continua da melhor maneira possível.  
  
 Se uma operação de BACKUP continuar depois de encontrar erros, ela executará as seguintes etapas:  
  
1.  Sinaliza o conjunto de backup na mídia de backup como contendo erros e localiza a página na tabela **suspect_pages** no banco de dados **msdb** . Para obter mais informações, veja [suspect_pages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md).  
  
2.  Faz o log do erro no log de erros do SQL Server.  
  
3.  Marca o conjunto de backup como contendo esse tipo de erro (na coluna **is_damaged** de **msdb.backupset)** . Para obter mais informações, veja [conjunto de backup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md).  
  
4.  Emite uma mensagem que o backup foi gerado com sucesso, mas contém erros de página.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
 **Para habilitar ou desabilitar as somas de verificação de backup**  
  
-   [Habilitar ou desabilitar as somas de verificação de backup durante backup ou restauração &#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
 **Para controlar a resposta a um erro durante uma operação de backup**  
  
-   [Especificar se uma operação de backup ou restauração continua ou é interrompida após um erro &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [conjunto de backup &#40;Transact-SQL&#41;](../../relational-databases/system-tables/backupset-transact-sql.md)   
 [Conjuntos de mídias de backup espelhadas &#40;SQL Server&#41;](../../relational-databases/backup-restore/mirrored-backup-media-sets-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [RESTORE VERIFYONLY &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-verifyonly-transact-sql.md)  
  
  
