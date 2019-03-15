---
title: sys.workload_management_workload_classifiers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/08/2019
ms.prod: ''
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: d93876db1bb31edab2ad128a0ab8af4d4a5230cd
ms.sourcegitcommit: aa8bec762be29a29aed651d98ed4d868da85ba67
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/14/2019
ms.locfileid: "57975360"
---
# <a name="sysworkloadmanagementworkloadclassifiers-transact-sql-preview"></a>sys.workload_management_workload_classifiers (Transact-SQL) (Preview)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

 Retorna detalhes de classificadores de carga de trabalho.  
  
|Nome da coluna|Tipo de Dados|Descrição|Intervalo|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|ID exclusiva do classificador. Não permite valor nulo||
group_name|**sysname**|Nome do grupo de carga de trabalho, a que o classificador é atribuído. Não permite valor nulo. |Classes de recursos estáticos</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80 </br>Classes de recursos dinâmicos</br>smallrc</br>mediumrc</br>Largerc</br>xlargerc|
nome|**sysname**|Nome do classificador. Deve ser exclusivo para a instância. Não permite valor nulo.||
|importance|**sysname**|É a importância relativa de uma solicitação neste grupo de carga de trabalho e em grupos de carga de trabalho para recursos compartilhados.  Importância especificada no classificador substitui a configuração de importância do grupo de carga de trabalho.|baixa, below_normal, normal, above_normal, alto |
|create_time|**datetime**|Hora em que o classificador foi criado. Não permite valor nulo.||
modify_time|**datetime**|Tempo de que classificador foi modificado pela última vez. Não permite valor nulo.||
is_enabled|**bit**|Exibe se a classificação está habilitada ou não. É habilitado por padrão. Não permite valor nulo.|0 = o classificador não está habilitado. </br> 1 = o classificador está habilitado|
|&nbsp;||||
  
## <a name="permissions"></a>Permissões

Requer a permissão VIEW SERVER STAT.

## <a name="next-steps"></a>Próximas etapas

 Para obter uma lista de todas as exibições de catálogo para o SQL Data Warehouse e Parallel Data Warehouse, consulte [SQL Data Warehouse e exibições do catálogo Parallel Data Warehouse](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md). Para criar um classificador de carga de trabalho, consulte [CLASSIFICADOR de carga de trabalho criar](../../t-sql/statements/create-workload-classifier-transact-sql.md). Para obter mais informações sobre a classificação de carga de trabalho consulte [classificação de carga de trabalho do SQL DATA Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)