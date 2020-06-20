---
title: Alterar propriedades da publicação e do artigo | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- modifying article properties
- modifying publication properties
- administering replication, properties
- publications [SQL Server replication], changing properties
- articles [SQL Server replication], properties
ms.assetid: f7df51ef-c088-4efc-b247-f91fb2c6ff32
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 185e5d0beb9df2ec8a3dcf263632c1d260a3bcd7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85038059"
---
# <a name="change-publication-and-article-properties"></a>Alterar propriedades da publicação e do artigo
  Depois que uma publicação foi criada, a maior parte das propriedades de publicação e do artigo podem ser alteradas, mas algumas requerem que um novo instantâneo seja gerado e/ou que as assinaturas sejam reinicializadas. Este tópico fornece informações sobre todas as propriedades que requerem uma ou ambas as ações, se forem alteradas.  
  
## <a name="publication-properties-for-snapshot-and-transactional-replication"></a>Propriedades de uma publicação de instantâneo ou de replicação transacional  
  
|DESCRIÇÃO|Procedimento armazenado|Propriedades|Requisitos|  
|-----------------|----------------------|----------------|------------------|  
|Alterar o formato de instantâneo.|**sp_changepublication**|**sync_method**|Novo instantâneo.|  
|Alterar o local do instantâneo.|**sp_changepublication**|**alt_snapshot_folder**<br /><br /> **snapshot_in_defaultfolder**|Novo instantâneo.|  
|Alterar o local do instantâneo.|**sp_changedistpublisher**|**working_directory**|Novo instantâneo.|  
|Alterar a compactação de instantâneo.|**sp_changepublication**|**compress_snapshot**|Novo instantâneo.|  
|Alterar qualquer opção de instantâneo de FTP (File Transfer Protocol).|**sp_changepublication**|**enabled_for_internet**<br /><br /> **ftp_address**<br /><br /> **ftp_login**<br /><br /> **ftp_password**<br /><br /> **ftp_port**<br /><br /> **ftp_subdirectory**|Novo instantâneo.|  
|Alterar localização do script pré ou pós-instantâneo.|**sp_changepublication**|**pre_snapshot_script**<br /><br /> **post_snapshot_script**|Novo instantâneo (também é necessário se você alterar os conteúdos de script).<br /><br /> A reinicialização é necessária para aplicar o script novo ao Assinante.|  
|Habilitar ou desabilitar o suporte para assinantes não [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|**sp_changepublication**|**is_enabled_for_het_sub**|Novo instantâneo.|  
|Alterar relatórios conflitantes para assinaturas de atualização em fila|**sp_changepublication**|**centralized_conflicts**|Só poderá ser alterado se não houver nenhuma assinatura ativa.|  
|Alterar a política de resolução de conflito para as assinaturas de atualização em fila.|**sp_changepublication**|**conflict_policy**|Só poderá ser alterado se não houver nenhuma assinatura ativa.|  
  
## <a name="article-properties-for-snapshot-and-transactional-replication"></a>Propriedades de um artigo para instantâneo e replicação transacional  
  
|DESCRIÇÃO|Procedimento armazenado|Propriedades|Requisitos|  
|-----------------|----------------------|----------------|------------------|  
|Descartar um artigo|**sp_droparticle**|Todos os parâmetros.|Os artigos podem ser descartados antes que as assinaturas sejam criadas. Com os procedimentos armazenados, é possível descartar uma assinatura de um artigo, usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], a assinatura inteira deve ser descartada, recriada e sincronizada. Para obter mais informações, consulte [Add Articles to and Drop Articles from Existing Publications](add-articles-to-and-drop-articles-from-existing-publications.md) (Adicionar e remover artigos para/de publicações existentes).|  
|Alterar um filtro de coluna.|**sp_articlecolumn**|**\@pilha**<br /><br /> **\@operacional**|Novo instantâneo.<br /><br /> Reinicialize as assinaturas.|  
|Adicionar um filtro de linha.|**sp_articlefilter**|Todos os parâmetros.|Novo instantâneo.<br /><br /> Reinicialize as assinaturas.|  
|Descartar um filtro de linha.|**sp_articlefilter**|**\@artigo**|Novo instantâneo.<br /><br /> Reinicialize as assinaturas.|  
|Alterar um filtro de linha.|**sp_articlefilter**|**\@filter_clause**|Novo instantâneo.<br /><br /> Reinicialize as assinaturas.|  
|Alterar um filtro de linha.|**sp_changearticle**|**sem**|Novo instantâneo.<br /><br /> Reinicialize as assinaturas.|  
|Alterar opções de esquema.|**sp_changearticle**|**schema_option**|Novo instantâneo.|  
|Alterar como as tabelas são controladas no Assinante antes de aplicar o instantâneo.|**sp_changearticle**|**pre_creation_cmd**|Novo instantâneo.|  
|Alterar o status de artigo|**sp_changearticle**|**status**|Novo instantâneo.|  
|Alterar os comandos INSERT, UPDATE ou DELETE.|**sp_changearticle**|**ins_cmd**<br /><br /> **upd_cmd**<br /><br /> **del_cmd**|Novo instantâneo.<br /><br /> Reinicialize as assinaturas.|  
|Alterar o nome da tabela de destino|**sp_changearticle**|**dest_table**|Novo instantâneo.<br /><br /> Reinicialize as assinaturas.|  
|Alterar o proprietário da tabela de destino (esquema).|**sp_changearticle**|**destination_owner**|Novo instantâneo.<br /><br /> Reinicialize as assinaturas.|  
|Alterar os mapeamentos de tipo de dados (aplica-se somente à edição com o Oracle).|**sp_changearticlecolumndatatype**|**\@tipo**<br /><br /> **\@muito**<br /><br /> **\@Preciso**<br /><br /> **\@escalonáve**|Novo instantâneo.<br /><br /> Reinicialize as assinaturas.|  
  
