---
title: MSSQLSERVER_10539 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10539 (Database Engine error)
ms.assetid: 49c26ff7-18b8-4f07-a087-f45f63463b3b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5fd1f190b8f5d3ab9755409bdd034fa374ea5314
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969766"
---
# <a name="mssqlserver_10539"></a>MSSQLSERVER_10539
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|10539|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_NO_PLAN_FOR_STMT|  
|Texto da mensagem|Não é possível criar o guia de plano '%.*ls' a partir do cache porque um plano de consulta não está disponível para a instrução com deslocamento inicial %d. Esse problema poderá ocorrer se a instrução depender de objetos do banco de dados que ainda não foram criados. Verifique se todos os objetos de banco de dados necessários existem e execute a instrução antes de criar o guia de plano.|  
  
## <a name="explanation"></a>Explicação  
 Não há um plano de consulta disponível no cache de planos para a instrução com o deslocamento inicial especificado.  
  
## <a name="user-action"></a>Ação do usuário  
 Verifique se todos os objetos de banco de dados necessários existem e execute a instrução antes de criar o guia de plano.  
  
## <a name="see-also"></a>Consulte Também  
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
