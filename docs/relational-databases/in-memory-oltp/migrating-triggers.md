---
title: Migrando gatilhos | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ad5385c5-5a50-40ca-a319-97d5606b8511
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4629b9f18cdf0b97b5a79cff0696973cb60f7c36
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68050139"
---
# <a name="migrating-triggers"></a>Migrando gatilhos
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  Este tópico discute gatilhos DDL e tabelas com otimização de memória.  
  
 Gatilhos DML têm suporte em tabelas com otimização de memória, mas apenas com o evento de gatilho FOR | AFTER. Para obter um exemplo, veja [Implementando UPDATE com FROM ou Subconsultas](../../relational-databases/in-memory-oltp/implementing-update-with-from-or-subqueries.md). 
  
 Os gatilhos LOGON são gatilhos definidos para serem disparados em eventos LOGON. Os gatilhos LOGON não afetam tabelas com otimização de memória.  
  
## <a name="ddl-triggers"></a>Gatilhos DDL  
 Os gatilhos DDL são gatilhos definidos para disparar quando uma instrução CREATE, ALTER, DROP, GRANT, DENY, REVOKE ou UPDATE STATISTICS é executada no banco de dados ou no servidor no qual está definida.  
  
 Você não pode criar tabelas com otimização de memória se o banco de dados ou o servidor tem um ou mais gatilhos DDL definidos em CREATE_TABLE ou em qualquer grupo de eventos que o inclua. Você não pode descartar uma tabela com otimização de memória se o banco de dados ou o servidor tem um ou mais gatilhos DDL definidos em DROP_TABLE ou em qualquer grupo de eventos que o inclua.  
  
 Você não pode criar procedimentos armazenados compilados de modo nativo quando há um ou mais gatilhos DDL em CREATE_PROCEDURE, em DROP_PROCEDURE ou em qualquer grupo de eventos que inclua esses eventos.  
  
## <a name="see-also"></a>Consulte Também  
 [Migrando para OLTP na memória](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)  
  
  
