---
description: MSmerge_settingshistory (Transact-SQL)
title: MSmerge_settingshistory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSmerge_settingshistory
- MSmerge_settingshistory_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_settingshistory system table
ms.assetid: 0bdf2d5f-5502-44cd-aa9d-2d5006ad20ce
author: cawrites
ms.author: chadam
ms.openlocfilehash: 10beb9d65bba15ef0b21acd2242fcbaf1d515dca
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98098574"
---
# <a name="msmerge_settingshistory-transact-sql"></a>MSmerge_settingshistory (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **MSmerge_settingshistory** é usada para manter um histórico das alterações feitas nas propriedades do artigo e da publicação para replicação de mesclagem, com uma linha para cada alteração feita em uma topologia de replicação de mesclagem. Essa tabela também armazena informações sobre quando as configurações de propriedade iniciais foram feitas. Essa tabela é armazenada nos bancos de dados de publicação e de assinatura.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**EventTime**|**datetime**|A data e hora em que o evento ocorreu.|  
|**pubid**|**uniqueidentifier**|O número de identificação exclusivo de determinada publicação.|  
|**artid**|**uniqueidentifier**|O número de identificação exclusivo para o artigo determinado.|  
|**EventType**|**tinyint**|Especifica o tipo de evento que está sendo registrado, que pode ser um dos seguintes:<br /><br /> **1** -configuração de propriedade de nível de publicação inicial.<br /><br /> **2** -alterar em uma propriedade de publicação.<br /><br /> **101** -configuração da Propriedade do artigo inicial.<br /><br /> **102** -alterar em uma propriedade de artigo.|  
|**propertyname**|**sysname**|O nome da propriedade definida ou alterada|  
|**previousvalue**|**sysname**|O valor da propriedade anterior se uma propriedade tiver sido alterada.|  
|**NewValue**|**sysname**|O valor para o qual a propriedade foi alterada ou no qual ela foi criada.|  
|**eventtext**|**nvarchar (2000)**|A cadeia de caracteres que descreve o evento.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
