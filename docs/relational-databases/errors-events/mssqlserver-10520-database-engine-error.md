---
title: MSSQLSERVER_10520 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10520 (Database Engine error)
ms.assetid: cc8799f1-5b90-4248-b209-e1d5087f9529
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4b39522a5aa1e3208dfe1f7440abe20f4f0e00fc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68068165"
---
# <a name="mssqlserver_10520"></a>MSSQLSERVER_10520
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|10520|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PG_PARAM_NOT_ALLOWED|  
|Texto da mensagem|Não é possível criar o guia de plano '%.*ls' porque @type foi especificado como '%ls' e um valor não NULL está especificado para o parâmetro '%ls'. Esse tipo requer um valor NULL para o parâmetro. Especifique um valor NULL para o parâmetro ou altere o tipo para um que permita um valor não NULL para o parâmetro.|  
  
## <a name="explanation"></a>Explicação  
O tipo especificado em @type exige um valor NULL para o parâmetro especificado; entretanto, foi fornecido um valor não NULL.  
  
## <a name="user-action"></a>Ação do usuário  
Especifique um valor NULL para o parâmetro ou altere o tipo para um que permita um valor não NULL para o parâmetro.  
  
## <a name="see-also"></a>Consulte Também  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guias de plano](~/relational-databases/performance/plan-guides.md)  
  
