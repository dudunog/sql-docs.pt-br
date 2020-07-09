---
title: Armazenamento do gerenciamento baseado em políticas | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, storage
ms.assetid: d0cbf214-fc2e-4917-8d31-1d71c9ffa61d
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 7b927398f565720412bbd9f15b9520a17ef0a960
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727303"
---
# <a name="policy-based-management-storage"></a>Armazenamento do Gerenciamento Baseado em Políticas
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  As políticas são armazenadas no banco de dados msdb. Após a alteração de uma política ou condição, deve ser feito backup do msdb. Para obter mais informações, consulte [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
## <a name="storing-policies"></a>Armazenando políticas  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] inclui políticas que podem ser usadas para monitorar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por padrão, essas políticas não são instaladas no [!INCLUDE[ssDE](../../includes/ssde-md.md)]; no entanto, elas podem ser importadas do local de instalação padrão C:\Arquivos de Programas (x86)\Microsoft SQL Server\140\Tools\Policies\DatabaseEngine\1033.  
  
 Você pode criar políticas diretamente usando o menu **Arquivo/Novo** e salvá-las em um arquivo. Isso permite criar políticas quando você não estiver conectado a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 O histórico de políticas avaliadas na instância atual do [!INCLUDE[ssDE](../../includes/ssde-md.md)] é mantido em tabelas do sistema de msdb. O histórico de políticas aplicadas a outras instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)] ou aplicadas ao [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ou ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não é retido.  
  
  
