---
title: Opção de configuração de servidor disallow results from triggers | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], result sets
- result sets [SQL Server], triggers
- disallow results from triggers option
ms.assetid: 47149073-307d-47a5-b7d2-66a737d3231d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 28bf3b201d54798f26c9e887e86a9d0bed78ee15
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68011865"
---
# <a name="disallow-results-from-triggers-server-configuration-option"></a>Opção de configuração de servidor disallow results from triggers
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Use a opção **rejeitar resultados dos gatilhos** para controlar se os gatilhos retornam conjuntos de resultados. Os gatilhos que retornam conjuntos de resultados podem causar um comportamento inesperado em aplicativos que não são projetados para trabalhar com eles.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Recomendamos que você defina esse valor como 1.  
  
 Ao definir como 1, a opção **rejeitar resultados dos gatilhos** será definida como ON. A configuração padrão para esta opção é 0 (OFF). Se esta opção estiver definida para 1 (ON), qualquer tentativa feita por um gatilho para retornar um conjunto de resultados falhará e o usuário receberá a seguinte mensagem de erro:  
  
 "Msg 524, Level 16, State 1, Procedure \<Procedure Name>, Line \<Line#>  
  
 "Um gatilho retornou um conjunto de resultados e a opção do servidor 'disallow_results_from_triggers' é verdadeira."  
  
 A opção **disallow results from triggers** é aplicada no nível de instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e determinará o comportamento de todos os gatilhos existentes na instância.  
  
 A opção **rejeitar resultados dos gatilhos** é uma opção avançada. Se você estiver usando o procedimento armazenado no sistema **sp_configure** para alterar a configuração, é possível alterar a opção rejeitar resultados dos gatilhos somente quando **mostrar opções avançadas** estiver definida como 1. A configuração entra em vigor imediatamente sem a reinicialização do servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
