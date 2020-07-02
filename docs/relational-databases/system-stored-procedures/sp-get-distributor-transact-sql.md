---
title: sp_get_distributor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_get_distributor
- sp_get_distributor_TSQL
helpviewer_keywords:
- sp_get_distributor
ms.assetid: f0134448-bc17-4f2f-bd81-619351ce56ac
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 545bc84b8b68f89428912aba635c87ce23dcbd22
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85757922"
---
# <a name="sp_get_distributor-transact-sql"></a>sp_get_distributor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Determina se um Distribuidor é instalado em um servidor. Esse procedimento armazenado é executado no computador onde o Distribuidor está sendo procurado, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_get_distributor   
```  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**recém-instalado**|**int**|**0** = não; **1** = Sim|  
|**servidor de distribuição**|**sysname**|O nome do servidor Distribuidor.|  
|**BD de distribuição instalado**|**int**|**0** = não; **1** = Sim|  
|**is distribution publisher**|**int**|**0** = não; **1** = Sim|  
|**tem Publicador de distribuição remota**|**int**|**0** = não; **1** = Sim|  
  
## <a name="remarks"></a>Comentários  
 **sp_get_distributor** é usado principalmente pela [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] replicação de instantâneo, transacional e de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário pode executar **sp_get_distributor**. Um conjunto de resultados não nulo é retornado quando esse procedimento armazenado é executado por membros das funções de banco de dados fixas **db_owner** ou **replmonitor** no banco de dados de distribuição ou membros da função de banco de dados fixa **db_owner** em pelo menos um banco de dados publicado. Um conjunto de resultados não nulo também é retornado quando esse procedimento armazenado é executado por usuários na PAL (lista de acesso à publicação) de pelo menos um banco de dados publicado ou na PAL do banco de dados de distribuição para um Publicador não SQL Server, também pode executar **sp_get_distributor**.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar a publicação e a distribuição](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Script de informações do distribuidor e do Publicador](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
