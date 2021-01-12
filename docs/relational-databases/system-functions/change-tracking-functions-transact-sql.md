---
description: Funções de controle de alterações (Transact-SQL)
title: Funções de Controle de Alterações (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- functions [SQL Server], change tracking
- change tracking [SQL Server], functions
ms.assetid: 04eb53c4-8b69-414e-9696-185d227fea35
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5fe7ea18e564c177e2d9b113be29ac62c8193508
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98095012"
---
# <a name="change-tracking-functions-transact-sql"></a>Funções de controle de alterações (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Os registros de controle de alterações inserem, atualizam e excluem atividades aplicadas a tabelas controladas, fornecendo detalhes das alterações em um formato relacional facilmente consumido. As seguintes funções retornam informações sobre as alterações.  
  
|Função|Descrição|  
|--------------|-----------------|  
|[CHANGETABLE (ALTERAÇÕES)](../../relational-databases/system-functions/changetable-transact-sql.md)|Retorna informações de controle de todas as alterações efetuadas em uma tabela desde uma versão especificada.|  
|[CHANGETABLE (VERSÃO)](../../relational-databases/system-functions/changetable-transact-sql.md)|Retorna as informações de controle de alterações mais recentes de uma linha especificada.|  
|[CHANGE_TRACKING_MIN_VALID_VERSION ()](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)|Retorna a versão mínima que é válida para uso na obtenção de informações de controle de alterações da tabela especificada quando você estiver usando a função [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md) .|  
|[CHANGE_TRACKING_CURRENT_VERSION](../../relational-databases/system-functions/change-tracking-current-version-transact-sql.md)|Obtém uma versão que está associada à última transação confirmada. Você pode usar essa versão na próxima vez que enumerar as alterações usando o CHANGEtable.|  
|[CHANGE_TRACKING_IS_COLUMN_IN_MASK](../../relational-databases/system-functions/change-tracking-is-column-in-mask-transact-sql.md)|Interpreta o valor SYS_CHANGE_COLUMNS retornado pela função CHANGEtable (CHANGES...).|  
|[WITH CHANGE_TRACKING_CONTEXT](../../relational-databases/system-functions/with-change-tracking-context-transact-sql.md)|Habilita a especificação de um contexto de alteração, como um ID do originador, quando um aplicativo altera os dados.|  
  
## <a name="see-also"></a>Consulte Também  
 [Controle de alterações de dados &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