## <a name="publication-properties-for-merge-replication"></a>Propriedades de publicação para a replicação de mesclagem  
  
|Descrição|Procedimento armazenado|Propriedades|Requisitos|  
|-----------------|----------------------|----------------|------------------|  
|Alterar o formato de instantâneo|**sp_changemergepublication**|**sync_mode**|Novo instantâneo.|  
|Alterar o local do instantâneo.|**sp_changemergepublication**|**alt_snapshot_folder**<br /><br /> **snapshot_in_defaultfolder**|Novo instantâneo.|  
|Alterar o local do instantâneo.|**sp_changedistpublisher**|**working_directory**|Novo instantâneo.|  
|Alterar a compactação de instantâneo.|**sp_changemergepublication**|**compress_snapshot**|Novo instantâneo.|  
|Alterar qualquer opção de instantâneo de FTP|**sp_changemergepublication**|**enabled_for_internet**<br /><br /> **ftp_address**<br /><br /> **ftp_login**<br /><br /> **ftp_password**<br /><br /> **ftp_port**<br /><br /> **ftp_subdirectory**|Novo instantâneo.|  
|Alterar scripts pré ou pós-instantâneo.|**sp_changemergepublication**|**pre_snapshot_script**<br /><br /> **post_snapshot_script**|Novo instantâneo (também é necessário se você alterar os conteúdos de script).<br /><br /> A reinicialização é necessária para aplicar o script novo ao Assinante.|  
|Adicionar um filtro de junção ou um registro lógico.|**sp_addmergefilter**|Todos os parâmetros.|Novo instantâneo.<br /><br /> Reinicialize as assinaturas.|  
|Descartar um filtro de junção ou um registro lógico.|**sp_dropmergefilter**|Todos os parâmetros.|Novo instantâneo.<br /><br /> Reinicialize as assinaturas.|  
|Alterar um filtro de junção ou registro lógico.|**sp_changemergefilter**|**\@Propriedade**<br /><br /> **\@valor**|Novo instantâneo<br /><br /> Reinicialize as assinaturas.|  
|Desabilitar o uso de filtros com parâmetros (habilitar os filtros com parâmetros não requer nenhuma ação especial).|**sp_changemergepublication**|Um valor **false** para **dynamic_filters**|Novo instantâneo.<br /><br /> Reinicialize as assinaturas.|  
|Ativar ou desabilitar o uso de partições pré-computadas.|**sp_changemergepublication**|**use_partition_groups**|Novo instantâneo.|  
|Habilitar ou desabilitar a [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)] otimização de partição.|**sp_changemergepublication**|**keep_partition_changes**|Reinicialize as assinaturas.|  
|Ativar ou desabilitar a validação de partição do Assinante.|**sp_changemergepublication**|**validate_subscriber_info**|Reinicialize as assinaturas.|  
|Altere o nível de compatibilidade de publicação para 80sp3 ou menos.|**sp_changemergepublication**|**publication_compatibility_level**|Novo instantâneo.|  
  
