---
description: MSmerge_genhistory (Transact-SQL)
title: MSmerge_genhistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_genhistory_TSQL
- MSmerge_genhistory
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_genhistory system table
ms.assetid: 475d08ae-eb8b-49de-afd6-33c96ab8004d
author: cawrites
ms.author: chadam
ms.openlocfilehash: 7ccd9f9b6cc2780681f1f76c0764aaf423c2af36
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98100550"
---
# <a name="msmerge_genhistory-transact-sql"></a>MSmerge_genhistory (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSmerge_genhistory** contém uma linha para cada geração que um assinante conhece (dentro do período de retenção). Ela é usada para evitar enviar gerações comuns durante trocas e para sincronizar novamente Assinantes restaurados de backups. Essa tabela é armazenada nos bancos de dados de publicação e de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**guidsrc**|**uniqueidentifier**|O identificador global das alterações identificadas pela geração no Assinante.|  
|**pubid**|**uniqueidentifier**|O identificador da publicação.|  
|**geração**|**bigint**|O valor de geração.|  
|**art_nick**|**int**|O apelido do artigo.|  
|**nicknames**|**varbinary (1001)**|Uma lista de apelidos de outros Assinantes que já têm essa geração. É usado para evitar enviar uma geração a um Assinante que já viu essas alterações. Apelidos da lista de apelidos são mantidos em ordem classificada para tornar as pesquisas mais eficientes. Se houver mais apelidos do que o que cabe nesse campo, eles não se beneficiarão dessa otimização.|  
|**coldate**|**datetime**|Data em que a geração atual é adicionada à tabela.|  
|**genstatus**|**tinyint**|O status da geração como segue:<br /><br /> **0** = abrir.<br /><br /> **1** = fechado.<br /><br /> **2** = fechado e originado em outro Assinante.|  
|**changecount**|**int**|O número de alterações refletido em uma determinada geração|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
