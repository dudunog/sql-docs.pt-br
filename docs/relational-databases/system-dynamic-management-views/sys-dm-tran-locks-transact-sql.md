---
title: sys. dm_tran_locks (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_tran_locks
- sys.dm_tran_locks
- sys.dm_tran_locks_TSQL
- dm_tran_locks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_locks dynamic management view
ms.assetid: f0d3b95a-8a00-471b-9da4-14cb8f5b045f
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1eb85c3b94de765a15fc60c2641730b6911ffcf5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "80873152"
---
# <a name="sysdm_tran_locks-transact-sql"></a>sys.dm_tran_locks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Retorna informações sobre os recursos de gerenciador de bloqueio ativos atualmente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Cada linha representa uma solicitação ativa no momento para o gerenciador de um bloqueio que foi concedido ou que está aguardando concessão.  
  
 As colunas do conjunto de resultados são divididas em dois grupos principais: recurso e solicitação. O grupo de recurso descreve o recurso em que a solicitação de bloqueio está sendo feita, e o grupo de solicitações descreve a solicitação de bloqueio.  
  
> [!NOTE]  
> Para chamá-lo [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] de [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]ou, use o nome **Sys. dm_pdw_nodes_tran_locks**.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**resource_type**|**nvarchar(60)**|Representa o tipo do recurso. O valor pode ser: DATABASE, FILE, OBJECT, PAGE, KEY, EXTENT, RID, APPLICATION, METADATA, HOBT ou ALLOCATION_UNIT.|  
|**resource_subtype**|**nvarchar(60)**|Representa um subtipo de **resource_type**. A aquisição de um bloqueio de subtipo sem a manutenção de um bloqueio que não seja de subtipo do tipo de pai é tecnicamente válido. Subtipos diferentes não entram em conflito entre si ou com o tipo de pai que não seja de subtipo. Nem todos os tipos do recurso têm subtipos.|  
|**resource_database_id**|**int**|ID do banco de dados em que o recurso serve de escopo. Todos os recursos controlados pelo gerenciador de bloqueio são usados como escopo pela ID do banco de dados.|  
|**resource_description**|**nvarchar(256)**|Descrição do recurso que contém apenas informações não disponíveis em outras colunas de recurso.|  
|**resource_associated_entity_id**|**bigint**|ID da entidade em um banco de dados a que um recurso está associado. Pode ser uma ID de objeto ID, ID do Hobt ou uma ID de unidade de alocação, dependendo do tipo do recurso.|  
|**resource_lock_partition**|**Int**|ID da partição de bloqueio de um recurso de bloqueio particionado. O valor para recursos de bloqueio sem-partição é 0.|  
|**request_mode**|**nvarchar(60)**|Modo da solicitação. Para solicitações concedidas, esse é o modo concedido; para solicitações em espera, esse é o modo sendo solicitado. <br /><br /> NULL = Nenhum acesso concedido ao recurso. Funciona como espaço reservado.<br /><br /> SCH-S (estabilidade do esquema) = garante que um elemento de esquema, como uma tabela ou um índice, não seja Descartado enquanto qualquer sessão mantiver um bloqueio de estabilidade de esquema no elemento de esquema.<br /><br /> SCH-M (modificação de esquema) = deve ser mantido por qualquer sessão que queira alterar o esquema do recurso especificado. Assegura que nenhuma outra sessão esteja fazendo referência ao objeto indicado.<br /><br /> S (compartilhado) = a sessão de retenção recebe acesso compartilhado ao recurso.<br /><br /> U (Update) = indica um bloqueio de atualização adquirido nos recursos que podem eventualmente ser atualizados. É usado para evitar uma forma comum de deadlock que ocorre quando várias sessões bloqueiam recursos para uma atualização potencial no futuro.<br /><br /> X (exclusivo) = a sessão de retenção recebe acesso exclusivo ao recurso.<br /><br /> IS (tentativa compartilhada) = indica a intenção de inserir os bloqueios em algum recurso subordinado na hierarquia de bloqueio.<br /><br /> IU (tentativa de atualização) = indica a intenção de posicionar os bloqueios de U em algum recurso subordinado na hierarquia de bloqueio.<br /><br /> IX (exclusivo da tentativa) = indica a intenção de posicionar X bloqueios em algum recurso subordinado na hierarquia de bloqueio.<br /><br /> O SIU (Shared pretended Update) = indica acesso compartilhado a um recurso com a intenção de adquirir bloqueios de atualização em recursos subordinados na hierarquia de bloqueio.<br /><br /> SEIS (exclusivo da intenção compartilhada) = indica acesso compartilhado a um recurso com a intenção de adquirir bloqueios exclusivos em recursos subordinados na hierarquia de bloqueio.<br /><br /> UIX (atualização de tentativa exclusiva) = indica uma retenção de bloqueio de atualização em um recurso com a intenção de adquirir bloqueios exclusivos em recursos subordinados na hierarquia de bloqueio.<br /><br /> BU = usado por operações em massa.<br /><br /> RangeS_S (intervalo de chaves compartilhado e bloqueio de recurso compartilhado) = indica verificação de intervalo serializável.<br /><br /> RangeS_U (intervalo de chaves compartilhadas e bloqueio de recurso de atualização) = indica verificação de atualização serializável.<br /><br /> RangeI_N (inserir intervalo de chaves e bloqueio de recurso nulo) = usado para testar intervalos antes de inserir uma nova chave em um índice.<br /><br /> RangeI_S = Bloqueio de conversão de intervalo de chaves, criado por uma sobreposição de RangeI_N e S Locks.<br /><br /> RangeI_U = bloqueio de conversão de intervalo de chaves, criado por uma sobreposição de RangeI_N e U Locks.<br /><br /> RangeI_X = bloqueio de conversão de intervalo de chaves, criado por uma sobreposição de RangeI_N e X Locks.<br /><br /> RangeX_S = bloqueio de conversão de intervalo de chaves, criado por uma sobreposição de RangeI_N e RangeS_S. RangeS-S.<br /><br /> RangeX_U = bloqueio de conversão de intervalo de chaves, criado por uma sobreposição de RangeI_N e RangeS_U bloqueios.<br /><br /> RangeX_X (intervalo de chaves exclusivo e bloqueio de recurso exclusivo) = este é um bloqueio de conversão usado ao atualizar uma chave em um intervalo.|  
|**request_type**|**nvarchar(60)**|Tipo de solicitação. O valor é LOCK.|  
|**request_status**|**nvarchar(60)**|Status atual desta solicitação. Os valores possíveis GRANTED, CONVERT, WAIT, LOW_PRIORITY_CONVERT, LOW_PRIORITY_WAIT ou ABORT_BLOCKERS. Para obter mais informações sobre esperas de baixa prioridade e bloqueadores de anulação, consulte a seção *low_priority_lock_wait* de [ALTER INDEX &#40;&#41;Transact-SQL ](../../t-sql/statements/alter-index-transact-sql.md).|  
|**request_reference_count**|**smallint**|Retorna um número aproximado de vezes que o mesmo solicitante solicitou o recurso.|  
|**request_lifetime**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**request_session_id**|**int**|ID da sessão que atualmente possui esta solicitação. A ID da sessão pode ser alterada para transações distribuídas e associadas. Um valor de -2 indica que a solicitação pertence a uma transação distribuída órfã. Um valor de -3 indica que a solicitação pertence a uma transação de recuperação adiada, como uma reversão de transação adiada na recuperação porque a reversão não pôde ser concluída corretamente.|  
|**request_exec_context_id**|**int**|ID do contexto de execução do processo que atualmente possui esta solicitação.|  
|**request_request_id**|**int**|ID de solicitação (ID lote) do processo que atualmente possui esta solicitação. Esse valor será alterado sempre que a conexão ativa MARS (Vários Conjuntos de Resultados Ativos) de uma transação for alterada.|  
|**request_owner_type**|**nvarchar(60)**|Tipo de entidade que é proprietária da solicitação. Solicitações de gerenciador de bloqueio podem ser de propriedade de várias entidades. Os valores possíveis são:<br /><br /> TRANSACTION = A solicitação que é propriedade de uma transação.<br /><br /> CURSOR = A solicitação que é propriedade de um cursor.<br /><br /> SESSION = A solicitação que é propriedade para uma sessão de usuário.<br /><br /> SHARED_TRANSACTION_WORKSPACE = A solicitação que é propriedade de uma parte compartilhada do workspace da transação.<br /><br /> EXCLUSIVE_TRANSACTION_WORKSPACE = A solicitação é de propriedade de uma parte exclusiva do workspace da transação.<br /><br /> NOTIFICATION_OBJECT = A solicitação é de propriedade de um componente interno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse componente solicitou que o gerenciador de bloqueio o notifique quando outro componente estiver esperando para obter o bloqueio. O recurso FileTable é um componente que usa esse valor.<br /><br /> **Observação:** Os espaços de trabalho são usados internamente para manter bloqueios para sessões enlistadas.|  
|**request_owner_id**|**bigint**|ID do proprietário específico desta solicitação.<br /><br /> Quando uma transação for a proprietária da solicitação, esse valor conterá a ID da transação.<br /><br /> Quando uma FileTable for a proprietária da solicitação, **request_owner_id** terá um dos seguintes valores:<br /> <ul><li>**-4** : uma filetable levou um bloqueio de banco de dados.<li> **-3** : uma filetable fez um bloqueio de tabela.<li> **Outro valor** : o valor representa um identificador de arquivo. Esse valor também aparece como **fcb_id** na exibição de gerenciamento dinâmico [sys. dm_filestream_non_transacted_handles &#40;&#41;do Transact-SQL ](../../relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql.md).</li></ul>|  
|**request_owner_guid**|**uniqueidentifier**|GUID do proprietário específico desta solicitação. Esse valor é usado apenas uma transação distribuída em que o valor corresponde ao GUID de MS DTC da transação.|  
|**request_owner_lockspace_id**|**nvarchar(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] Este valor representa a ID de lockspace do solicitante. Essa ID determina se dois solicitantes são compatíveis entre si e podem receber bloqueios nos modos que de outra forma entrariam em conflito entre si.|  
|**lock_owner_address**|**varbinary (8)**|Endereço de memória da estrutura de dados interna que é usada para rastrear esta solicitação. Esta coluna pode ser unida à coluna **resource_address** em **sys.dm_os_waiting_tasks**.|  
|**pdw_node_id**|**int**|**Aplica-se a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)],[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> O identificador do nó em que essa distribuição está.|  
  
## <a name="permissions"></a>Permissões
Ativado [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requer `VIEW SERVER STATE` permissão.   
Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .   
 
## <a name="remarks"></a>Comentários  
 Um status de solicitação concedida indica que um bloqueio foi concedido em um recurso ao solicitante. Uma solicitação de espera indica que a solicitação ainda não foi concedida. Os tipos da solicitação de espera a seguir são retornados pela coluna **request_status**:  
  
-   Um status de solicitação de conversão indica que o solicitante já recebeu uma solicitação referente ao recurso e está no momento aguardando a concessão de atualização para a solicitação inicial.  
  
-   Um status de solicitação de espera indica que o solicitante não mantém no momento uma solicitação concedida no recurso.  
  
 Como **sys.dm_tran_locks** é populado de estruturas de dados do gerenciador de bloqueio interno, a manutenção dessas informações não adicionará sobrecarga extra ao processamento regular. A materialização da exibição requer acesso às estruturas de dados internos do gerenciador de bloqueio. Isso pode ter efeitos secundários no processamento regular no servidor. Esses efeitos não devem ser percebidos e devem afetar somente os recursos bastante usados. Como os dados dessa exibição correspondem ao estado do gerenciador de bloqueio ativo, os dados podem ser alterados a qualquer momento e as linhas são adicionadas e removidas à medida que os bloqueios são adquiridos e liberados. Essa exibição não tem nenhuma informação de histórico.  
  
 Duas solicitações só funcionarão no mesmo recurso se todas as colunas do grupo de recursos forem iguais.  
  
 Você pode controlar o bloqueio de operações de leitura usando as seguintes ferramentas:  
  
-   Use SET TRANSACTION ISOLATION LEVEL para especificar o nível de bloqueio de uma sessão. Para obter mais informações, veja [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md).  
  
-   Use dicas de tabela de bloqueio para especificar o nível de bloqueio de uma referência individual de uma tabela em uma cláusula FROM. Para sintaxe e restrições, consulte [dicas de tabela &#40;&#41;Transact-SQL ](../../t-sql/queries/hints-transact-sql-table.md).  
  
 Um recurso em execução em uma ID de sessão pode ter mais de um bloqueio concedido. Várias entidades em execução em uma sessão podem ter um bloqueio no mesmo recurso e as informações são exibidas nas colunas **request_owner_type** e **request_owner_id** retornadas por **sys.dm_tran_locks**. Se houver várias instâncias da mesma **request_owner_type**, a coluna **request_owner_id** será usada para distinguir cada instância. Para transações distribuídas, as colunas **request_owner_type** e ** request_owner_guid** exibirão as várias informações de entidade.  
  
 Por exemplo, Sessão S1 possui um bloqueio compartilhado em **Table1**; e transação T1, que está em execução na sessão S1, também possui um bloqueio compartilhado em **Table1**. Nesse caso, a coluna **resource_description** retornada por **sys.dm_tran_locks** mostrará duas instâncias do mesmo recurso. A coluna **request_owner_type** mostrará uma instância como sessão e outra como transação. Além disso, a coluna **resource_owner_id** terá valores diferentes.  
  
 Vários cursores em execução em uma sessão são indistinguíveis e são tratados como uma entidade.  
  
 As transações distribuídas não associadas a uma ID de sessão são órfãs e recebem o valor da ID de sessão igual a -2. Para obter mais informações, consulte [KILL &#40;Transact-SQL&#41;](../../t-sql/language-elements/kill-transact-sql.md).  

## <a name="locks"></a><a name="locks"></a>Bloquea
Os bloqueios são mantidos nos recursos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , como linhas lidas ou modificadas durante uma transação, para evitar o uso simultâneo de recursos por transações diferentes. Por exemplo, se um bloqueio exclusivo (X) for mantido em uma linha de uma tabela por uma transação, nenhuma outra transação poderá modificar essa linha até que o bloqueio seja liberado. Minimizar bloqueios aumenta a simultaneidade, o que pode melhorar o desempenho. 

## <a name="resource-details"></a>Detalhes dos recursos  
 A tabela a seguir lista os recursos representados na coluna **resource_associated_entity_id**.  
  
|Tipo de recurso|Descrição do recurso|Resource_associated_entity_id|  
|-------------------|--------------------------|--------------------------------------|  
|DATABASE|Representa um banco de dados.|Não aplicável|  
|FILE|Representa um arquivo de banco de dados. Esse arquivo pode ser um arquivo de log ou de dados.|Não aplicável|  
|OBJECT|Representa um objeto de banco de dados. Esse objeto pode ser uma tabela de dados, uma exibição, um procedimento armazenado, um procedimento armazenado estendido ou qualquer objeto que tenha uma ID de objeto.|ID de objeto|  
|PAGE|Representa uma única página em um arquivo de dados.|ID do HoBt. Esse valor corresponde a **sys.partitions.hobt_id**. A ID do HoBt não está sempre disponível para os recursos PAGE porque ela representa informações extras que podem ser fornecidas pelo chamador, e nem todos os chamadores podem fornecer essas informações.|  
|KEY|Representa uma linha em um índice.|ID do HoBt. Esse valor corresponde a **sys.partitions.hobt_id**.|  
|EXTENT|Representa uma extensão de arquivo de dados. Uma extensão é um grupo de oito páginas contíguas.|Não aplicável|  
|RID|Representa uma linha física em um heap.|ID do HoBt. Esse valor corresponde a **sys.partitions.hobt_id**. A ID do HoBt não está sempre disponível para os recursos RID porque ela representa informações extras que podem ser fornecidas pelo chamador, e nem todos os chamadores podem fornecer essas informações.|  
|APPLICATION|Representa um recurso especificado de aplicativo.|Não aplicável|  
|METADATA|Representa informações de metadados.|Não aplicável|  
|HOBT|Representa um heap ou uma árvore B. Essas são as estruturas de caminho de acesso básicas.|ID do HoBt. Esse valor corresponde a **sys.partitions.hobt_id**.|  
|ALLOCATION_UNIT|Representa um conjunto de páginas relacionadas, como uma partição de índice. Cada unidade de alocação cobre uma única cadeia de página IAM.|ID da unidade de alocação. Esse valor corresponde a **sys.allocation_units.allocation_unit_id**.|  
  
 A tabela a seguir lista os subtipos associados a cada tipo de recurso.  
  
|ResourceSubType|Sincroniza|  
|---------------------|------------------|  
|ALLOCATION_UNIT.BULK_OPERATION_PAGE|Páginas pré-alocadas usadas para operações em massa.|  
|ALLOCATION_UNIT.PAGE_COUNT|Estatísticas de contagem de páginas de unidade de alocação durante as operações de descarte adiadas.|  
|DATABASE.BULKOP_BACKUP_DB|Backups de banco de dados com operações em massa.|  
|DATABASE.BULKOP_BACKUP_LOG|Backups de log de banco de dados com operações em massa.|  
|DATABASE.CHANGE_TRACKING_CLEANUP|Tarefas de limpeza do controle de alterações.|  
|DATABASE.CT_DDL|Banco de dados e operações DDL de controle de alterações do nível de tabela.|  
|DATABASE.CONVERSATION_PRIORITY|Operações de prioridade de conversa do Service Broker como CREATE BROKER PRIORITY.|  
|DATABASE.DDL|Operações DDL (linguagem de definição de dados) com operações de grupo de arquivos, como descarte.|  
|DATABASE.ENCRYPTION_SCAN|Sincronização de criptografia de TDE.|  
|DATABASE.PLANGUIDE|Sincronização de guia de plano.|  
|DATABASE.RESOURCE_GOVERNOR_DDL|Operações de DDL para operações de administrador de recurso como ALTER RESOURCE POOL.|  
|DATABASE.SHRINK|Operações de redução de banco de dados.|  
|DATABASE.STARTUP|Usado para sincronização de inicialização de banco de dados.|  
|FILE.SHRINK|Operações de redução de arquivo.|  
|HOBT.BULK_OPERATION|Operações de carregamento em massa otimizadas para heap com verificação simultânea nestes níveis de isolamento: instantâneo, leitura não confirmada e leitura confirmada com controle de versão de linha.|  
|HOBT.INDEX_REORGANIZE|Operações de reorganização de heap ou índice.|  
|OBJECT.COMPILE|Compilação de procedimento armazenado.|  
|OBJECT.INDEX_OPERATION|Operações de índice.|  
|OBJECT.UPDSTATS|Atualizações de estatísticas em uma tabela.|  
|METADATA.ASSEMBLY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASSEMBLY_CLR_NAME|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASSEMBLY_TOKEN|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASYMMETRIC_KEY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT_ACTIONS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT_SPECIFICATION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AVAILABILITY_GROUP|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CERTIFICATE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CHILD_INSTANCE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.COMPRESSED_FRAGMENT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.COMPRESSED_ROWSET|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSTATION_ENDPOINT_RECV|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSTATION_ENDPOINT_SEND|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_GROUP|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_PRIORITY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CREDENTIAL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CRYPTOGRAPHIC_PROVIDER|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATA_SPACE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATABASE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATABASE_PRINCIPAL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_MIRRORING_SESSION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_MIRRORING_WITNESS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_PRINCIPAL_SID|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ENDPOINT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ENDPOINT_WEBMETHOD|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.EXPR_COLUMN|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.EXPR_HASH|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_CATALOG|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_INDEX|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_STOPLIST|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INDEX_EXTENSION_SCHEME|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INDEXSTATS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INSTANTIATED_TYPE_HASH|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.MESSAGE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.METADATA_CACHE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PARTITION_FUNCTION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PASSWORD_POLICY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PERMISSIONS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PLAN_GUIDE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PLAN_GUIDE_HASH|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PLAN_GUIDE_SCOPE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.QNAME|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.QNAME_HASH|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.REMOTE_SERVICE_BINDING|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ROUTE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SCHEMA|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SECURITY_CACHE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SECURITY_DESCRIPTOR|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SEQUENCE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER_EVENT_SESSIONS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER_PRINCIPAL|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_BROKER_GUID|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_CONTRACT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_MESSAGE_TYPE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.STATS|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SYMMETRIC_KEY|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.USER_TYPE|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_COLLECTION|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_COMPONENT|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_INDEX_QNAME|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 A tabela seguinte fornece o formato da coluna **resource_description** para cada tipo de recurso.  
  
|Recurso|Formatar|Descrição|  
|--------------|------------|-----------------|  
|DATABASE|Não aplicável|A ID de banco de dados já está disponível na coluna **resource_database_id**.|  
|FILE|<file_id>|ID do arquivo representado por esse recurso.|  
|OBJECT|<object_id>|ID do objeto representado por esse recurso. Este objeto pode ser qualquer objeto listado em **sys.objects**, não apenas uma tabela.|  
|PAGE|<file_id>:<page_in_file>|Representa o arquivo e a ID da página representada por esse recurso.|  
|KEY|<hash_value>|Representa um hash das colunas principais da linha representada por esse recurso.|  
|EXTENT|<file_id>:<page_in_files>|Representa o arquivo e a ID da extensão representada por esse recurso. A ID de extensão é igual à ID da página da primeira página na extensão.|  
|RID|<file_id>:<page_in_file>:<row_on_page>|Representa a ID da página e a ID da linha representada por esse recurso. Observe que se a ID de objeto associada for 99, esse recurso representará um dos oito slots de página misturados na primeira página IAM de uma cadeia IAM.|  
|APPLICATION|\<DbPrincipalId>:\<até 32 caracteres>:(<HASH_VALUE>)|Representa a ID do banco de dados principal usado para fazer o escopo desse recurso de bloqueio de aplicativo. Também incluídos estão até 32 caracteres da cadeia de caracteres de recurso que corresponde a este recurso de bloqueio de aplicativo. Em certos casos, podem ser exibidos só 2 caracteres devido à cadeia de caracteres cheia que já não está mais disponível. Esse comportamento ocorre apenas no momento da recuperação do banco de bancos com relação aos bloqueios que são readquiridos como parte do processo de recuperação. O valor de hash representa um hash da cadeia de caracteres de recurso cheia, que corresponde a esse recurso de bloqueio de aplicativo.|  
|HOBT|Não aplicável|ID do HOBT está incluída como **resource_associated_entity_id**.|  
|ALLOCATION_UNIT|Não aplicável|A ID da unidade de alocação está incluída como **resource_associated_entity_id**.|  
|METADATA.ASSEMBLY|assembly_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASSEMBLY_CLR_NAME|$qname_id = Q|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASSEMBLY_TOKEN|assembly_id = A, $token_id|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ASSYMMETRIC_KEY|asymmetric_key_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT|audit_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT_ACTIONS|device_id = D, major_id = M|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AUDIT_SPECIFICATION|audit_specification_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.AVAILABILITY_GROUP|availability_group_id = A|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CERTIFICATE|certificate_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CHILD_INSTANCE|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.COMPRESSED_FRAGMENT|object_id = O , compressed_fragment_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.COMPRESSED_ROW|object_id = O|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSTATION_ENDPOINT_RECV|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSTATION_ENDPOINT_SEND|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_GROUP|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CONVERSATION_PRIORITY|conversation_priority_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CREDENTIAL|credential_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.CRYPTOGRAPHIC_PROVIDER|provider_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATA_SPACE|data_space_id = D|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATABASE|database_id = D|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DATABASE_PRINCIPAL|principal_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_MIRRORING_SESSION|database_id = D|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_MIRRORING_WITNESS|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.DB_PRINCIPAL_SID|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ENDPOINT|endpoint_id = E|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ENDPOINT_WEBMETHOD|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_CATALOG|fulltext_catalog_id = F|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_INDEX|object_id = O|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.EXPR_COLUMN|object_id = O, column_id = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.EXPR_HASH|object_id = O, $hash = H|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_CATALOG|fulltext_catalog_id = F|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_INDEX|object_id = O|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.FULLTEXT_STOPLIST|fulltext_stoplist_id = F|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INDEX_EXTENSION_SCHEME|index_extension_id = I|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INDEXSTATS|object_id = O, index_id or stats_id = I|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.INSTANTIATED_TYPE_HASH|user_type_id = U, hash = H|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.MESSAGE|message_id = M|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.METADATA_CACHE|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PARTITION_FUNCTION|function_id = F|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PASSWORD_POLICY|principal_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PERMISSIONS|class = C|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.PLAN_GUIDE|plan_guide_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA. PLAN_GUIDE_HASH|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA. PLAN_GUIDE_SCOPE|scope_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.QNAME|$qname_id = Q|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.QNAME_HASH|$qname_scope_id = Q, $qname_hash = H|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.REMOTE_SERVICE_BINDING|remote_service_binding_id = R|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.ROUTE|route_id = R|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SCHEMA|schema_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SECURITY_CACHE|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SECURITY_DESCRIPTOR|sd_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SEQUENCE|$seq_type = S, object_id = O|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER|server_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER_EVENT_SESSIONS|event_session_id = E|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVER_PRINCIPAL|principal_id = P|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE|service_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_BROKER_GUID|$hash = H1:H2:H3|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_CONTRACT|service_contract_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SERVICE_MESSAGE_TYPE|message_type_id = M|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.STATS|object_id = O, stats_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.SYMMETRIC_KEY|symmetric_key_id = S|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.USER_TYPE|user_type_id = U|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_COLLECTION|xml_collection_id = X|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_COMPONENT|xml_component_id = X|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|METADATA.XML_INDEX_QNAME|object_id = O, $qname_id = Q|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 Os XEvents a seguir estão relacionados à **opção** de partição e à recompilação de índice online. Para obter informações sobre a sintaxe, consulte [ALTER TABLE &#40;Transact-sql&#41;](../../t-sql/statements/alter-table-transact-sql.md) e [ALTER INDEX &#40;&#41;do Transact-SQL ](../../t-sql/statements/alter-index-transact-sql.md).  
  
-   lock_request_priority_state  
  
-   process_killed_by_abort_blockers  
  
-   ddl_with_wait_at_low_priority  
  
 O **Progress_report_online_index_operation** XEvent existente para operações de índice online foi estendido adicionando **partition_number** e **partition_id**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-sysdm_tran_locks-with-other-tools"></a>a. Usando sys.dm_tran_locks com outras ferramentas  
 O exemplo a seguir trabalha com um cenário no qual uma operação de atualização é bloqueada por outra transação. Usando **sys.dm_tran_locks** e outras ferramentas, são fornecidas informações sobre como bloquear recursos.  
  
```sql  
USE tempdb;  
GO  
  
-- Create test table and index.  
CREATE TABLE t_lock  
    (  
    c1 int, c2 int  
    );  
GO  
  
CREATE INDEX t_lock_ci on t_lock(c1);  
GO  
  
-- Insert values into test table  
INSERT INTO t_lock VALUES (1, 1);  
INSERT INTO t_lock VALUES (2,2);  
INSERT INTO t_lock VALUES (3,3);  
INSERT INTO t_lock VALUES (4,4);  
INSERT INTO t_lock VALUES (5,5);  
INSERT INTO t_lock VALUES (6,6);  
GO  
  
-- Session 1  
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;  
  
BEGIN TRAN  
    SELECT c1  
        FROM t_lock  
        WITH(holdlock, rowlock);  
  
-- Session 2  
BEGIN TRAN  
    UPDATE t_lock SET c1 = 10  
```  
  
 A consulta a seguir exibirá informações de bloqueio. O valor de `<dbid>` deve ser substituído pelo **database_id** de **sys.databases**.  
  
```sql  
SELECT resource_type, resource_associated_entity_id,  
    request_status, request_mode,request_session_id,  
    resource_description   
    FROM sys.dm_tran_locks  
    WHERE resource_database_id = <dbid>  
```  
  
 A consulta a seguir retorna informações de objeto usando `resource_associated_entity_id` na consulta anterior. Essa consulta deverá ser executada enquanto você estiver conectado ao banco de dados que contém o objeto.  
  
```  
SELECT object_name(object_id), *  
    FROM sys.partitions  
    WHERE hobt_id=<resource_associated_entity_id>  
```  
  
 A consulta a seguir mostrará informações de bloqueio.  
  
```sql  
SELECT   
        t1.resource_type,  
        t1.resource_database_id,  
        t1.resource_associated_entity_id,  
        t1.request_mode,  
        t1.request_session_id,  
        t2.blocking_session_id  
    FROM sys.dm_tran_locks as t1  
    INNER JOIN sys.dm_os_waiting_tasks as t2  
        ON t1.lock_owner_address = t2.resource_address;  
```  
  
 Libere recursos revertendo as transações.  
  
```sql  
-- Session 1  
ROLLBACK;  
GO  
  
-- Session 2  
ROLLBACK;  
GO  
```  
  
### <a name="b-linking-session-information-to-operating-system-threads"></a>B. Vinculando informações de sessão a threads do sistema operacional  
 O exemplo a seguir retorna informações que associam uma ID de sessão a uma ID de thread do Windows. O desempenho do thread pode ser monitorado no Monitor de Desempenho do Windows. Essa consulta não retorna IDs de sessão atualmente suspensos.  
  
```sql  
SELECT STasks.session_id, SThreads.os_thread_id  
    FROM sys.dm_os_tasks AS STasks  
    INNER JOIN sys.dm_os_threads AS SThreads  
        ON STasks.worker_address = SThreads.worker_address  
    WHERE STasks.session_id IS NOT NULL  
    ORDER BY STasks.session_id;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
[sys. dm_tran_database_transactions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-database-transactions-transact-sql.md)      
[Funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)     
[Funções e exibições de gerenciamento dinâmico relacionadas à transação &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)      
[SQL Server, objeto Locks](../../relational-databases/performance-monitor/sql-server-locks-object.md)      
