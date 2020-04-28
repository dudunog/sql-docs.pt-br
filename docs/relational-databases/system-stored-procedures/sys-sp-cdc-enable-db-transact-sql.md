---
title: sys. sp_cdc_enable_db (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_enable_db_TSQL
- sp_cdc_enable_db
- sys.sp_cdc_enable_db
- sys.sp_cdc_enable_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_enable_db
- change data capture [SQL Server], enabling databases
- sp_cdc_enable_db
ms.assetid: 176d83b3-493d-43cd-800e-aa123c3bdf17
author: rothja
ms.author: jroth
ms.openlocfilehash: 87cb8f207d85220b88ef00d65fd4704b21becf63
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68106500"
---
# <a name="syssp_cdc_enable_db-transact-sql"></a>sys.sp_cdc_enable_db (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Habilita o Change Data Capture para o banco de dados atual. Esse procedimento deve ser executado para um banco de dados antes que qualquer tabela possa ser habilitada para o Change Data Capture nesse banco de dados. O Change Data Capture registra, insere, atualiza, e exclui atividades aplicadas às tabelas habilitadas, disponibilizando os detalhes das alterações em um formato relacional de fácil de consumir. Informações de coluna que espelham a estrutura de coluna de uma tabela de origem rastreada são capturadas para as linhas modificadas, juntamente com os metadados necessários para aplicar as alterações a um ambiente de destino.  
  
> [!IMPORTANT]
>  A captura de dados de alteração não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_cdc_enable_db  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 O Change Data Capture não pode ser habilitado em bancos de dados do [sistema](../../relational-databases/databases/system-databases.md) ou de distribuição.  
  
 O sys.sp_cdc_enable_db cria os objetos do Change Data Capture que têm escopo em todo o banco de dados, inclusive tabelas de metadados e gatilhos DDL. Ele também cria o esquema CDC e o usuário do banco de dados CDC e define a coluna is_cdc_enabled para a entrada do banco de dados na exibição do catálogo [Sys. databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) como 1.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de servidor fixa sysadmin.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir habilita a captura de dados de alterações.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_enable_db;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys. sp_cdc_disable_db &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md)  
  
  
