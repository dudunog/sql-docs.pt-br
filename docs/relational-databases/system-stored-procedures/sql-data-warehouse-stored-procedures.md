---
description: Procedimentos armazenados do Azure Synapse Analytics
title: Procedimentos armazenados do Azure Synapse Analytics
ms.custom: ''
ms.date: 03/15/2017
ms.service: sql-data-warehouse
ms.subservice: design
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 02e04dfe-d565-4e45-b427-b8e89c958ba3
author: ronortloff
ms.author: rortloff
monikerRange: = azure-sqldw-latest
ms.openlocfilehash: 1ee858953867209a6686f1775c17e539d13aae2f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97410002"
---
# <a name="azure-synapse-analytics-stored-procedures"></a>Procedimentos armazenados do Azure Synapse Analytics
[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

  [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] fornece procedimentos internos que você pode usar para executar operações relacionadas a funções de banco de dados. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] inclui os seguintes procedimentos de sistema:  
  
<a name="AggregateFunctions"></a>[sp_datatype_info_90 &#40;o Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-datatype-info-90-sql-data-warehouse.md)  
  
 [sp_pdw_add_network_credentials &#40;o Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-add-network-credentials-sql-data-warehouse.md)  
  
 [sp_pdw_database_encryption &#40;o Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-sql-data-warehouse.md)  
  
 [sp_pdw_database_encryption_regenerate_system_keys &#40;o Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-database-encryption-regenerate-system-keys-sql-data-warehouse.md)  
  
 [sp_pdw_log_user_data_masking &#40;o Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-log-user-data-masking-sql-data-warehouse.md)  
  
 [sp_pdw_remove_network_credentials &#40;o Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-pdw-remove-network-credentials-sql-data-warehouse.md)  
  
 [sp_special_columns_100 &#40;o Azure Synapse Analytics&#41;](../../relational-databases/system-stored-procedures/sp-special-columns-100-sql-data-warehouse.md)  
  
> [!NOTE]  
>  Alguns procedimentos armazenados adicionais do sistema são usados somente dentro de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou por meio de APIs de cliente e não se destinam a uso geral do cliente. Esses procedimentos estão listados em [procedimentos armazenados do sistema (Transact-SQL)](./system-stored-procedures-transact-sql.md). Esses procedimentos estão sujeitos a alterações e a compatibilidade não é garantida. Todos os procedimentos da lista não estão disponíveis no [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Funções armazenadas do sistema &#40;&#41;Transact-SQL ](~/relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
