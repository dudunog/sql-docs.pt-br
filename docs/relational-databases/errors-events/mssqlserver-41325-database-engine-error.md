---
title: MSSQLSERVER_41325 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41325 (Database Engine error)
ms.assetid: 97c6a8bb-139a-44f3-9ed5-f46d047e8ed3
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: fadfc5afc9e45b8c09591e2c133343146a5fbe99
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68123357"
---
# <a name="mssqlserver_41325"></a>MSSQLSERVER_41325
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41325|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|HK_TX_COMMIT_SR_VALIDATION|  
|Texto da mensagem|A transação atual não foi confirmada devido a uma falha de validação serializável.|  
  
## <a name="explanation"></a>Explicação  
A transação encontrou uma falha de validação e agora está condenada.  
  
## <a name="user-action"></a>Ação do usuário  
Repita a transação com falha. Para obter mais informações, veja [OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
## <a name="see-also"></a>Consulte Também  
[OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
