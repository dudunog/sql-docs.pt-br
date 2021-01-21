---
title: Habilitar backups coordenados (transacional)
description: Saiba como habilitar backups coordenados no banco de dados de distribuição, de modo que o log de transações do banco de dados de publicação da replicação transacional não seja truncado até que as transações que foram propagadas para o Distribuidor tenham sido copiadas em backup.
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- transactional replication, backup and restore
- sp_replicationdboption
- sync with backup [SQL Server replication]
- coordinated backups [SQL Server replication]
- backups [SQL Server replication], transactional replication
ms.assetid: 73a914ba-8b2d-4f4d-ac1b-db9bac676a30
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 34911188162ac5b63f5a43d510d10d503820d200
ms.sourcegitcommit: f29f74e04ba9c4d72b9bcc292490f3c076227f7c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/13/2021
ms.locfileid: "98170468"
---
# <a name="enable-coordinated-backups-for-transactional-replication"></a>Habilitar backups coordenados para replicação transacional
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Quando habilitar um banco de dados para a replicação transacional, é possível especificar que seja efetuado um backup de todas as transações antes que elas sejam entregues ao banco de dados de distribuição. Você pode habilitar também um backup coordenado no banco de dados de distribuição de modo que o log de transações, para o banco de dados de publicação, não fique truncado até que seja efetuado o backup das transações que foram propagadas ao Distribuidor. Para obter mais informações, consulte [Estratégias para fazer backup e restaurar o instantâneo e a replicação transacional](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md).  
  
### <a name="to-enable-coordinated-backups-for-a-database-published-with-transactional-replication"></a>Para habilitar backups coordenados para um banco de dados publicado com replicação transacional  
  
1.  No Publicador, use a função `SELECT DATABASEPROPERTYEX(DB_NAME(),'IsSyncWithBackup')` [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) para retornar a propriedade **IsSyncWithBackup** do banco de dados de publicação. Se a função retornar **1**, os backups coordenados já estarão habilitados para o banco de dados publicado.  
  
2.  Se a função na etapa 1 retornar **0**, execute [sp_replicationdboption &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) no Publicador do banco de dados de publicação. Especifique um valor de **sync with backup** para **\@optname** e **true** para **\@value**.  
  
    > [!NOTE]  
    >  Se alterar a opção **sync with backup** para **falso**, o ponto de truncamento do banco de dados de publicação será atualizado após a execução do Agente de Leitor de Log ou após um intervalo, caso o Agente de Leitor de Log esteja executando continuamente. O intervalo máximo é controlado pelo parâmetro do agente **-MessageInterval** (que tem um padrão de 30 segundos).  
  
### <a name="to-enable-coordinated-backups-for-a-distribution-database"></a>Para habilitar backups coordenados para um banco de dados de distribuição  
  
1.  No Editor, use a função [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) para retornar a propriedade **IsSyncWithBackup** do banco de dados de distribuição. Se a função retornar **1**, os backups coordenados já estarão habilitados para o banco de dados de distribuição.  
  
2.  Se a função na etapa 1 retornar **0**, execute [sp_replicationdboption &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) no Distribuidor do banco de dados de distribuição. Especifique um valor de **sync with backup** para **\@optname** e **true** para **\@value**.  
  
### <a name="to-disable-coordinated-backups"></a>Para desabilitar backups coordenados  
  
1.  No Publicador do banco de dados de publicação ou no Distribuidor no banco de dados de distribuição, execute [sp_replicationdboption &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md). Especifique um valor **sync with backup** para **\@optname** e **false** para **\@value**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-retrieve-the-issyncwithbackup-property-for-the-current-database"></a>a. Recuperar a propriedade `IsSyncWithBackup` para o banco de dados atual

Este exemplo retorna a propriedade `IsSyncWithBackup` para o banco de dados atual:
  
```sql
SELECT DATABASEPROPERTYEX(DB_NAME(),'IsSyncWithBackup')`
```

### <a name="b-retrieve-the-issyncwithbackup-property-for-a-specific-database"></a>B. Recuperar a propriedade `IsSyncWithBackup` para um banco de dados específico

Este exemplo retorna a propriedade `IsSyncWithBackup` para o banco de dados `NameOfDatabaseToCheck`:
  
```sql
SELECT DATABASEPROPERTYEX('NameOfDatabaseToCheck','IsSyncWithBackup')`
```
