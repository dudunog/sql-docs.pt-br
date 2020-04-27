---
title: Change Data Capture and Other SQL Server Features | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- change data capture [SQL Server], other SQL Server features and
ms.assetid: 7dfcb362-1904-4578-8274-da16681a960e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 87fcd7656ff1e86522e4ea398fc49d91acde9a34
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62672070"
---
# <a name="change-data-capture-and-other-sql-server-features"></a>Change Data Capture e outros recursos do SQL Server
  Este tópico descreve como os seguintes recursos interagem com a captura de dados de alteração:  
  
-   [Controle de alterações](#ChangeTracking)  
  
-   [Espelhamento de banco de dados](#DatabaseMirroring)  
  
-   [Replicação transacional](#TransReplication)  
  
-   [Restaurando ou anexando um banco de dados habilitado para captura de dados de alteração](#RestoreOrAttach)  
  
##  <a name="change-tracking"></a><a name="ChangeTracking"></a>Controle de Alterações  
 A captura de dados de alteração e o [controle de alterações](about-change-tracking-sql-server.md) podem ser habilitados no mesmo banco de dados. Nenhuma consideração especial é necessária. Para obter mais informações, veja [Trabalhar com o controle de alterações &#40;SQL Server&#41;](work-with-change-tracking-sql-server.md).  
  
##  <a name="database-mirroring"></a><a name="DatabaseMirroring"></a>Espelhamento de banco de dados  
 Um banco de dados que é habilitado para captura de dados de alteração pode ser espelhado. Para assegurar que a captura e a limpeza ocorram automaticamente após um failover, siga estas etapas:  
  
1.  Verifique se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent está sendo executado na nova instância de servidor principal.  
  
2.  Crie os trabalhos de captura e de limpeza no novo banco de dados principal (o antigo banco de dados espelho). Para criar os trabalhos, use o procedimento armazenado [sp_cdc_add_job](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-add-job-transact-sql) .  
  
 Para exibir a configuração atual de um trabalho de limpeza ou captura, use o procedimento armazenado [sys.sp_cdc_help_jobs](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql) na nova instância de servidor principal. Para um determinado banco de dados, o trabalho de captura é chamado de cdc.*database_name*_capture e o trabalho de limpeza é chamado de cdc.*database_name*_cleanup, em que *database_name* é o nome do banco de dados.  
  
 Para alterar a configuração de um trabalho, use o procedimento armazenado [sys.sp_cdc_change_job](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-change-job-transact-sql) .  
  
 Para obter informações sobre o espelhamento de banco de dados, veja [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).  
  
##  <a name="transactional-replication"></a><a name="TransReplication"></a>Replicação transacional  
 A captura de dados de alteração e a replicação transacional podem coexistir no mesmo banco de dados, mas a população das tabelas de alteração ocorre de modo diferente quando os dois recursos estão habilitados. A captura de dados de alteração e a replicação transacional sempre usam o mesmo procedimento, [sp_replcmds](/sql/relational-databases/system-stored-procedures/sp-replcmds-transact-sql), para ler alterações no log de transações. Quando a captura de dados de alteração é habilitada por iniciativa própria, um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent chama `sp_replcmds`. Quando ambos os recursos estão habilitados no mesmo banco de dados, `sp_replcmds`o agente de leitor de log chama. Esse agente preenche as tabelas de alteração e do banco de dados de distribuição. Para obter mais informações, consulte [Replication Log Reader Agent](../replication/agents/replication-log-reader-agent.md).  
  
 Considere um cenário em que a captura de dados de alteração está habilitada no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e há duas tabelas habilitadas para captura. Para popular as tabelas de alteração, as chamadas `sp_replcmds`de trabalho de captura. O banco de dados está habilitado para replicação transacional, e é criada uma publicação. Agora, o Agente de Leitor de Log é criado para o banco de dados, e o trabalho de captura é excluído. O Agente de Leitor de Log continua a examinar o log do último número de sequência de log confirmado na tabela de alteração. Isso assegura a consistência de dados nas tabelas de alteração. Se a replicação transacional estiver desabilitada nesse banco de dados, o Log Reader Agent será removido e o trabalho de captura, recriado.  
  
> [!NOTE]  
>  Quando o Agente de Leitor de Log for usado para captura de dados e replicação transacional, as alterações replicadas serão gravadas primeiro no banco de dados de distribuição. Em seguida, as alterações capturadas são gravadas nas tabelas de alteração. As duas operações são confirmadas ao mesmo tempo. Se houver uma latência na gravação no banco de dados de distribuição, haverá uma latência correspondente antes de as alterações aparecerem nas tabelas de alteração.  
  
 A opção **proc exec** da replicação transacional não está disponível quando a opção change data capture está habilitada.  
  
##  <a name="restoring-or-attaching-a-database-enabled-for-change-data-capture"></a><a name="RestoreOrAttach"></a>Restaurando ou anexando um banco de dados habilitado para o Change Data Capture  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa a seguinte lógica para determinar se a captura de dados de alteração deve permanecer habilitada depois que um banco de dados for restaurado ou anexado:  
  
-   Se um banco de dados for restaurado para o mesmo servidor com o mesmo nome de banco de dados, a captura de dados de alteração permanecerá habilitada.  
  
-   Se um banco de dados for restaurado para outro servidor, por padrão a captura de dados de alteração será desabilitada, e todos os metadados relacionados serão excluídos.  
  
     Para manter a captura de dados de alteração, use a opção `KEEP_CDC` quando restaurar o banco de dados. Para obter mais informações sobre essa opção, consulte [RESTORE](/sql/t-sql/statements/restore-statements-transact-sql).  
  
-   Se um banco de dados for desanexado e anexado ao mesmo servidor ou a outro servidor, a captura de dados de alteração permanecerá habilitada.  
  
-   Se um banco de dados for anexado ou restaurado com a `KEEP_CDC` opção para qualquer edição diferente de Enterprise, a operação será bloqueada porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a captura de dados de alterações requer Enterprise. A mensagem de erro 934 é exibida:  
  
     `SQL Server cannot load database '%.*ls' because change data capture is enabled. The currently installed edition of SQL Server does not support change data capture. Either disable change data capture in the database by using a supported edition of SQL Server, or upgrade the instance to one that supports change data capture.`  
  
 Você pode usar [sys.sp_cdc_disable_db](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql) para remover a captura de dados de alterações de um banco de dados restaurado ou anexado.  
  
## <a name="change-data-capture-and-alwayson"></a>Change Data Capture e AlwaysON  
 Quando você usa AlwaysON, a enumeração de alteração deve ser feita em replicação secundária para reduzir a carga do disco na réplica primária.  
  
## <a name="see-also"></a>Consulte Também  
 [Administrar e monitorar a captura de dados de alteração &#40;SQL Server&#41;](../track-changes/administer-and-monitor-change-data-capture-sql-server.md)  
  
  
