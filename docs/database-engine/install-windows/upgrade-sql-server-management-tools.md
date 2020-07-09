---
title: Fazer upgrade das Ferramentas de Gerenciamento do SQL Server | Microsoft Docs
description: Este artigo descreve o suporte para atualização de componentes de gerenciamento e Ferramentas de Gerenciamento do SQL Server, como o SQL Server Agent.
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- management tools, upgrading
ms.assetid: 1dab50b9-d16c-49a1-9ecc-af72adb6c378
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 2c10d77a72ef23616feb2ac59db44589966fe49a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85900229"
---
# <a name="upgrade-sql-server-management-tools"></a>Atualizar Ferramentas de Gerenciamento do SQL Server

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dá suporte à atualização do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e posterior. Este artigo documenta o suporte e o comportamento da atualização das Ferramentas de Gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e dos componentes de gerenciamento, tais como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, Database Mail, Maintenance Plans, XPStar e XPWeb.  
  
> [!IMPORTANT]  
>  Em instalações locais, você deve executar a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como um administrador. Se você executar a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir de um compartilhamento remoto, deverá usar uma conta de domínio que tenha permissões de leitura e execução no compartilhamento remoto.  
  
## <a name="known-upgrade-issues"></a>Problemas de atualização conhecidos  
Considere os seguintes problemas antes de atualizar para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
### <a name="for-all-upgrade-scenarios"></a>Para todos os cenários de atualização:  
  
- Todos os servidores TSX devem ser atualizados antes que o servidor MSX seja atualizado. Para obter mais informações sobre MSX/TSX no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Administração automatizada em toda a empresa](../../ssms/agent/automated-administration-across-an-enterprise.md).  
  
-   Todos os componentes de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem ser atualizados ao mesmo tempo. Os números de versão dos componentes do [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]e do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] devem ser os mesmos em uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   É possível adicionar componentes a uma instalação existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no momento em que você atualiza para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter mais informações, consulte [Fazer upgrade do SQL Server 2016 usando o Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md).  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] As Ferramentas de Cliente, tais como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]e o Orientador de otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] , sqlcmd e osql não são atualizadas para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. As Ferramentas de Cliente são executadas lado a lado com ferramentas de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] dá suporte a configurações de importação de versões anteriores de Ferramentas de Cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   A autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será atualizada da Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para a Autenticação do Windows durante a atualização. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Não há suporte à autenticação no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   Os dados de trabalhos e alertas serão preservados durante a atualização para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   Se o SQLMail estiver sendo usado na instância a ser atualizada, depois da atualização haverá suporte para os XPs associados e eles serão habilitados. Caso contrário, eles ficarão desligados.  
  
-   O Database Mail, também conhecido como SQLiMail, será atualizado com o componente [!INCLUDE[ssDE](../../includes/ssde-md.md)] do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Por padrão, o Database Mail será desligado após a atualização. Quaisquer atualizações de esquema devem ser reconciliadas com um script de atualização após a atualização.  
  
## <a name="see-also"></a>Consulte Também  
 [Atualizações de versão e edição com suporte](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [Compatibilidade com versões anteriores_excluída](https://msdn.microsoft.com/library/15d9117e-e2fa-4985-99ea-66a117c1e9fd)   
 [Fazer Upgrade do SQL Server Usando o Assistente de Instalação &#40;Instalação&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)  
  
  
