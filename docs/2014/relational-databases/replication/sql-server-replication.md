---
title: Replicação do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], about
- replication [SQL Server]
ms.assetid: 3a5f4592-3c61-4b4d-9ceb-39716aeeba41
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: be03754ea8eeb61d838357667da6e37e1be6bc31
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62626142"
---
# <a name="sql-server-replication"></a>Replicação do SQL Server
  A replicação é um conjunto de tecnologias para copiar e distribuir dados e objetos de um banco de dados para outro e, em seguida, sincronizar entre os bancos de dados para manter a consistência. Usando replicação, é possível distribuir dados para diferentes locais e para usuários remotos e móveis através de redes locais e de longa distância, conexões discadas, conexões sem-fio e a Internet.  
  
 A replicação transacional normalmente é usada em cenários de servidor para servidor que requerem alta taxa de transferência, incluindo: melhora da escalabilidade e disponibilidade; armazenamento de dados data warehouse e relatórios; integração de dados de vários sites; integração de dados heterogêneos e descarregamento de processamento em lote. A replicação de mesclagem é projetada principalmente para aplicativos móveis ou de servidor distribuído que possuem possíveis conflitos de dados. Os cenários comuns incluem: troca de dados com usuários móveis; aplicativos de POS (ponto de vendas) para o consumidor e integração de dados de vários sites. A replicação de instantâneo é usada para fornecer o conjunto inicial de dados para replicação transacional e de mesclagem. Ela também pode ser usada quando atualizações completas de dados forem apropriadas. Com esses três tipos de replicação, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece um sistema poderoso e flexível para sincronizar dados em sua empresa. A replicação para SQLCE 3.5 e SQLCE 4.0 tem suporte no [!INCLUDE[win8srv](../../includes/win8srv-md.md)] e no [!INCLUDE[win8](../../includes/win8-md.md)].  
  
 Como alternativa à replicação, você pode sincronizar bancos de dados por meio do Microsoft Sync Framework. O Sync Framework inclui componentes e uma API intuitiva e flexível que facilitam a sincronização entre os bancos de dados SQL Server, SQL Server Express, SQL Server Compact e SQL Azure. O Sync Framework também incluir classes que podem ser adaptadas para sincronização entre um banco de dados do SQL Server e qualquer outro banco de dados que seja compatível com o ADO.NET. Para obter a documentação detalhada dos componentes de sincronização de banco de dados do Sync Framework, consulte [Sincronizando bancos de dados](https://go.microsoft.com/fwlink/?LinkId=209079). Para obter uma visão geral do Sync Framework, consulte a [Central do desenvolvedor do Microsoft Sync Framework](https://go.microsoft.com/fwlink/?LinkId=209078). Para obter uma comparação entre o Sync Framework e Replicação de Mesclagem, consulte [Visão geral da sincronização de bancos de dados](https://msdn.microsoft.com/library/bb902818\(SQL.110\).aspx)  
  

## <a name="whats-new"></a>Novidades 
- O SQL Server 2017 não incorporou novos recursos significativos para Replicação do SQL Server. 
- O SQL Server 2016 não incorporou novos recursos significativos para Replicação do SQL Server. 

Para informações de compatibilidade com versões anteriores, confira [Compatibilidade de replicação com versões anteriores](replication-backward-compatibility.md) 


 ## <a name="replication-security"></a>Segurança de replicação
  
-   [Exibir e modificar as configurações de segurança de replicação](security/view-and-modify-replication-security-settings.md)  
-   [Gerenciar logons na lista de acesso à publicação](security/manage-logins-in-the-publication-access-list.md)  
  
## <a name="publishing-and-distribution"></a>Publicação e Distribuição  
  
-   [Configurar a publicação e a distribuição](configure-publishing-and-distribution.md)   
-   [Exibir e modificar as propriedades da publicação](publish/view-and-modify-publication-properties.md)   
-   [Desabilitar publicação e distribuição](disable-publishing-and-distribution.md)  
  
## <a name="publications-and-articles"></a>Publicações e Artigos 
  
-   [Criar uma publicação](publish/create-a-publication.md)    
-   [Definir um artigo](publish/define-an-article.md)   
-   [Exibir e modificar as propriedades da publicação](publish/view-and-modify-publication-properties.md)   
-   [Exibir e modificar as propriedades do artigo](publish/view-and-modify-article-properties.md)    
-   [Excluir uma publicação](publish/delete-a-publication.md)   
-   [Excluir um artigo](publish/delete-an-article.md)    
-   [Criar uma publicação de um Banco de Dados Oracle](publish/create-a-publication-from-an-oracle-database.md)   
-   [Definir o período de validade da assinatura](publish/set-the-expiration-period-for-subscriptions.md)  
-   [Especificar opções de esquema](publish/specify-schema-options.md)  
-   [Replicar alterações de esquema](publish/replicate-schema-changes.md)    
-   [Gerenciar colunas de identidade](publish/manage-identity-columns.md)   
-   [Definir o nível de compatibilidade para publicações de mesclagem](publish/set-the-compatibility-level-for-merge-publications.md)  
  
### <a name="snapshot-options"></a>Opções de instantâneo  
  
-   [Configurar propriedades de instantâneo](publish/configure-snapshot-properties-replication-transact-sql-programming.md)    
-   [Entregar um instantâneo por FTP](publish/deliver-a-snapshot-through-ftp.md) 
  
### <a name="filter-data"></a>Filtrar Dados  
  
-   [Definir e modificar um filtro de colunas](publish/define-and-modify-a-column-filter.md)    
-   [Definir e modificar um filtro de linha estático](publish/define-and-modify-a-static-row-filter.md)    
-   [Definir e modificar um filtro de linha parametrizado para um artigo de mesclagem](publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)    
-   [Otimizar filtros de linha com parâmetros](publish/optimize-parameterized-row-filters.md)    
-   [Definir e modificar um filtro de junção entre artigos de mesclagem](publish/define-and-modify-a-join-filter-between-merge-articles.md)  
  
### <a name="transactional-replication-options"></a>Opções de replicação transacional  
  
-   [Definir o método de propagação de alterações de dados para artigos transacionais](publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)    
-   [Habilitar atualização de assinaturas para publicações transacionais](publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
### <a name="merge-replication-options"></a>Opções de replicação de mesclagem  
  
-   [Define a Logical Record Relationship Between Merge Table Articles](publish/define-a-logical-record-relationship-between-merge-table-articles.md)    
-   [Especificar propriedades de replicação de mesclagem](publish/specify-merge-replication-properties.md)    
-   [Especificar um resolvedor de artigo de mesclagem](publish/specify-a-merge-article-resolver.md)    

  
## <a name="manage-subscriptions"></a>Gerenciar assinaturas  
  
-   [Create a Pull Subscription](create-a-pull-subscription.md)    
-   [Exibir e modificar propriedades de assinatura pull](view-and-modify-pull-subscription-properties.md)    
-   [Excluir uma assinatura pull](delete-a-pull-subscription.md)    
-   [Criar uma assinatura push](create-a-push-subscription.md)   
-   [Exibir e modificar propriedades de assinatura push](view-and-modify-push-subscription-properties.md)   
-   [Excluir uma assinatura push](delete-a-push-subscription.md)   
-   [Especificar agendas de sincronização](specify-synchronization-schedules.md)    
-   [Criar uma assinatura atualizável em uma publicação transacional](publish/create-an-updatable-subscription-to-a-transactional-publication.md)  
-   [Criar uma assinatura para um Assinante não SQL Server](create-a-subscription-for-a-non-sql-server-subscriber.md)  
  
## <a name="synchronize-subscriptions"></a>Sincronizar Assinaturas  
  
-   [Criar e aplicar o instantâneo inicial](create-and-apply-the-initial-snapshot.md)   
-   [Criar um instantâneo para uma publicação de mesclagem com filtros parametrizados](create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)    
-   [Inicializar uma assinatura transacional de um backup](initialize-a-transactional-subscription-from-a-backup.md)    
-   [Inicializar uma assinatura manualmente](initialize-a-subscription-manually.md)    
-   [Sincronizar uma assinatura pull](synchronize-a-pull-subscription.md)    
-   [Sincronizar uma assinatura push](synchronize-a-push-subscription.md)   
-   [Reinicializar uma assinatura](reinitialize-a-subscription.md)    
-   [Executar scripts durante sincronização](execute-scripts-during-synchronization-replication-transact-sql-programming.md)    
-   [Implementar um manipulador de lógica de negócios para um artigo de mesclagem](implement-a-business-logic-handler-for-a-merge-article.md)  
-   [Depurar um manipulador de lógica de negócios &#40;Programação de Replicação&#41;](debug-a-business-logic-handler-replication-programming.md)    
-   [Controlar o comportamento de gatilhos e restrições durante a sincronização](control-behavior-of-triggers-and-constraints-in-synchronization.md)    
-   [Implementar um resolvedor de conflitos personalizado para um artigo de mesclagem](implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
## <a name="administeration"></a>Administração do 
  
-   [Trabalhar com perfis do Agente de Replicação](agents/work-with-replication-agent-profiles.md)   
-   [Validar dados no assinante](validate-data-at-the-subscriber.md)    
-   [Gerenciar partições para uma publicação de mesclagem com filtros com parâmetros](publish/manage-partitions-for-a-merge-publication-with-parameterized-filters.md)    
-   [Carregar dados em massa em tabelas em uma publicação de mesclagem](bulk-load-data-into-tables-in-a-merge-publication.md)    
-   [Limpar metadados de mesclagem](administration/clean-up-merge-metadata-replication-transact-sql-programming.md)    
-   [Executar uma atualização fictícia para um artigo de mesclagem](administration/perform-a-dummy-update-for-a-merge-article-replication-transact-sql-programming.md)    
-   [Exibir comandos replicados e outras informações no banco de dados de distribuição](monitor/view-replicated-commands-and-information-in-distribution-database.md)    
-   [Habilitar backups coordenados para replicação transacional](administration/enable-coordinated-backups-for-transactional-replication.md)   
-   [Administrar uma topologia ponto a ponto](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md)    
-   [Desativar uma topologia de replicação](administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)    
-   [Configurar o trabalho do conjunto de transações para um Publicador Oracle](administration/configure-the-transaction-set-job-for-an-oracle-publisher.md)   
-   [Atualizar scripts de replicação](administration/upgrade-replication-scripts-replication-transact-sql-programming.md)  
  
## <a name="monitor"></a>Monitoramento
  
-   [Permitir que não administradores usem o Replication Monitor](monitor/allow-non-administrators-to-use-replication-monitor.md)    
-   [Monitorar a replicação de forma programática](monitor/programmatically-monitor-replication.md)    
-   [Exibir comandos replicados e outras informações no banco de dados de distribuição](monitor/view-replicated-commands-and-information-in-distribution-database.md)    
-   [Exibir informações sobre conflitos para publicações de mesclagem](view-conflict-information-for-merge-publications.md) 
-   [Medir a latência e validar as conexões para a replicação transacional](monitor/measure-latency-and-validate-connections-for-transactional-replication.md)  
  