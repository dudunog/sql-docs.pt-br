---
title: Fazer backup e restauração de bancos de dados do SQL Server | Microsoft Docs
description: Este artigo descreve os benefícios de fazer backup dos bancos de dados do SQL Server e apresenta estratégias de backup e restauração e considerações de segurança.
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], see restoring [SQL Server]
- backups [SQL Server]
- restoring databases [SQL Server]
- backup [SQL Server], see backing up [SQL Server]
- databases [SQL Server], restoring
- backing up databases [SQL Server]
- restore [SQL Server], see restoring [SQL Server]
- disaster recovery [SQL Server], see backing up [SQL Server]
- backing up [SQL Server]
- Database Engine [SQL Server], backups
- databases [SQL Server], backups
ms.assetid: 570a21b3-ad29-44a9-aa70-deb2fbd34f27
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: bea2f639677de4869b537d3fb6cfbd1faa271134
ms.sourcegitcommit: 9afb612c5303d24b514cb8dba941d05c88f0ca90
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/28/2020
ms.locfileid: "82220631"
---
# <a name="back-up-and-restore-of-sql-server-databases"></a>Fazer backup e restaurar bancos de dados do SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este artigo descreve os benefícios do backup dos bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados, as condições de backup e restauração básicas, apresenta estratégias de backup e restauração para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e considerações de segurança sobre backup e restauração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 

