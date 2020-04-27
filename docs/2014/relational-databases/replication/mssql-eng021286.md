---
title: MSSQL_ENG021286 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021286 error
ms.assetid: b63620b7-1c6d-46f7-90ea-3a8e99af8de4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 54e5d7b496affcd6d9ead2c50f50e807e7e920a7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63023225"
---
# <a name="mssql_eng021286"></a>MSSQL_ENG021286
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|21286|  
|Origem do Evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|A tabela de conflitos '%s' não existe.|  
  
## <a name="explanation"></a>Explicação  
 Esse erro será acionado se a tabela de conflitos de um artigo listado em [sysmergearticles &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysmergearticles-transact-sql) não existir de fato. O erro pode ocorrer ao tentar adicionar uma coluna ou descartar uma coluna de uma tabela publicada para replicação de mesclagem.  
  
## <a name="user-action"></a>Ação do usuário  
 Execute [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql) no banco de dados com a tabela de conflitos ausente para verificar se não há problemas de consistência de dados.  
  
 Se a tabela de conflitos estiver ausente em um Assinante, descarte a assinatura e recrie-a. Se a tabela de conflitos estiver ausente em um Publicador, descarte todas as assinaturas, descarte a publicação e, depois, recrie a publicação e todas as assinaturas. Para obter mais informações, consulte [Publicar dados e objetos de banco de dados](publish/publish-data-and-database-objects.md) e [Assinar publicações](subscribe-to-publications.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](errors-and-events-reference-replication.md)  
  
  
