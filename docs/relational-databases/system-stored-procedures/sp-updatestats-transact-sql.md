---
description: sp_updatestats (Transact-SQL)
title: sp_updatestats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_updatestats_TSQL
- sp_updatestats
dev_langs:
- TSQL
helpviewer_keywords:
- sp_updatestats
ms.assetid: 01184651-6e61-45d9-a502-366fecca0ee4
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: fbcfad5e5639fab399d65bd5ffbc24a1e0bd6cea
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473458"
---
# <a name="sp_updatestats-transact-sql"></a>sp_updatestats (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

É executado `UPDATE STATISTICS` em todas as tabelas internas e definidas pelo usuário no banco de dados atual.  
  
Para obter mais informações sobre o `UPDATE STATISTICS` , consulte [atualizar estatísticas &#40;&#41;TRANSACT-SQL ](../../t-sql/statements/update-statistics-transact-sql.md). Para obter mais informações sobre estatísticas, consulte [Estatísticas](../../relational-databases/statistics/statistics.md).  
    
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_updatestats [ [ @resample = ] 'resample']  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="arguments"></a>Argumentos  
`[ @resample = ] 'resample'` Especifica que **sp_updatestats** usará a opção reamostrar da instrução [Update Statistics](../../t-sql/statements/update-statistics-transact-sql.md) . Se **' reamostrar '** não for especificado, o **sp_updatestats** atualizará as estatísticas usando a amostragem padrão. a **reamostragem** é **varchar (8)** com um valor padrão de no.  
  
## <a name="remarks"></a>Comentários  
 **sp_updatestats** é executado `UPDATE STATISTICS` , especificando a `ALL` palavra-chave, em todas as tabelas internas e definidas pelo usuário no banco de dados. sp_updatestats exibe mensagens que indicam seu progresso. Quando a atualização é concluída, ela informa que as estatísticas foram atualizadas em todas as tabelas.  
  
**sp_updatestats** atualiza estatísticas em índices não clusterizados desabilitados e não atualiza estatísticas em índices clusterizados desabilitados.  
  
Para tabelas baseadas em disco, o **sp_updatestats** atualiza as estatísticas com base nas informações de **modification_counter** na exibição de catálogo **Sys. dm_db_stats_properties** , atualizando as estatísticas em que pelo menos uma linha foi modificada. As estatísticas em tabelas com otimização de memória sempre são atualizadas durante a execução de **sp_updatestats**. Portanto, não execute **sp_updatestats** mais do que o necessário.  
  
**sp_updatestats** pode disparar uma recompilação de procedimentos armazenados ou outro código compilado. No entanto, **sp_updatestats** pode não causar uma recompilação, se apenas um plano de consulta for possível para as tabelas referenciadas e os índices nelas. Uma recompilação será desnecessária nesses casos mesmo que as estatísticas sejam atualizadas.  
  
Para bancos de dados com um nível de compatibilidade abaixo de 90, a execução de **sp_updatestats** não preserva a configuração NORECOMPUTE mais recente para estatísticas específicas. Para bancos de dados com um nível de compatibilidade de 90 ou superior, sp_updatestats preserva a opção NORECOMPUTE mais recente para estatísticas específicas. Para obter mais informações sobre como desabilitar e reabilitar atualizações de estatísticas, veja [Estatísticas](../../relational-databases/statistics/statistics.md).  
  
## <a name="permissions"></a>Permissões  

Para executar **sp_updatestats**, o usuário deve ser o proprietário do banco de dados (o `dbo` , não apenas membro da função `db_owner` ) ou ser membro da função de servidor fixa sysadmin.

## <a name="examples"></a>Exemplos  
O exemplo a seguir atualiza as estatísticas de tabelas no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_updatestats;   
```  

## <a name="automatic-index-and-statistics-management"></a>Índice automático e gerenciamento de estatísticas
Aproveite soluções como a [Desfragmentação de índice adaptável](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag) para gerenciar automaticamente a desfragmentação de índice e as atualizações de estatísticas em um ou mais bancos de dados. Este procedimento escolhe automaticamente se deve recompilar ou reorganizar um índice de acordo com seu nível de fragmentação, entre outros parâmetros, e atualizar as estatísticas com um limite linear.

## <a name="see-also"></a>Consulte Também  
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sp_autostats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-autostats-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_createstats ](../../relational-databases/system-stored-procedures/sp-createstats-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [Procedimentos armazenados do sistema](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
 
