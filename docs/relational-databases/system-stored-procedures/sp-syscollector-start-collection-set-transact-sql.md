---
title: sp_syscollector_start_collection_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_start_collection_set_TSQL
- sp_syscollector_start_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_start_collection_set
ms.assetid: d8357180-f51e-4681-99f9-0596fe2d2b53
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 52afba46b09552af62ba9f08c34e1749689f41cc
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82809812"
---
# <a name="sp_syscollector_start_collection_set-transact-sql"></a>sp_syscollector_start_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inicia um conjunto de coleta se o coletor já estiver habilitado e o conjunto de coleta não estiver sendo executado. Se o coletor não estiver habilitado, habilite o coletor executando [sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md) e, em seguida, use esse procedimento armazenado para iniciar um conjunto de coleta.  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syscollector_start_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @collection_set_id = ] collection_set_id`É o identificador local exclusivo para o conjunto de coleta. *collection_set_id* é **int** com um valor padrão de NULL. *collection_set_id* deverá ter um valor se o *nome* for nulo.  
  
`[ @name = ] 'name'`É o nome do conjunto de coleta. o *nome* é **sysname** com um valor padrão de NULL. o *nome* deve ter um valor se *collection_set_id* for nulo.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 sp_syscollector_create_collection_set deve ser executado no contexto do banco de dados do sistema msdb e o SQL Server Agent deve estar habilitado.  
  
 Este procedimento falha quando executado em um conjunto de coleta que não tem uma agenda. Se o conjunto de coleta não tiver um agendamento (porque seu modo de coleta está definido como não armazenado em cache, por exemplo), use o procedimento armazenado [sp_syscollector_run_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql.md) para iniciar o conjunto de coleta.  
  
 Este procedimento habilita os trabalhos de carregamento e de coleta para o conjunto de coleta especificado e iniciará imediatamente o trabalho do agente de coleta, se o conjunto de coleta tiver seu modo de coleta definido como armazenado em cache (0). Para obter mais informações, consulte [sp_syscollector_create_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md).  
  
 Se o conjunto de coleta não contiver nenhum item de coleta, essa operação não terá nenhum efeito. O erro 14685 é retornado como um aviso.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa dc_operator para executar esse procedimento. Se o conjunto de coleta não tiver uma conta proxy, a associação da função de servidor fixa sysadmin será necessária.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir inicia um conjunto de coleta usando seu identificador.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_start_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Coleta de dados](../../relational-databases/data-collection/data-collection.md)   
 [syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
