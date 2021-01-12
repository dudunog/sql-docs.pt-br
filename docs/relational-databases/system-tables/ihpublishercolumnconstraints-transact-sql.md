---
description: IHpublishercolumnconstraints (Transact-SQL)
title: IHpublishercolumnconstraints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishercolumnconstraints
- IHpublishercolumnconstraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumnconstraints system table
ms.assetid: d7a41da6-e067-430a-8da2-3f6745b8a4f3
author: cawrites
ms.author: chadam
ms.openlocfilehash: 8f82d650cc09c7379c9ad9256413229143be4cdf
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98092476"
---
# <a name="ihpublishercolumnconstraints-transact-sql"></a>IHpublishercolumnconstraints (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela do sistema **IHpublishercolumnconstraints** mapeia colunas de uma publicação não SQL Server na tabela do sistema [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) para restrições na tabela do sistema [IHpublisherconstraints](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md) . Esta tabela é armazenada no banco de dados de distribuição.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|Identifica a coluna de [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) com uma restrição associada.|  
|**publisherconstraint_id**|**int**|Identifica uma restrição de [IHpublisherconstraints](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md) associada à coluna.|  
|**indid**|**int**|Indica posição da coluna na tabela publicada.|  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
