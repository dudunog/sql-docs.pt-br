---
description: Exibições de catálogo Controle de Alterações-sys.change_tracking_databases
title: sys.change_tracking_databases (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- change_tracking_databases
- sys.change_tracking_databases_TSQL
- sys.change_tracking_databases
- change_tracking_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.change_tracking_databases
- change tracking [SQL Server], sys.change_tracking_databases
ms.assetid: bb233baa-2991-4904-a0eb-3772b81121a4
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5a4122bb16ea7fced5acb078f28f8b11c37c54c5
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98093241"
---
# <a name="change-tracking-catalog-views---syschange_tracking_databases"></a>Exibições de catálogo Controle de Alterações-sys.change_tracking_databases
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna uma linha para cada banco de dados com o controle de alterações habilitado.  

|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID do banco de dados. Exclusivo na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|is_auto_cleanup_on|**bit**|Indica se os dados do controle de alterações devem ser limpos automaticamente após o período de retenção configurado:<br /><br /> 0 = Desativado<br /><br /> 1 = Ativado|  
|retention_period|**int**|Se a limpeza automática estiver sendo usada, o período de retenção especificará por quanto tempo os dados de controle de alterações serão mantidos no banco de dados.|  
|retention_period_units_desc|**nvarchar(60)**|Especifica a descrição do período de retenção:<br /><br /> minutos<br /><br /> Horas<br /><br /> Dias|  
|retention_period_units|**tinyint**|Unidade de tempo do período de retenção:<br /><br /> 1 = Minutos<br /><br /> 2 = Horas<br /><br /> 3 = Dias|  
  
## <a name="permissions"></a>Permissões  
 As mesmas verificações de permissão são feitas para sys.change_tracking_databases e para sys.databases. Se o chamador sys.change_tracking_databases não for o proprietário do banco de dados, as permissões mínimas necessárias para verificar a linha correspondente serão ALTER ANY DATABASE ou VIEW ANY DATABASE em nível de servidor ou CREATE DATABASE no banco de dados mestre ou atual.  
  
## <a name="see-also"></a>Consulte Também  
 [Controle de Alterações exibições de catálogo &#40;Transact-SQL&#41;](./catalog-views-transact-sql.md)   
 [Controle de alterações de dados &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
