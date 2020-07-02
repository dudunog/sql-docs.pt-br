---
title: sysarticles (exibição do sistema) (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticles
- sysarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticles view
ms.assetid: 18f8c9b3-cab7-4e8f-8754-11ac38c3f789
author: stevestein
ms.author: sstein
ms.openlocfilehash: d947bdcf0e777d96c18551fafae61d3db9a930b6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85759983"
---
# <a name="sysarticles-system-view-transact-sql"></a>sysarticles (exibição de sistema) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  A exibição **sysarticles** expõe as propriedades do artigo. Essa exibição é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|A coluna de identidade que fornece um número de ID exclusivo para o artigo.|  
|**creation_script**|**nvarchar (255)**|O script de esquema para o artigo.|  
|**del_cmd**|**nvarchar (255)**|O comando para executar em DELETE; caso contrário, construir do log.|  
|**ndescrição**|**nvarchar (255)**|A entrada descritiva para o artigo.|  
|**dest_table**|**sysname**|O nome da tabela de destino.|  
|**sem**|**int**|A ID do procedimento armazenado, usado para particionamento horizontal.|  
|**filter_clause**|**ntext**|A cláusula WHERE do artigo, usada para filtragem horizontal.|  
|**ins_cmd**|**nvarchar (255)**|O comando para executar em INSERT; caso contrário, construir do log.|  
|**name**|**sysname**|O nome associado ao artigo, exclusivo dentro da publicação.|  
|**objid**|**int**|A ID do objeto de tabela publicada.|  
|**pubid**|**int**|A ID da publicação à qual o artigo pertence.|  
|**pre_creation_cmd**|**tinyint**|O comando de pré-criação para DROP TABLE, DELETE TABLE ou TRUNCATE:<br /><br /> **0** = nenhum.<br /><br /> **1** = descartar.<br /><br /> **2** = excluir.<br /><br /> **3** = truncar.|  
|**status**|**tinyint**|O bitmask de opções e status do artigo, que pode ser o resultado OR lógico bit a bit de um ou mais destes valores:<br /><br /> **1** = o artigo está ativo.<br /><br /> **8** = incluir o nome da coluna em instruções INSERT.<br /><br /> **16** = usar instruções parametrizadas.<br /><br /> **24** = ambos incluem o nome da coluna em instruções INSERT e usam instruções parametrizadas.<br /><br /> **64** = a partição horizontal do artigo é definida por uma assinatura transformável.<br /><br /> Por exemplo, um artigo ativo usando instruções parametrizadas teria um valor de **17** nesta coluna. Um valor de **0** significa que o artigo está inativo e nenhuma propriedade adicional é definida.|  
|**sync_objid**|**int**|A ID da tabela ou exibição que representa a definição de artigo.|  
|**type**|**tinyint**|O tipo de artigo:<br /><br /> **1** = artigo baseado em log.<br /><br /> **3** = artigo baseado em log com filtro manual.<br /><br /> **5** = artigo baseado em log com exibição manual.<br /><br /> **7** = artigo baseado em log com filtro manual e exibição manual.<br /><br /> **8** = execução de procedimento armazenado.<br /><br /> **24** = execução de procedimento armazenado serializável.<br /><br /> **32** = procedimento armazenado (somente esquema).<br /><br /> **64** = exibição (somente esquema).<br /><br /> **128** = função (somente esquema).|  
|**upd_cmd**|**nvarchar (255)**|O comando para executar em UPDATE; caso contrário, construir do log.|  
|**schema_option**|**binário (8)**|Um bitmask das opções de geração de esquema para o artigo, que controla de qual parte do esquema de artigo é feito um script para entrega no Assinante. Para obter mais informações sobre opções de esquema, consulte [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md).|  
|**dest_owner**|**sysname**|O proprietário da tabela no banco de dados de destino.|  
|**ins_scripting_proc**|**int**|O procedimento armazenado personalizado registrado ou script executado quando uma instrução INSERT é replicada.|  
|**del_scripting_proc**|**int**|O procedimento armazenado personalizado registrado ou script executado quando uma instrução DELETE é replicada.|  
|**upd_scripting_proc**|**int**|O procedimento armazenado personalizado registrado ou script executado quando uma instrução UPDATE é replicada.|  
|**custom_script**|**nvarchar(2048)**|O procedimento armazenado personalizado registrado ou script executado ao término do gatilho DDL.|  
|**fire_triggers_on_snapshot**|**bit**|Indica se os gatilhos replicados são executados quando o instantâneo é aplicado, que pode ser um destes valores:<br /><br /> **0** = gatilhos não são executados.<br /><br /> **1** = gatilhos são executados.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changearticle](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helparticle](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [&#41;sysarticles &#40;Transact-SQL](../../relational-databases/system-tables/sysarticles-transact-sql.md)  
  
  
