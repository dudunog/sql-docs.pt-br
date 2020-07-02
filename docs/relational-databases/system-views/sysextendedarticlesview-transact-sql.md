---
title: sysextendedarticlesview (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysextendedarticlesview_TSQL
- sysextendedarticlesview
dev_langs:
- TSQL
helpviewer_keywords:
- sysextendedarticlesview view
ms.assetid: 8bdd22f7-c268-49b6-820c-3fe603feb128
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3c89e15e2a5da3a33afc5641ac9d96c468afb20c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85750124"
---
# <a name="sysextendedarticlesview-transact-sql"></a>sysextendedarticlesview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  A exibição **sysextendedarticlesview** fornece informações sobre artigos publicados. Essa exibição é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|A coluna de identidade que fornece um número de ID exclusivo para o artigo.|  
|**creation_script**|**nvarchar (255)**|O script de criação de esquema para o artigo.|  
|**del_cmd**|**nvarchar (255)**|O comando para executar em DELETE; caso contrário, construir do log.|  
|**ndescrição**|**nvarchar (255)**|A entrada descritiva para o artigo.|  
|**dest_table**|**nvarchar(128)**|O nome da tabela de destino.|  
|**sem**|**int**|O identificador de objeto do procedimento armazenado usado para particionamento horizontal.|  
|**filter_clause**|**ntext**|A cláusula WHERE do artigo, usada para filtragem horizontal.|  
|**ins_cmd**|**nvarchar (255)**|O comando para executar em INSERT.|  
|**name**|**nvarchar(128)**|O nome associado ao artigo, exclusivo dentro da publicação.|  
|**objid**|**int**|A ID do objeto de tabela publicada.|  
|**pubid**|**int**|A ID da publicação à qual o artigo pertence.|  
|**pre_creation_cmd**|**tinyint**|O comando de pré-criação para DROP TABLE, DELETE TABLE ou TRUNCATE:<br /><br /> **0** = nenhum.<br /><br /> **1** = descartar.<br /><br /> **2** = excluir.<br /><br /> **3** = truncar.|  
|**status**|**int**|O bitmask de opções e status do artigo, que pode ser o resultado OR lógico bit a bit de um ou mais destes valores:<br /><br /> **1** = o artigo está ativo.<br /><br /> **8** = incluir o nome da coluna em instruções INSERT.<br /><br /> **16** = usar instruções parametrizadas.<br /><br /> **24** = ambos incluem o nome da coluna em instruções INSERT e usam instruções parametrizadas.<br /><br /> Por exemplo, um artigo ativo que usa instruções com parâmetros teria um valor 17 nessa coluna. Um valor 0 significa que o artigo está inativo e nenhuma propriedade adicional está definida.|  
|**sync_objid**|**int**|A ID da tabela ou exibição que representa a definição de artigo.|  
|**type**|**tinyint**|O tipo de artigo:<br /><br /> **1** = artigo baseado em log.<br /><br /> **3** = artigo baseado em log com filtro manual.<br /><br /> **5** = artigo baseado em log com exibição manual.<br /><br /> **7** = artigo baseado em log com filtro manual e exibição manual.|  
|**upd_cmd**|**nvarchar (255)**|O comando para executar em UPDATE; caso contrário, construir do log.|  
|**schema_option**|**binary**|Indica de quais propriedades do objeto publicado foram efetuados scripts no instantâneo. Para obter uma lista de opções de esquema com suporte, consulte [sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).|  
|**dest_owner**|**nvarchar(128)**|O proprietário da tabela no banco de dados de destino.|  
|**ins_scripting_proc**|**int**|O identificador de objeto do procedimento armazenado personalizado ou script executados quando uma instrução INSERT é replicada.|  
|**del_scripting_proc**|**int**|O identificador de objeto do procedimento armazenado personalizado ou script executados quando uma instrução DELETE é replicada.|  
|**upd_scripting_proc**|**int**|O identificador de objeto do procedimento armazenado personalizado ou script executados quando uma instrução UPDATE é replicada.|  
|**custom_script**|**int**|O identificador de objeto do script personalizado ou procedimento executados na conclusão de um gatilho DDL.|  
|**fire_triggers_on_snapshot**|**int**|Indica se os gatilhos replicados são executados quando o instantâneo é aplicado, que pode ser um destes valores:<br /><br /> **0** = gatilhos não são executados.<br /><br /> **1** = gatilhos são executados.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changearticle](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helparticle](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [&#41;sysarticles &#40;Transact-SQL](../../relational-databases/system-tables/sysarticles-transact-sql.md)  
  
  