## <a name="article-properties-for-merge-replication"></a>Propriedades do artigo para replicação de mesclagem  
  
|Descrição|Procedimento armazenado|Propriedades|Requisitos|  
|-----------------|----------------------|----------------|------------------|  
|Descartar um artigo, quando o artigo tem o último filtro com parâmetros na publicação.|**sp_dropmergearticle**|Todos os parâmetros|Novo instantâneo.<br /><br /> Reinicialize as assinaturas.|  
|Descartar um artigo, quando é um artigo pai em um filtro de junção ou em um registro lógico (isso tem como efeito colateral o descarte da junção).|**sp_dropmergearticle**|Todos os parâmetros|Novo instantâneo.<br /><br /> Reinicialize as assinaturas.|  
|Descartar um artigo, todas as outras circunstâncias.|**sp_dropmergearticle**|Todos os parâmetros|Novo instantâneo.|  
|Incluir um filtro de coluna que não foi publicado anteriormente.|**sp_mergearticlecolumn**|**\@pilha**<br /><br /> **\@operacional**|Novo instantâneo.<br /><br /> Reinicialize as assinaturas.|  
|Adicionar, descartar ou alterar um filtro de linha.|**sp_changemergearticle**|**subset_filterclause**|Novo instantâneo.<br /><br /> Reinicialize as assinaturas.<br /><br /> Se você adicionar, descartar ou alterar um filtro com parâmetros, as alterações pendentes no Assinante não poderão ser carregadas no Publicador durante a reinicialização. Para carregar alterações pendentes, sincronize todas as assinaturas antes de alterar o filtro.<br /><br /> Se um artigo não estiver envolvido em um filtro de junção, você poderá descartar o artigo e adicioná-lo novamente, com um filtro de linha diferente, não é necessário reinicializar a assinatura inteira. Para obter mais informações sobre como adicionar e remover artigos, consulte [Add Articles to and Drop Articles from Existing Publications](add-articles-to-and-drop-articles-from-existing-publications.md) (Adicionar e remover artigos para/de publicações existentes).|  
|Alterar opções de esquema.|**sp_changemergearticle**|**schema_option**|Novo instantâneo.|  
|Controlar as alterações do nível de coluna para o nível de linha (alterar o controle do nível de linha para controle do nível de coluna não requer nenhuma ação especial).|**sp_changemergearticle**|Um valor **false** para **column_tracking**|Novo instantâneo.<br /><br /> Reinicialize as assinaturas.|  
|Alterar se as permissões são verificadas antes que as instruções realizadas no Assinante sejam aplicadas ao Publicador.|**sp_changemergearticle**|**check_permissions**|Novo instantâneo.<br /><br /> Reinicialize as assinaturas.|  
|Habilitar ou desabilitar assinaturas de somente download (alterar para ou de outras opções de carregamento não requer nenhuma ação especial).|**sp_changemergearticle**|Alterar para ou de um valor **2** para **subscriber_upload_options**|Reinicialize as assinaturas.|  
|Alterar o proprietário da tabela de destino.|**sp_changemergearticle**|**destination_owner**|Novo instantâneo.<br /><br /> Reinicialize as assinaturas.|  
  
## <a name="see-also"></a>Consulte Também  
 [Perguntas frequentes sobre administração de replicação](../administration/frequently-asked-questions-for-replication-administrators.md)   
 [Criar e aplicar o instantâneo](../create-and-apply-the-snapshot.md)   
 [Reinicializar assinaturas](../reinitialize-subscriptions.md)   
 [&#41;&#40;Transact-SQL de sp_addmergefilter](/sql/relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_articlecolumn](/sql/relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_articlefilter](/sql/relational-databases/system-stored-procedures/sp-articlefilter-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_changearticlecolumndatatype](/sql/relational-databases/system-stored-procedures/sp-changearticlecolumndatatype-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_changedistpublisher](/sql/relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_changemergefilter](/sql/relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_droparticle](/sql/relational-databases/system-stored-procedures/sp-droparticle-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_dropmergearticle](/sql/relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql)   
 [&#41;&#40;Transact-SQL de sp_dropmergefilter](/sql/relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql)   
 [sp_mergearticlecolumn &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql)  
  
  
