---
title: Procedimentos armazenados compilados nativamente e opções definidas
description: As opções SET de uma sessão não afetam uma execução de procedimento armazenado, exceto pelo fato de que determinadas opções SET fazem com que procedimentos armazenados não sejam executados.
ms.custom: seo-dt-2019
ms.date: 10/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c1869cf7-9030-4d18-85d6-0e419a4e9af7
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e86ab52348e4e51a2b060bab50aecf2d3c453fc3
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97485278"
---
# <a name="natively-compiled-stored-procedures-and-execution-set-options"></a>Procedimentos armazenados compilados nativamente e opções de execução Set
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

As opções de sessão são fixadas em blocos atômicos, conforme descrito em [Blocos atômicos](atomic-blocks-in-native-procedures.md). A execução de um procedimento armazenado não é afetada pelas opções SET de uma sessão, pois os blocos atômicos são necessários. No entanto, determinadas opções SET, como SET NOEXEC e SET SHOWPLAN_XML, fazem com que os procedimentos armazenados (incluindo os procedimentos armazenados compilados nativamente) não sejam executados.   
  
 Quando um procedimento armazenado compilado nativamente for executado com qualquer opção STATISTICS ativada, as estatísticas serão coletadas para o procedimento como um todo, e não por instrução. Para obter mais informações, veja [SET STATISTICS IO &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-io-transact-sql.md), [SET STATISTICS PROFILE &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-profile-transact-sql.md), [SET STATISTICS TIME &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-time-transact-sql.md) e [SET STATISTICS XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-xml-transact-sql.md). Para obter estatísticas de execução no nível por instrução em procedimentos armazenados criados nativamente, use uma sessão de evento estendido no evento sp_statement_completed, que inicia quando cada consulta individual em uma execução de procedimentos armazenados é concluída. Para obter mais informações sobre como criar sessões de Eventos Estendidos, veja [CREATE EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md).  
  
 Há suporte para **SHOWPLAN_XML** para procedimentos armazenados compilados de modo nativo. Não há suporte para **SHOWPLAN_ALL** e **SHOWPLAN_TEXT** em procedimentos armazenados compilados de modo nativo.  
  
 Não há suporte para **SET FMTONLY** com procedimentos armazenados compilados nativamente. Em vez disso, use [sp_describe_first_result_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados compilados nativamente](./a-guide-to-query-processing-for-memory-optimized-tables.md)  
  
