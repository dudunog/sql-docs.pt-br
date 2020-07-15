---
title: Opção de configuração de servidor ft crawl bandwidth | Microsoft Docs
description: Saiba mais sobre a opção "ft crawl bandwidth". Veja como ela afeta o número de buffers que SQL Server mantém no pool de buffers de memória grandes.
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- large memory buffers
- memory [SQL Server], buffers
- ft crawl bandwidth option
ms.assetid: e5864ad9-92f5-43b5-95de-46d68ded8694
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 59caa1e868c4caab24afd17909c34f57c96f0005
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789790"
---
# <a name="ft-crawl-bandwidth-server-configuration-option"></a>Opção de configuração de servidor ft crawl bandwidth
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Use a opção **ft crawl bandwidth** para especificar o tamanho até o qual o pool de buffers de memória grandes pode se expandir. Buffers de memória grandes têm o tamanho de 4 MB (megabytes). O valor do parâmetro **max** especifica o número máximo de buffers que o gerenciador de memória de texto completo deve manter em um pool de buffers grandes. Se o valor de **max** for zero, não haverá limite máximo ao número de buffers no pool de buffers grandes.  
  
 O valor do parâmetro **min** especifica o número mínimo de buffers de memória que deve ser mantido no pool de buffers de memória grandes. Mediante solicitação do gerenciador de memória do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], todos os pools de buffers extras serão liberados, mas esse número mínimo de buffers será mantido. Se, contudo, o valor especificado de **min** for zero, todos os buffers de memória serão liberados.  
  
 Em algumas circunstâncias, o número de buffers alocados atualmente é menor que o valor especificado pelo parâmetro **min** .  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Opção de configuração de servidor ft notify bandwidth](../../database-engine/configure-windows/ft-notify-bandwidth-server-configuration-option.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
