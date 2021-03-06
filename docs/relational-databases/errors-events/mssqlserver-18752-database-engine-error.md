---
description: MSSQLSERVER_18752
title: MSSQLSERVER_18752 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 18752 (Database Engine error)
ms.assetid: 234c58d8-7a1e-4b07-a64b-32a311527980
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 50327e76c43f67dbed77e45457481e2b032f32ef
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499477"
---
# <a name="mssqlserver_18752"></a>MSSQLSERVER_18752
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|18752|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|REPL_INUSE|  
|Texto da mensagem|Somente um Agente de Leitor de Log ou um procedimento relacionado ao log (sp_repldone, sp_replcmds e sp_replshowcmds) pode se conectar ao banco de dados de cada vez. Se você tiver executado um procedimento relacionado ao log, descarte a conexão através da qual o procedimento foi executado ou execute sp_replflush por essa conexão antes de iniciar o Agente de Leitor de Log ou de executar outro procedimento relacionado ao log.|  
  
## <a name="explanation"></a>Explicação  
Somente um Log Reader Agent ou um procedimento relacionado ao log pode se conectar ao banco de dados de cada vez.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique se nenhum outro leitor de log está sendo executado no mesmo banco de dados de publicação e se nenhuma outra conexão ativa executou sp_replcmds/sp_repltrans/sp_repldone anteriormente sem executar sp_replflush em seguida ou desconectar.  
  