> Este artigo apresenta os backups do SQL Server. Para obter etapas específicas para fazer backup de bancos de dados do SQL Server, confira [Criar backups](#creating-backups).
  
 O componente de backup e restauração do SQL Server oferece uma proteção essencial para dados críticos armazenados em bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para minimizar o risco de perda de dados catastrófica, você precisa fazer backup de seus bancos de dados para preservar as modificações nos seus dados regularmente. Uma estratégia de backup e restauração bem planejada ajuda a proteger os bancos de dados contra perda de dados causada por uma variedade de falhas. Teste sua estratégia restaurando um conjunto de backups e, em seguida, recuperando seu banco de dados para se preparar para responder com eficiência a um desastre.
  
 Além do armazenamento local para guardar os backups, o SQL Server também oferece suporte ao backup e à restauração no serviço de Armazenamento de Blobs do Azure. Para obter mais informações, consulte [Backup e restauração do SQL Server com o serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md). Para os arquivos de banco de dados armazenados usando o serviço de armazenamento de Blob do Microsoft Azure, o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] fornece a opção de usar instantâneos do Azure para backups quase imediatos e restaurações mais rápidas. Para obter mais informações, consulte [Backups de instantâneo de arquivo para arquivos de banco de dados no Azure](../../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md). O Azure também fornece uma solução de backup de classe empresarial para SQL Server em execução em VMs do Azure. Uma solução de backup totalmente gerenciada, compatível com grupos de disponibilidade Always On, retenção de longo prazo, recuperação pontual e gerenciamento e monitoramento central. Para obter mais informações, confira [Backup do Azure para o SQL Server em VM do Azure](https://docs.microsoft.com/azure/backup/backup-azure-sql-database).
  
##  <a name="why-back-up"></a>Por que fazer backup?  
-   O backup dos bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a execução de procedimentos de restauração de teste nos backups e o armazenamento de cópias de backups em um local externo seguro evita a perda de dados potencialmente catastrófica. **Realizar backup é a única maneira de proteger seus dados.**

     Com backups válidos de um banco de dados, você pode recuperar seus dados de muitas falhas, como:  
  
    -   Falha de mídia.    
    -   Por exemplo, erros de usuário, que removem uma tabela por engano.    
    -   Por exemplo, problemas de hardware, uma unidade de disco danificada ou perda permanente de um servidor.    
    -   Desastres naturais. Ao usar o Backup do SQL Server para serviço de Armazenamento de Blobs do Azure, é possível criar um backup externo em uma região diferente daquela do seu local, para usar caso um desastre natural afete seu local.  
  
-   Além disso, os backups de um banco de dados são úteis para fins administrativos rotineiros, como copiar um banco de dados de um servidor para outro, configurar o espelhamento do banco de dados ou [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] e fazer arquivamento.  
  
##  <a name="glossary-of-backup-terms"></a>Glossário de termos de backup
 **fazer backup** [verbo]  
 O processo de criação de um **backup [substantivo]** copiando registros de dados de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados ou registros de log do seu log de transações.  
  
 **backup** [substantivo]  
 Uma cópia dos dados que podem ser usados para restaurar e recuperar os dados após uma falha. Os backups de um banco de dados também podem ser usados para restaurar uma cópia do banco de dados em um novo local.  
  
dispositivo de**backup**  
 Um disco ou dispositivo de fita no qual os backups do SQL Server serão gravados e nos quais eles poderão ser restaurados. Os backups do SQL Server também podem ser gravados em um serviço de Armazenamento de Blobs do Azure. O formato de **URL** é usado para especificar o destino e o nome do arquivo de backup. Para obter mais informações, consulte [Backup e restauração do SQL Server com o serviço de Armazenamento de Blobs do Microsoft Azure](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
**mídia de backup**  
 Uma ou mais fitas ou arquivos de disco nos quais um ou mais backups foram gravados.  
  
**backup de dados**  
 Um backup de dados em um banco de dados completo (um backup de banco de dados), um banco de dados parcial (um backup parcial) ou um conjunto de arquivos de dados ou grupos de arquivos (um backup de arquivo).  
  
**backup de banco de dados**  
 Um backup de um banco de dados. Os backups completos de banco de dados representam todo o banco de dados no momento em que o backup é concluído. Os backups de banco de dados diferenciais contêm somente alterações feitas no banco de dados desde seu backup completo de banco de dados mais recente.  
  
**backup diferencial**  
 Um backup de dados que se baseia no backup completo mais recente de um banco de dados completo ou parcial ou um conjunto de arquivos de dados ou grupos de arquivos (a base diferencial) que contém somente os dados alterados desde essa base.  
  
**backup completo**  
 Um backup de dados que contém todos os dados em um banco de dados ou em um conjunto de grupos de arquivos ou arquivos, além de log suficiente para permitir a recuperação desses dados.  
  
**backup de log**  
 Um backup de logs de transações que inclui todos os registros de log dos quais não foi feito backup em um backup de log anterior. (modelo de recuperação completa)  
  
**recover**  
 Para retornar um banco de dados a um estado estável e consistente.  
  
**recuperação**  
 Uma fase de inicialização de banco de dados ou de restauração com recuperação que coloca o banco de dados em um estado de transação consistente.  
  
**modelo de recuperação**  
 Uma propriedade de banco de dados que controla a manutenção do log de transações em um banco de dados. Existem três modelos de recuperação: simples, completo e bulk-logged. O modelo de recuperação de banco de dados determina seus requisitos de backup e de restauração.  
  
**restaurar**  
 Um processo multifase que copia todos os dados e páginas de log de um backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um banco de dados especificado e, em seguida, efetua roll forward de todas as transações registradas no backup, aplicando as alterações registradas para avançar os dados no tempo.  
  
 ##  <a name="backup-and-restore-strategies"></a>Estratégias de backup e restauração  
 O backup e a restauração dos dados devem ser personalizados em um ambiente específico e devem funcionar com os recursos disponíveis. Portanto, um uso confiável de backup e restauração para recuperação requer uma estratégia de backup e restauração. Uma estratégia de backup e restauração bem projetada equilibra os requisitos de negócios para máxima disponibilidade de dados e mínima perda de dados, levando em consideração o custo de manutenção e armazenamento de backups.  

 Uma estratégia de backup e restauração contém uma parte de backup e uma parte de restauração. A parte de backup da estratégia define o tipo e a frequência dos backups, a natureza e velocidade do hardware exigido para eles, como os backups serão testados e em que local e como a mídia de backup deve ser armazenada (incluindo considerações de segurança). A parte de restauração da estratégia define quem é responsável por realizar restaurações, como as restaurações devem ser executadas para atender às suas metas de disponibilidade de banco de dados e minimizar a perda de dados e como as restaurações são testadas. 
  
 O design de uma estratégia de backup e restauração eficaz requer planejamento, implementação e teste cuidadosos. Testar é necessário: você não tem uma estratégia de backup até que tenha restaurado com êxito os backups em todas as combinações incluídas na sua estratégia de restauração e tenha testado a consistência física do banco de dados restaurado. Você deve considerar uma variedade de fatores. Eles incluem:  
  
- As metas de sua organização para os bancos de dados de produção, especialmente os requisitos para disponibilidade e proteção contra perda ou danificação de dados.  
  
-  A natureza de cada banco de dados: o tamanho, os padrões de uso, a natureza de seu conteúdo, os requisitos dos dados e assim por diante.  
  
-   Restrições de recursos, como hardware, pessoal, espaço para armazenagem de mídia de backup, a segurança física da mídia armazenada, e assim por diante.  

## <a name="best-practice-recommendations"></a>Recomendações de melhores práticas

### <a name="use-separate-storage"></a>Usar armazenamento separado 
> [!IMPORTANT] 
> Coloque os backups de banco de dados em um local físico ou dispositivo separado dos arquivos de banco de dados. Quando a unidade física que armazena seus bancos de dados falha ou apresenta um problema de funcionamento, a recuperação depende da capacidade de acessar a unidade separada ou o dispositivo remoto que armazenou os backups para executar uma restauração. Saiba que você pode criar vários volumes lógicos ou partições de uma mesma unidade de disco físico. Analise atentamente os layouts de partição de disco e volume lógico antes de escolher um local de armazenamento para os backups.

### <a name="choose-appropriate-recovery-model"></a>Escolher o modelo de recuperação apropriado
 As operações de backup e restauração ocorrem dentro do contexto de um [modelo de recuperação](../backup-restore/recovery-models-sql-server.md). Um modelo de recuperação é uma propriedade de banco de dados que controla a forma de gerenciamento do log de transações. Assim, o modelo de recuperação de um banco de dados determina quais tipos de backup e cenários de restauração são compatíveis com o banco de dados e qual será o tamanho dos backups de log de transações. Em geral, um banco de dados usa o modelo de recuperação simples ou o modelo de recuperação completa. O modelo de recuperação completa pode ser aumentado alternando para o modelo de recuperação bulk-logged antes das operações em massa. Para obter uma introdução a esses modelos de recuperação e como eles afetam o gerenciamento do log de transações, consulte [O log de transação (SQL Server)](../logs/the-transaction-log-sql-server.md)  
  
 A melhor escolha do modelo de recuperação para o banco de dados depende de seus requisitos empresariais. Para evitar gerenciamento de log de transações e simplificar o backup e a restauração, use o modelo de recuperação simples. Para minimizar exposição à perda de trabalho, às custas de uma sobrecarga administrativa, use o modelo de recuperação completa. Para minimizar o impacto sobre o tamanho do log durante operações bulk-logged e, ao mesmo tempo, permitir a recuperação dessas operações, use o modelo de recuperação bulk-logged. Para obter informações sobre o efeito dos modelos de recuperação sobre o backup e a restauração, consulte [Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
### <a name="design-your-backup-strategy"></a>Planejar a estratégia de backup  
 Depois de selecionar um modelo de recuperação que satisfaça seus requisitos empresariais para um banco de dados específico, você precisa planejar e implementar uma estratégia de backup correspondente. A melhor estratégia de backup depende de uma série de fatores, dos quais os seguintes são especialmente significativos:  
  
-   Quantas horas ao dia os aplicativos precisam acessar o banco de dados?  
  
     Se houver um período de pouca atividade previsível, recomendamos que você agende backups de banco de dados completos para aquele período.  
  
-   Com que frequência as alterações e atualizações deverão ocorrer?  
  
     Se as alterações forem frequentes, considere o seguinte:  
  
    -   No modelo de recuperação simples, agende backups diferenciais entre os backups de banco de dados completos. Um backup diferencial captura só as alterações desde o último backup completo do banco de dados.  
  
    -   No modelo de recuperação completa, você deve agendar backups de log frequentes. O agendamento de backups diferenciais entre backups completos pode reduzir o tempo de restauração reduzindo o número de backups de log a serem restaurados após a restauração dos dados.  
  
-   As alterações ocorrem geralmente em uma pequena parte do banco de dados ou em uma grande parte do banco de dados?  
  
     Para um banco de dados grande no qual mudanças estão concentradas em uma parte dos arquivos ou grupos de arquivos, backups parciais e backups de arquivo podem ser úteis. Para obter mais informações, consulte [Backups parciais &#40;SQL Server&#41;](../../relational-databases/backup-restore/partial-backups-sql-server.md) e [Backups completos de arquivo &#40;SQL Server&#41;](../../relational-databases/backup-restore/full-file-backups-sql-server.md).  
  
-   Quanto espaço em disco é necessário para um backup completo de banco de dados?  
-   Há quanto tempo sua empresa exige a manutenção de backups? 

    Verifique se você tem uma agenda de backup adequado estabelecida de acordo com as necessidades dos aplicativos e dos requisitos de negócios. Conforme os backups envelhecem, o risco de perda de dados é maior, a menos que você tenha uma maneira de regenerar todos os dados até o ponto de falha. Antes de optar por descartar os backups antigos devido a limitações de recursos de armazenamento, considere se é necessária uma capacidade de recuperação distante no passado

  
 ### <a name="estimate-the-size-of-a-full-database-backup"></a>Estimar o tamanho de um backup de banco de dados completo  
 Antes de implementar uma estratégia de backup e restauração, calcule quanto espaço em disco um backup de banco de dados completo usará. A operação de backup copia os dados no banco de dados para o arquivo de backup. O backup contém só os dados reais no banco de dados e não qualquer espaço não utilizado. Portanto, o backup é geralmente menor do que o próprio banco de dados. Você pode estimar o tamanho de um backup de banco de dados completo usando o procedimento armazenado do sistema **sp_spaceused** . Para obter mais informações, veja [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md).  
  
### <a name="schedule-backups"></a>Agendar backups  
 A execução do backup tem um efeito mínimo sobre as transações em andamento; portanto, as operações de backup podem ser realizadas durante a operação regular. Você pode executar um backup do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com um efeito mínimo sobre as cargas de trabalho de produção.  
   
>  Para obter informações sobre restrições de simultaneidade durante o backup, consulte [Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md).  
  
 Depois de decidir os tipos de backups necessários e a frequência de execução de cada tipo, recomendamos que você agende backups regulares como parte de um plano de manutenção de banco de dados para o banco de dados. Para obter informações sobre planos de manutenção e como criá-los para fazer backups de banco de dados e backups de log, consulte [Use the Maintenance Plan Wizard](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md).
  
### <a name="test-your-backups"></a>Teste seus backups.  
 Não existirá uma estratégia de restauração até que você tenha testado seus backups. É muito importante testar sua estratégia de backup completamente para cada um dos bancos de dados, restaurando uma cópia do banco de dados em um sistema de teste. É necessário testar a restauração de cada tipo de backup que você pretende usar. Também é recomendável que, depois de restaurar o backup, você execute verificações de consistência do banco de dados usando DBCC CHECKDB do banco de dados para validar se a mídia de backup não foi danificada. 

### <a name="verify-media-stability-and-consistency"></a>Verificar a estabilidade e a consistência da mídia
Use as opções de verificação fornecidas pelos utilitários de backup (comando T-SQL de BACKUP, Planos de Manutenção do SQL Server, seu software ou solução de backup etc). Para um exemplo, confira [RESTORE VERIFYONLY] (../t-sql/statements/restore-statements-verifyonly-transact-sql.md) Use recursos avançados como BACKUP CHECKSUM para detectar problemas com a mídia de backup em si. Para obter mais informações, confira os [Possíveis erros de mídia durante o backup e a restauração (SQL Server)](../backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)

### <a name="document-backuprestore-strategy"></a>Documentar estratégia de backup/restauração 
Recomendamos que você documente seus procedimentos de backup e restauração e mantenha uma cópia da documentação em seu livro de execuções.
Recomendamos também que você mantenha um manual de operações para cada banco de dados. Esse manual operacional deve documentar o local dos backups, os nomes do dispositivo de backup (se houver) e o tempo necessário para restaurar os backups de teste.



## <a name="monitor-progress-with-xevent"></a>Monitorar o progresso com xEvent
Operações de backup e restauração podem levar um tempo considerável devido ao tamanho de um banco de dados e à complexidade das operações envolvidas. Quando ocorrem problemas com a operação, você pode usar o evento estendido **backup_restore_progress_trace** para monitorar o progresso em tempo real. Para obter mais informações sobre eventos estendidos, veja [eventos estendidos](../extended-events/extended-events.md).

  >[!WARNING]
  > Usar o evento estendido backup_restore_progress_trace pode causar um problema de desempenho e consumir uma quantidade significativa de espaço em disco. Use por curtos períodos de tempo, tenha cuidado e teste bem antes de implementar na produção.


```sql
-- Create the backup_restore_progress_trace extended event esssion
CREATE EVENT SESSION [BackupRestoreTrace] ON SERVER 
ADD EVENT sqlserver.backup_restore_progress_trace
ADD TARGET package0.event_file(SET filename=N'BackupRestoreTrace')
WITH (MAX_MEMORY=4096 KB,EVENT_RETENTION_MODE=ALLOW_SINGLE_EVENT_LOSS,MAX_DISPATCH_LATENCY=5 SECONDS,MAX_EVENT_SIZE=0 KB,MEMORY_PARTITION_MODE=NONE,TRACK_CAUSALITY=OFF,STARTUP_STATE=OFF)
GO

-- Start the event session  
ALTER EVENT SESSION [BackupRestoreTrace]  
ON SERVER  
STATE = start;  
GO  

-- Stop the event session  
ALTER EVENT SESSION [BackupRestoreTrace]  
ON SERVER  
STATE = stop;  
GO  
```

### <a name="sample-output-from-extended-event"></a>Exemplo de saída do evento estendido 

![Exemplo de saída xevent de backup](media/back-up-and-restore-of-sql-server-databases/backup-xevent-example.png)
![Exemplo de saída xevent de restauração](media/back-up-and-restore-of-sql-server-databases/restore-xevent-example.png)
 
  
## <a name="more-about-backup-tasks"></a>Mais informações sobre tarefas de backup  
-   [Criar um Plano de Manutenção](../../relational-databases/maintenance-plans/create-a-maintenance-plan.md)  
  
-   [Criar um trabalho](../../ssms/agent/create-a-job.md)  
  
-   [Agendar um trabalho](../../ssms/agent/schedule-a-job.md)  
  
## <a name="working-with-backup-devices-and-backup-media"></a>Trabalhando com dispositivos e mídias de backup  
-   [Definir um dispositivo de backup lógico para um arquivo de disco &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [Definir um dispositivo de backup lógico para uma unidade de fita &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [Especificar um disco ou fita como destino de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [Excluir um dispositivo de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/delete-a-backup-device-sql-server.md)  
  
-   [Definir a data de validade em um backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [Exibir o conteúdo de um arquivo ou fita de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [Exibir os dados e arquivos de log em um conjunto de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [Exibir as propriedades e o conteúdo de um dispositivo de backup lógico &#40;SQL Server&#41;](../../relational-databases/backup-restore/view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [Restaurar um backup de um dispositivo &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-backup-from-a-device-sql-server.md)  
  
## <a name="creating-backups"></a>Criando backups  
**Observação!** Para backups parciais ou somente cópia, use a instrução [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](../../t-sql/statements/backup-transact-sql.md) com a opção PARTIAL ou COPY_ONLY, respectivamente.  
  
 ### <a name="using-ssms"></a>Usando SSMS   
-   [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [Fazer backup de um log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)  
  
-   [Fazer backup de arquivos e de grupos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-files-and-filegroups-sql-server.md)  
  
-   [Criar um backup diferencial de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
 ### <a name="using-t-sql"></a>Usando o T-SQL  
-   [Usar o Resource Governor para limitar o uso de CPU por meio de compactação de backup &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [Fazer backup do log de transações quando o banco de dados está danificado &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
-   [Habilitar ou desabilitar as somas de verificação de backup durante backup ou restauração &#40;SQL Server&#41;](../../relational-databases/backup-restore/enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
-   [Especificar se uma operação de backup ou restauração continua ou é interrompida após um erro &#40;SQL Server&#41;](../../relational-databases/backup-restore/specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  
## <a name="restore-data-backups"></a>Restaurar backups de dados 
### <a name="using-ssms"></a>Usando SSMS 
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [Restaurar um banco de dados em um novo local &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
  
-   [Restaurar um backup de banco de dados diferencial &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-differential-database-backup-sql-server.md)  
  
-   [Restaurar arquivos e grupos de arquivos &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-sql-server.md)  
  
### <a name="using-t-sql"></a>Usando o T-SQL
-   [Restaurar um backup de banco de dados no modelo de recuperação simples &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [Restaurar um banco de dados até o ponto de falha no modelo de recuperação completa &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [Restaurar arquivos e grupos de arquivos sobre arquivos existentes &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [Restaurar arquivos em um novo local &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [Restaurar o banco de dados mestre &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-the-master-database-transact-sql.md)  

## <a name="restore-transaction-logs-full-recovery-model"></a>Restaurar logs de transações (Modelo de Recuperação Completa)
### <a name="using-ssms"></a>Usando SSMS  
-   [Restaurar um banco de dados para uma transação marcada &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [Restaurar um backup de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)  
  
-   [Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
 ### <a name="using-t-sql"></a>Usando o T-SQL 
-   [Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](../../relational-databases/backup-restore/restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
 
-   [Reiniciar uma operação de restauração interrompida &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restart-an-interrupted-restore-operation-transact-sql.md)  
  
-   [Recuperar um banco de dados sem restaurar dados &#40;Transact-SQL&#41;](../../relational-databases/backup-restore/recover-a-database-without-restoring-data-transact-sql.md)  
 
## <a name="more-information-and-resources"></a>Mais informações e recursos
 [Visão geral do backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [Visão geral de restauração e recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-and-recovery-overview-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)   
 [Backup e restauração de bancos de dados do Analysis Services](https://docs.microsoft.com/analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases)   
 [Fazer backup e restaurar índices e catálogos de texto completo](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)   
 [Fazer backup e restaurar bancos de dados replicados](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
 [O log de transações &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Modelos de recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)   
 [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
