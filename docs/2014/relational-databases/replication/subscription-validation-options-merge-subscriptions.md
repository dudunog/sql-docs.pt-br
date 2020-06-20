---
title: Opções de validação de assinatura (assinaturas de mesclagem) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.validate.mergeoptions.f1
helpviewer_keywords:
- Subscription Validation Options dialog box
ms.assetid: 4958c4ab-2025-42ce-b836-6fb4e9e6f24d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 458da0387dbaa1b366348c374748c42946893feb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063744"
---
# <a name="subscription-validation-options-merge-subscriptions"></a>Opções de Validação de Assinatura (assinaturas de mesclagem)
  Use a caixa de diálogo **Opções de Validação de Assinatura** para especificar se a validação deve usar somente uma contagem de linhas ou uma contagem de linhas e uma soma de verificação binária.  
  
## <a name="options"></a>Opções  
 **Verificar as contagens de linhas somente**  
 Selecione para validar se a tabela no Assinante tem o mesmo número de linhas que a tabela no Publicador. Esse método não valida que o conteúdo de correspondências de linhas. A validação de número de linhas fornece uma abordagem superficial à validação que pode alertá-lo sobre problemas com seus dados.  
  
 **Verificar as contagens de linhas e comparar as somas de verificação para verificar os dados da linha**  
 Além de contar o número de linhas no Publicador e no Assinante, uma soma de verificação de todos os dados é calculada usando o algoritmo de soma de verificação binária. Se a contagem de linhas falhar, a soma de verificação não será executada. Esta opção não é válida para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Validar dados no Assinante](validate-data-at-the-subscriber.md)   
 [Validar os dados replicados](validate-data-at-the-subscriber.md)  
  
  
