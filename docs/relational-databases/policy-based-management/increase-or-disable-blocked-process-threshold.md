---
title: Aumentar ou desabilitar o limite de processo bloqueado | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 71db8ef6-341b-4465-99db-5c63e48d4c7d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: ef493b3af967adf83b59a1d272f69b0b677149c5
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68087218"
---
# <a name="increase-or-disable-blocked-process-threshold"></a>Aumentar ou desabilitar o limite de processo bloqueado
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Estas regras verificam se a opção de limite de processo bloqueado está definida como 0 (desabilitada) ou com um valor maior ou igual a 5 (segundos). Definir a opção de limite de processo bloqueado com um valor de 1 até 4 pode fazer o monitor de deadlock ser executado constantemente. Valores de 1 a 4 devem ser usados apenas para solução de problemas e nunca a longo prazo ou em um ambiente de produção sem a assistência do Suporte e Atendimento ao Cliente [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Para resolver este problema, defina a opção de limite de processo bloqueado com um valor de 5 (segundos) ou mais ou desabilite o limite de processo bloqueado definindo o valor como 0. Para definir o limite de processo bloqueado com um valor de `5` segundos, execute a seguinte instrução:  
  
```  
sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE ;  
GO  
sp_configure 'blocked process threshold', 5 ;  
GO  
RECONFIGURE ;  
GO  
```  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Opção blocked process threshold de configuração de servidor](../../database-engine/configure-windows/blocked-process-threshold-server-configuration-option.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor melhores práticas usando o gerenciamento baseado em políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
