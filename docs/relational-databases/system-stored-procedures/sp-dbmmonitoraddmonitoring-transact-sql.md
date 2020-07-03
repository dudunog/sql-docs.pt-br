---
title: sp_dbmmonitoraddmonitoring (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitoraddmonitoring
- sp_dbmmonitoraddmonitoring_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database mirroring [SQL Server], monitoring
- sp_dbmmonitoraddmonitoring
ms.assetid: 9489dc30-af29-4363-a172-4645947fc95e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 268226d28b134ffe13a5acfca3baf47bde655baf
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85866739"
---
# <a name="sp_dbmmonitoraddmonitoring-transact-sql"></a>sp_dbmmonitoraddmonitoring (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Cria um trabalho de monitor de espelhamento de banco de dados que atualiza periodicamente o status do espelhamento de cada banco de dados espelho na instância do servidor.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dbmmonitoraddmonitoring [ update_period ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *update_period*  
 Especifica o intervalo entre atualizações em minutos. Esse valor pode ser de 1 a 120 minutos. O padrão é 1 minuto.  
  
> [!NOTE]  
>  Se o período de atualização for definido muito baixo, o tempo de resposta poderá aumentar para clientes.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Este procedimento requer aquele Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é permitido executar na instância de servidor e para executar, Agente deve estar executando para o trabalho de monitor de espelhamento de banco de dados.  
  
 Se o espelhamento de banco de dados for iniciado no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , o procedimento de **sp_dbmmonitoraddmonitoring** será executado automaticamente. Se você iniciar o espelhamento manualmente usando instruções ALTER DATABASE, para monitorar o banco de dados espelhado na instância do servidor, será necessário executar **sp_dbmmonitoraddmonitoring** manualmente.  
  
> [!NOTE]  
>  Se você executar **sp_dbmmonitoraddmonitoring** antes de configurar o espelhamento de banco de dados, o trabalho de monitoramento será executado, mas não atualizará a tabela de status na qual o histórico do monitor de espelhamento de banco de dados é armazenado.  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir inicia o monitoramento com um período de atualização de `3` minutos.  
  
```  
EXEC sp_dbmmonitoraddmonitoring 3;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitorchangemonitoring](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitordropmonitoring](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitorhelpmonitoring](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
