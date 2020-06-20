---
title: Opção de configuração de servidor lightweight pooling | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- default lightweight pooling
- decreasing overhead
- lightweight pooling option
- system overhead [SQL Server]
- performance [SQL Server], lightweight pooling
- context switching [SQL Server], lightweight pooling option
- excessive context switching [SQL Server]
- reducing overhead
- overhead [SQL Server]
ms.assetid: 2dc11b61-d065-4126-8e00-acf40390f9fb
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 549ff7451a31b48459b5a290b94ad406c3768a91
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935230"
---
# <a name="lightweight-pooling-server-configuration-option"></a>Opção lightweight pooling de configuração de Servidor
  Use a opção **lightweight pooling** para fornecer meios para reduzir a sobrecarga do sistema associada à alternância excessiva de contexto que ocorre às vezes em ambientes SMP (multiprocessamento simétrico). Quando há alternância excessiva de contexto, o lightweight pooling pode fornecer melhor transferência realizando a alternância de contexto embutido, ajudando assim a reduzir as transições de chamadas entre o usuário e o kernel.  
  
 O modo fibra foi projetado para determinadas situações nas quais a alternância de contexto dos trabalhadores UMS são o gargalo crítico no desempenho. Como isso é raro, o modo fibra raramente aumenta o desempenho ou a escalabilidade no sistema típico. A alternância de contexto aprimorada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] também reduziu a necessidade do modo fibra. Não recomendamos o uso de agendamento do modo fibra para operação de rotina. Isso porque pode diminuir o desempenho ao inibir os benefícios comuns da alternância de contexto, e como alguns componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usam o TLS (Armazenamento de Thread Local) ou objetos de propriedade de thread, como mutexes (um tipo de objeto kernel de Win32), não funcionam corretamente no modo fibra.  
  
 Definir **lightweight pooling** como 1 faz com que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alterne para a programação de modo fibra. O valor padrão desta opção é 0.  
  
 A opção **lightweight pooling** é uma opção avançada. Se você estiver usando o procedimento armazenado do sistema **sp_configure** para alterar a configuração, será possível alterar a opção **lightweight pooling** apenas quando **show advanced options** estiver definida como 1. A configuração terá efeito depois que o servidor for reiniciado.  
  
> [!NOTE]  
>  Não há suporte para a opção lightweight pooling no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 2000 e no [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows XP. [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] fornece suporte completo à lightweight pooling.  
  
> [!NOTE]  
>  Não há suporte para a execução de CLR (common language runtime) com lightweight pooling. Desabilite uma das duas opções: “clr enabled” ou “lightweight pooling”. Alguns dos recursos que dependem de CLR e não funcionam corretamente no modo fibra incluem o tipo de dados de hierarquia, a replicação e Gerenciamento Baseado em Políticas.  
  
## <a name="see-also"></a>Consulte Também  
 [Opção clr enabled de configuração de servidor](clr-enabled-server-configuration-option.md)   
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [Opção de configuração do servidor clr enabled](clr-enabled-server-configuration-option.md)  
  
  
