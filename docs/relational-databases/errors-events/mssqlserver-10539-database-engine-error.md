---
description: MSSQLSERVER_10539
title: MSSQLSERVER_10539 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10539 (Database Engine error)
ms.assetid: 49c26ff7-18b8-4f07-a087-f45f63463b3b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9f1f36f5b8721a94b7badb3316f30f9b3d4e059d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88338202"
---
# <a name="mssqlserver_10539"></a>MSSQLSERVER_10539
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
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
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
