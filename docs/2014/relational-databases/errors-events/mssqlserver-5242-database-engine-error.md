---
title: MSSQLSERVER_5242 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 5242 (Database Engine error)
ms.assetid: 712b1a10-2f87-41df-a111-1ed9f14102d4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: baf35c096ec552c39b70729470263765570e79dd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62913627"
---
# <a name="mssqlserver_5242"></a>MSSQLSERVER_5242
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|5242|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico||  
|Texto da mensagem|Foi detectada uma inconsistência durante uma operação interna no banco de dados '%.*ls' (ID:%d) na página %S_PGID. Contate o suporte técnico. Número de referência %ld.|  
  
## <a name="explanation"></a>Explicação  
 Ocorreu uma inconsistência estrutural na página do banco de dados referenciada na mensagem de erro.  
  
## <a name="see-also"></a>Consulte Também  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [Arquivos e grupos de arquivos do banco de dados](../databases/database-files-and-filegroups.md)  
  
  
