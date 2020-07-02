---
title: sp_changemergearticle (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/09/2015
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changemergearticle_TSQL
- sp_changemergearticle
helpviewer_keywords:
- sp_changemergearticle
ms.assetid: 0dc3da5c-4af6-45be-b5f0-074da182def2
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 97c6a7d309578ebe0cc6e93b5408ad6d9fad6296
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771510"
---
# <a name="sp_changemergearticle-transact-sql"></a>sp_changemergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Altera as propriedades de um artigo de mesclagem. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changemergearticle [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação na qual o artigo existe. a *publicação* é **sysname**, sem padrão.  
  
`[ @article = ] 'article'`É o nome do artigo a ser alterado. o *artigo* é **sysname**, sem padrão.  
  
`[ @property = ] 'property'`É a propriedade a ser alterada para o artigo e a publicação fornecidos. a *Propriedade* é **nvarchar (30)** e pode ser um dos valores listados na tabela.  
  
`[ @value = ] 'value'`É o novo valor para a propriedade especificada. *Value* é **nvarchar (1000)** e pode ser um dos valores listados na tabela.  
  
 Essa tabela descreve as propriedades de artigos e os valores dessas propriedades.  
  
|Propriedade|Valores|Descrição|  
|--------------|------------|-----------------|  
|**allow_interactive_resolver**|**true**|Habilita o uso de um resolvedor interativo para o artigo.|  
||**false**|Desabilita o uso de um resolvedor interativo para o artigo.|  
|**article_resolver**||Resolvedor personalizado para o artigo. Aplica-se somente a um artigo de tabela.|  
|**check_permissions** (bitmap)|**0x00**|Permissões em nível de tabela não são verificadas.|  
||**0x10**|Permissões em nível de tabela são verificadas no Publicador antes que as instruções INSERT feitas no Assinante sejam aplicadas no Publicador.|  
||**0x20**|Permissões em nível de tabela são verificadas no Publicador antes que as instruções UPDATE feitas no Assinante sejam aplicadas no Publicador.|  
||**0x40**|Permissões em nível de tabela são verificadas no Publicador antes que as instruções DELETE feitas no Assinante sejam aplicadas no Publicador.|  
|**column_tracking**|**true**|Ativa o rastreamento em nível de coluna. Aplica-se somente a um artigo de tabela.<br /><br /> Observação: o controle de nível de coluna não pode ser usado ao publicar tabelas com mais de 246 colunas.|  
||**false**|Ativa o rastreamento em nível de coluna e deixa a detecção de conflito no nível de linha. Aplica-se somente a um artigo de tabela.|  
|**compensate_for_errors**|**true**|Ações de compensação são executadas quando ocorrem erros durante a sincronização. Para obter mais informações, consulte [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).|  
||**false**|As ações de compensação não são executadas, o que é o comportamento padrão. Para obter mais informações, consulte [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).<br /><br /> Importante embora os dados nas linhas afetadas pareçam estar fora de convergência, assim que você resolver erros, as alterações poderão ser aplicadas e os dados convergirão. ** \* \* \* \* ** Se a tabela de origem de um artigo já estiver publicada em outra publicação, o valor de *compensate_for_errors* deverá ser o mesmo para ambos os artigos.|  
|**creation_script**||Caminho e nome de um script de esquema de artigo opcional usados para criar o artigo no banco de dados de assinatura.|  
|**delete_tracking**|**true**|Instruções DELETE são replicadas, o que é o comportamento padrão.|  
||**false**|Instruções DELETE não são replicadas.<br /><br /> ** \* \* Importante \* a \* ** configuração **delete_tracking** como **falso** resulta em não convergência e as linhas excluídas precisam ser removidas manualmente.|  
|**ndescrição**||Entrada descritiva para o artigo.|  
|**destination_owner**||Nome do proprietário do objeto no banco de dados de assinatura, se não for **dbo**.|  
|**identity_range**||**bigint** que especifica o tamanho do intervalo a ser usado ao atribuir novos valores de identidade se o artigo tiver **identityrangemanagementoption** definido como **auto** ou **auto_identity_range** definido como **true**. Aplica-se apenas a um artigo de tabela. Para obter mais informações, consulte a seção "replicação de mesclagem" de [replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**identityrangemanagementoption**|**Manual**|Desabilita gerenciamento automático do intervalo de identidade. Marca colunas de identidade com NOT FOR REPLICATION para ativar o tratamento manual do intervalo de identidade. Para obter mais informações, consulte [Replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
||**nenhum**|Desabilita todo o gerenciamento do intervalo de identidade.|  
|**logical_record_level_conflict_detection**|**true**|Um conflito será detectado se forem feitas alterações no registro lógico. Requer que **logical_record_level_conflict_resolution** seja definido como **true**.|  
||**false**|A detecção de conflito padrão é usada conforme especificado pelo **column_tracking**.|  
|**logical_record_level_conflict_resolution**|**true**|Todo o registro lógico vencedor substitui o registro lógico perdedor.|  
||**false**|As linhas vencedoras não são restringidas ao registro lógico.|  
|**partition_options**|**0**|A filtragem do artigo é estática ou não gera um subconjunto único de dados para cada partição, ou seja, uma partição “sobreposta”.|  
||**1**|As partições são sobrepostas e as atualizações DML feitas no Assinante não podem alterar a partição a qual uma linha pertence.|  
||**2**|A filtragem do artigo gera partições não sobrepostas, mas vários Assinantes podem receber a mesma partição.|  
||**3**|A filtragem para o artigo gera partições não sobrepostas exclusivas de cada assinatura.<br /><br /> Observação: se você especificar um valor de **3** para **partition_options**, pode haver apenas uma única assinatura para cada partição de dados nesse artigo. Se uma segunda assinatura for criada na qual o critério de filtragem da nova assinatura for resolvido para a mesma partição como a assinatura existente, a assinatura existente será cancelada.|  
|**pre_creation_command**|**nenhum**|Se a tabela já existir no Assinante, nenhuma ação será tomada.|  
||**delete**|Emite uma exclusão com base na cláusula WHERE no filtro de subconjunto.|  
||**suspensa**|Cancela a tabela antes de recriá-la.|  
||**truncar**|Trunca a tabela de destino.|  
|**processing_order**||**int** que indica a ordem de processamento dos artigos em uma publicação de mesclagem.|  
|**pub_identity_range**||**bigint** que especifica o tamanho do intervalo alocado a um assinante com uma assinatura de servidor se o artigo tiver **identityrangemanagementoption** definido como **auto** ou **auto_identity_range** definido como **true**. Esse intervalo de identidade é reservado para um Assinante de republicação para ser alocado a seus próprios Assinantes. Aplica-se apenas a um artigo de tabela. Para obter mais informações, consulte a seção "replicação de mesclagem" de [replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**published_in_tran_pub**|**true**|Artigo também é publicado em uma publicação transacional.|  
||**false**|O artigo também não é publicado em uma publicação transacional.|  
|**resolver_info**||É usado para especificar informações adicionais requeridas por um determinador personalizado. Alguns resolvedores do [!INCLUDE[msCoName](../../includes/msconame-md.md)] necessitam de uma coluna fornecida como entrada para o resolvedor. **resolver_info** é **nvarchar (255)**, com um padrão de NULL. Para obter mais informações, consulte [Resolvedores Microsoft baseados em COM](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md).|  
|**schema_option** (bitmap)||Para obter mais informações, consulte a seção Comentários, mais adiante neste tópico.|  
||**0x00**|Desabilita o script pelo Agente de Instantâneo e usa o script fornecido no **creation_script**.|  
||**0x01**|Gera o script de criação de objeto (CREATE TABLE, CREATE PROCEDURE e assim por diante).|  
||**0x10**|Gera um índice clusterizado correspondente.|  
||**0x20**|Converte tipos de dados definidos pelo usuário em tipos de dados base no Assinante. Essa opção não poderá ser usada quando houver uma restrição CHECK ou DEFAULT em uma coluna UDT (tipo definido pelo usuário), se uma coluna UDT fizer parte da chave primária ou se uma coluna computada fizer referência a uma coluna UDT.|  
||**0x40**|Gera índices não clusterizados correspondentes.|  
||**0x80**|Inclui integridade referencial declarada nas chaves primárias.|  
||**0x100**|Replica gatilhos de usuário em um artigo de tabela, se definido.|  
||**0x200**|Replica restrições FOREIGN KEY. Se a tabela referenciada não fizer parte de uma publicação, todas as restrições FOREIGN KEY em uma tabela publicada não serão replicadas.|  
||**0x400**|Replica restrições CHECK.|  
||**0x800**|Replica padrões.|  
||**0x1000**|Replica ordenação em nível de coluna.|  
||**0x2000**|Replica propriedades estendidas associadas com o objeto de origem do artigo publicado.|  
||**0x4000**|Replica chaves exclusivas definidas em um artigo de tabela.|  
||**0x8000**|Gera instruções ALTER TABLE em scripts de restrições.|  
||**0x10000**|Replica instruções CHECK como NOT FOR REPLICATION para que as restrições não sejam forçadas durante a sincronização.|  
||**0x20000**|Replica instruções FOREIGN KEY como NOT FOR REPLICATION para que as restrições não sejam forçadas durante a sincronização.|  
||**0x40000**|Replica grupos de arquivos associados a uma tabela ou índice particionado.|  
||**0x80000**|Replica o esquema de partição para uma tabela particionada.|  
||**0x100000**|Replica o esquema de partição para um índice particionado.|  
||**0x200000**|Replica estatísticas de tabela.|  
||**0x400000**|Replica associações padrão|  
||**0x800000**|Replica associações de regra.|  
||**0x1000000**|Replica o índice de texto completo.|  
||**0x2000000**|As coleções de esquema XML vinculadas a colunas **XML** não são replicadas.|  
||**0x4000000**|Replica índices em colunas **XML** .|  
||**0x8000000**|Cria qualquer esquema ainda não presente no assinante.|  
||**0x10000000**|Converte colunas **XML** em **ntext** no Assinante.|  
||**0x20000000**|Converte tipos de dados de objeto grande (**nvarchar (max)**, **varchar (max)** e **varbinary (max)**) que foram introduzidos nos [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] tipos de dados com suporte no [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] .|  
||**0x40000000**|Replicar permissões.|  
||**0x80000000**|Tente descartar as dependências de todos os objetos que não fazem parte da publicação.|  
||**0x100000000**|Use esta opção para replicar o atributo FILESTREAM se ele for especificado em colunas **varbinary (max)** . Não especifique essa opção se você estiver replicando tabelas para Assinantes [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Não há suporte para a replicação de tabelas que têm colunas FILESTREAM para [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] assinantes, independentemente de como essa opção de esquema está definida. Consulte a opção relacionada **0x800000000**.|  
||**0x200000000**|Converte os tipos de dados de data e hora (**Date**, **time**, **DateTimeOffset**e **datetime2**) que são introduzidos nos [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] tipos de dados com suporte em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
||**0x400000000**|Replica a opção de compactação para dados e índices. Para saber mais, veja [Data Compression](../../relational-databases/data-compression/data-compression.md).|  
||**0x800000000**|Defina essa opção para armazenar dados FILESTREAM em seu próprio grupo de arquivos no Assinante. Se essa opção não for definida, os dados FILESTREAM serão armazenados no grupo de arquivos padrão. A replicação não cria grupos de arquivos; portanto, se você definir essa opção, deverá criar o grupo de arquivos antes de aplicar o instantâneo no Assinante. Para obter mais informações sobre como criar objetos antes de aplicar o instantâneo, consulte [executar scripts antes e depois que o instantâneo for aplicado](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied).<br /><br /> Consulte a opção relacionada **0x100000000**.|  
||**0x1000000000**|Converte os UDTs (tipos definidos pelo usuário) Common Language Runtime (CLR) em **varbinary (max)** para que as colunas do tipo UDT possam ser replicadas para os assinantes que estão em execução [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .|  
||**0x2000000000**|Converte o tipo de dados **hierarchyid** em **varbinary (max)** para que as colunas do tipo **hierarchyid** possam ser replicadas para os assinantes que estão em execução [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] . Para obter mais informações sobre como usar colunas **hierarchyid** em tabelas replicadas, consulte [hierarchyid &#40;Transact-SQL&#41;](../../t-sql/data-types/hierarchyid-data-type-method-reference.md).|  
||**0x4000000000**|Replica qualquer índice filtrado na tabela. Para obter mais informações sobre índices filtrados, consulte [criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md).|  
||**0x8000000000**|Converte os tipos de dados **geography** e **Geometry** em **varbinary (max)** para que as colunas desses tipos possam ser replicadas para os assinantes que estão em execução [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .|  
||**0x10000000000**|Replica índices em colunas do tipo **geography** e **Geometry**.|  
||NULO|O sistema gera automaticamente uma opção de esquema válida para o artigo.|  
|**status**|**active**|O script de processamento inicial para publicação da tabela é executado.|  
||**unsynced**|O script de processamento inicial para publicar a tabela é executado da próxima vez que o Snapshot Agent é executado.|  
|**stream_blob_columns**|**true**|Uma otimização de fluxo de dados é usada ao replicar colunas de objeto binário grande. Porém, certas funcionalidades de replicação de mesclagem, como registros lógicos, ainda podem impedir que a otimização de fluxo seja usada. *stream_blob_columns* é definido como true quando o FileStream está habilitado. Isso permite a replicação de dados FILESTREAM para executar da maneira ideal e reduzir a utilização de memória. Para forçar os artigos da tabela FILESTREAM a não usarem o streaming de BLOB, defina *stream_blob_columns* como false.<br /><br /> Importante a habilitação dessa otimização de memória pode prejudicar o desempenho do agente de mesclagem durante a sincronização. ** \* \* \* \* ** Esta opção só deve ser usada ao replicar colunas que contêm megabytes de dados.|  
||**false**|A otimização não é usada ao replicar colunas de objeto binário grande.|  
|**subscriber_upload_options**|**0**|Nenhuma restrição em atualizações feitas em um Assinante com uma assinatura de cliente. As alterações são carregadas no Publicador. A alteração dessa propriedade pode exigir a reinicialização dos Assinantes existentes.|  
||**1**|Alterações são permitidas em um Assinante com assinatura de cliente, mas elas não são carregadas no Publicador.|  
||**2**|Não são permitidas alterações em um Assinante com uma assinatura de cliente.|  
|**subset_filterclause**||Cláusula WHERE especificando filtragem horizontal. Aplica-se somente a um artigo de tabela.<br /><br /> Importante por motivos de desempenho, recomendamos que você não aplique funções a nomes de colunas em cláusulas de filtro de linha com parâmetros, como. ** \* \* \* \* ** `LEFT([MyColumn]) = SUSER_SNAME()` Se você usar [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) em uma cláusula de filtro e substituir o valor de HOST_NAME, talvez seja necessário converter os tipos de dados usando [converter](../../t-sql/functions/cast-and-convert-transact-sql.md). Para obter mais informações sobre as práticas recomendadas para esse caso, consulte a seção "substituindo o valor de HOST_NAME ()" em [filtros de linha com parâmetros](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).|  
|**threshold**||Valor percentual usado para assinantes que executam o [!INCLUDE[ssEW](../../includes/ssew-md.md)] ou versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . controles de **limite** quando o agente de mesclagem atribui um novo intervalo de identidade. Quando a porcentagem de valores especificada no limite é usada, o Merge Agent cria um novo intervalo de identidade. Usado quando **identityrangemanagementoption** é definido como **auto** ou **auto_identity_range** é definido como **true**. Aplica-se apenas a um artigo de tabela. Para obter mais informações, consulte a seção "replicação de mesclagem" de [replicar colunas de identidade](../../relational-databases/replication/publish/replicate-identity-columns.md).|  
|**verify_resolver_signature**|**1**|A assinatura digital em um resolvedor personalizado é verificada para determinar se é de uma fonte confiável.|  
||**0**|A assinatura digital em um resolvedor personalizado não é verificada para determinar se é de uma fonte confiável.|  
|NULL (padrão)||Retorna a lista de valores com suporte para a *Propriedade*.|  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`O reconhece que a ação executada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de **0**.  
  
 **0** especifica que as alterações no artigo de mesclagem não fazem com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração requer um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** significa que as alterações no artigo de mesclagem podem fazer com que o instantâneo seja inválido e, se houver assinaturas existentes que exijam um novo instantâneo, dará permissão para que o instantâneo existente seja marcado como obsoleto e um novo instantâneo gerado.  
  
 Consulte a seção Comentários das propriedades que, quando alteradas, requerem a geração de um novo instantâneo.  
  
`[ @force_reinit_subscription = ] force_reinit_subscription`Reconhece que a ação executada por este procedimento armazenado pode exigir que as assinaturas existentes sejam reinicializadas. *force_reinit_subscription* é um **bit**, com um padrão de **0**.  
  
 **0** especifica que as alterações no artigo de mesclagem não fazem com que a assinatura seja reinicializada. Se o procedimento armazenado detectar que a alteração irá requerer assinaturas existentes para ser reiniciada, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** significa que as alterações no artigo de mesclagem fazem com que as assinaturas existentes sejam reinicializadas e concede a permissão para que a reinicialização da assinatura ocorra.  
  
 Consulte a seção Comentários para as propriedades que, quando alteradas, requerem que todas as assinaturas existentes sejam reiniciadas.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_changemergearticle** é usado na replicação de mesclagem.  
  
 Como **sp_changemergearticle** é usado para alterar as propriedades do artigo que foram especificadas inicialmente usando [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), consulte [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) para obter informações adicionais sobre essas propriedades.  
  
 A alteração das propriedades a seguir requer que um novo instantâneo seja gerado, e você deve especificar um valor de **1** para o parâmetro *force_invalidate_snapshot* :  
  
-   **check_permissions**  
  
-   **column_tracking**  
  
-   **destination_owner**  
  
-   **pre_creation_command**  
  
-   **schema_options**  
  
-   **subset_filterclause**  
  
 A alteração das propriedades a seguir exige que as assinaturas existentes sejam reinicializadas e você deve especificar um valor de **1** para o parâmetro *force_reinit_subscription* :  
  
-   **check_permissions**  
  
-   **column_tracking**  
  
-   **destination_owner**  
  
-   **pre_creation_command**  
  
-   **identityrangemanagementoption**  
  
-   **subscriber_upload_options**  
  
-   **subset_filterclause**  
  
-   **creation_script**  
  
-   **schema_option**  
  
-   **logical_record_level_conflict_detection**  
  
-   **logical_record_level_conflict_resolution**  
  
 Ao especificar um valor de 3 para **partition_options**, os metadados são limpos sempre que o agente de mesclagem é executado e o instantâneo particionado expira mais rapidamente. Ao usar essa opção, considere habilitar o instantâneo particionado solicitado pelo assinante. Para obter mais informações, consulte [Snapshots for Merge Publications with Parameterized Filters](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md).  
  
 Ao definir a propriedade **column_tracking** , se a tabela já estiver publicada em outras publicações de mesclagem, o rastreamento de coluna deverá ser o mesmo que o valor que está sendo usado por artigos existentes com base nesta tabela. Esse parâmetro só é específico a artigos de tabela.  
  
 Se várias publicações publicarem artigos com base na mesma tabela subjacente, alterar a propriedade **delete_tracking** ou a propriedade **compensate_for_errors** de um artigo fará com que a mesma alteração seja feita nos outros artigos baseados na mesma tabela.  
  
 Se o logon/conta de usuário do Publicador usado pelo processo de mesclagem não possuir as permissões corretas de tabela, as alterações inválidas serão registradas como conflitos.  
  
 Ao alterar o valor de **schema_option**, o sistema não executa uma atualização de bit de bits. Isso significa que, quando você definir **schema_option** usando **sp_changemergearticle**, as configurações de bits existentes poderão ser desativadas. Para manter as configurações existentes, você deve executar [& (AND e)](../../t-sql/language-elements/bitwise-and-transact-sql.md) entre o valor que está definindo e o valor atual de *schema_option*, que pode ser determinado executando [sp_helpmergearticle](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md).  
  
> [!CAUTION]  
>  Quando muitas (talvez centenas) de artigos em uma publicação e você executa **sp_changemergearticle** para um dos artigos, pode levar muito tempo para concluir a execução.  
  
## <a name="valid-schema-option-table"></a>Tabela de opção de esquema válida  
 A tabela a seguir descreve os valores de *schema_option*permitidos, dependendo do tipo de artigo.  
  
|Tipo de artigo|Valores de opção de esquema|  
|------------------|--------------------------|  
|**func schema only**|**0x01** e **0x2000**|  
|**indexed view schema only**|**0x01**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x1000000**e **0x200000**|  
|**proc schema only**|**0x01** e **0x2000**|  
|**table**|Todas as opções.|  
|**view schema only**|**0x01**, **0x040**, **0x0100**, **0x2000**, **0x40000**, **0x1000000**e **0x200000**|  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_changemergearticle](../../relational-databases/replication/codesnippet/tsql/sp-changemergearticle-tr_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_changemergearticle**.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar propriedades do artigo](../../relational-databases/replication/publish/view-and-modify-article-properties.md)   
 [Alterar propriedades da publicação e do artigo](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [&#41;&#40;Transact-SQL de sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropmergearticle](../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpmergearticle](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
