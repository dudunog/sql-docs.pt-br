---
description: cursores (Transact-SQL)
title: Cursores (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- statements [SQL Server], cursors
- functions [SQL Server], cursors
- cursors [SQL Server], statements
ms.assetid: 63000023-54fc-4efc-a30f-fb4d4db73aae
author: cawrites
ms.author: chadam
ms.openlocfilehash: c32458123a5f67ac47718bee19f07912c548879c
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98100936"
---
# <a name="cursors-transact-sql"></a>cursores (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  As instruções do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] produzem um conjunto de resultados completo, mas há momentos em que os resultados são mais bem processados considerando uma linha de cada vez. Abrir um cursor em um conjunto de resultados permite o processamento do conjunto de resultados uma linha por vez. Você pode atribuir um cursor a uma variável ou um parâmetro com um tipo de dados **cursor**.  
  
 Operações de cursor têm suporte nestas instruções:  
  
 [CLOSE](../../t-sql/language-elements/close-transact-sql.md)  
  
 [CREATE PROCEDURE](../../t-sql/statements/create-procedure-transact-sql.md)  
  
 [DEALLOCATE](../../t-sql/language-elements/deallocate-transact-sql.md)  
  
 [DECLARE CURSOR](../../t-sql/language-elements/declare-cursor-transact-sql.md)  
  
 [DECLARE @local_variable](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
  
 [DELETE](../../t-sql/statements/delete-transact-sql.md)  
  
 [FETCH](../../t-sql/language-elements/fetch-transact-sql.md)  
  
 [OPEN](../../t-sql/language-elements/open-transact-sql.md)  
  
 [UPDATE](../../t-sql/queries/update-transact-sql.md)  
  
 [SET](../../t-sql/statements/set-statements-transact-sql.md)  
  
 Estas funções de sistema e procedimentos armazenados do sistema também oferecem suporte a cursores:  
  
 [@@CURSOR_ROWS](../../t-sql/functions/cursor-rows-transact-sql.md)  
  
 [CURSOR_STATUS](../../t-sql/functions/cursor-status-transact-sql.md)  
  
 [@@FETCH_STATUS](../../t-sql/functions/fetch-status-transact-sql.md)  
  
 [sp_cursor_list](../../relational-databases/system-stored-procedures/sp-cursor-list-transact-sql.md)  
  
 [sp_describe_cursor](../../relational-databases/system-stored-procedures/sp-describe-cursor-transact-sql.md)  
  
 [sp_describe_cursor_columns](../../relational-databases/system-stored-procedures/sp-describe-cursor-columns-transact-sql.md)  
  
 [sp_describe_cursor_tables](../../relational-databases/system-stored-procedures/sp-describe-cursor-tables-transact-sql.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Cursores](../../relational-databases/cursors.md)  
  
  
