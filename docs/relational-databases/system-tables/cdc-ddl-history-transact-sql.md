---
description: cdc.ddl_history (Transact-SQL)
title: cdc.ddl_history (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- cdc.ddl_history_TSQL
- cdc.ddl_history
dev_langs:
- TSQL
helpviewer_keywords:
- cdc.ddl_history
ms.assetid: cb97ea71-da2f-441a-bbd2-db1f5f48ab49
author: cawrites
ms.author: chadam
ms.openlocfilehash: 7536929659cf4c1c329116a27ab456efc0d9e5e0
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98094914"
---
# <a name="cdcddl_history-transact-sql"></a>cdc.ddl_history (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma linha para cada alteração de linguagem de definição de dados (DDL) feita nas tabelas que estão habilitadas para captura de dados de alteração. Você pode usar esta tabela para determinar quando uma alteração de DDL ocorre em uma tabela de origem e qual foi a alteração. As tabelas de origem que não tiverem tido alterações de DDL não terão entradas nesta tabela.  
  
 É recomendável não consultar diretamente as tabelas do sistema. Em vez disso, execute o procedimento armazenado [Sys.sp_cdc_get_ddl_history](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md) .  
   
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**source_object_id**|**int**|A identificação da tabela de origem na qual a DDL foi aplicada.|  
|**object_id**|**int**|ID da tabela de alteração associada a uma instância de captura da tabela de origem.|  
|**required_column_update**|**bit**|Indica que o tipo de dados de uma coluna capturada foi modificado na tabela de origem. Esta modificação alterou a coluna na tabela de alteração.|  
|**ddl_command**|**nvarchar(max)**|Instrução DDL aplicada à tabela de origem.|  
|**ddl_lsn**|**binary(10)**|Número de sequência de log (LSN) associado com a confirmação da modificação de DDL.|  
|**ddl_time**|**datetime**|Data e hora em que a alteração de DDL foi feita na tabela de origem.|  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sys.sp_cdc_help_change_data_capture ](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
