---
title: Instalar o SQL Server PowerShell | Microsoft Docs
description: Este artigo descreve os componentes do SQL Server PowerShell instalados quando você seleciona recursos do SQL Server que exigem suporte do PowerShell.
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 854c0b2f-02d2-46a4-a8cc-6b7a5d191cf8
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 1de1d21208319773552d315714306abe3530f871
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670413"
---
# <a name="install-sql-server-powershell"></a>Instalar o SQL Server PowerShell
[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A instalação configura automaticamente os componentes do PowerShell.  

Você instala o software que oferece suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao Windows PowerShell usando o programa de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ao selecionar quaisquer recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que exigem suporte do PowerShell, a Instalação instala os seguintes componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell:  
  
- Snap-ins do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell. Os snap-ins são arquivos dll que implementam dois tipos de suporte do Windows PowerShell ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
  - Conjunto de cmdlets do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os cmdlets são comandos que implementam uma ação específica. Por exemplo, **Invoke-Sqlcmd** executa um script [!INCLUDE[tsql](../../includes/tsql-md.md)] ou XQuery que também pode ser executado usando o utilitário **sqlcmd** , e **Invoke-PolicyEvaluation** relata se os objetos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cumprem as políticas de gerenciamento baseadas em políticas.  
  
  - Um provedor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O provedor permite navegar pela hierarquia dos objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um caminho semelhante a um caminho de sistema de arquivos. Cada objeto é associado a uma classe de modelos de objeto de gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Você pode usar os métodos e as propriedades da classe para realizar trabalhos nos objetos. Por exemplo, se você usar cd para um objeto do banco de dados em um caminho, poderá usar os métodos e as propriedades da classe Microsoft.SqlServer.Managment.SMO.Database para gerenciar o banco de dados.  
 
- O módulo **sqlps** , que é importado para as sessões do Windows PowerShell a fim de carregar os snap-ins do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
 
- [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] dá suporte à inicialização das sessões do Windows PowerShell por meio da árvore do Pesquisador de Objetos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent dá suporte às etapas de trabalho do Windows PowerShell.  
  
O Windows Server 2012 e posterior e o Windows 8 e posterior são fornecidos com o PowerShell instalado e configurado. Para obter informações sobre como instalar o Windows PowerShell, confira [Instalando o Windows PowerShell](/powershell/scripting/install/installing-windows-powershell).  

Para obter mais informações, consulte:   

- [SQL Server PowerShell](../../powershell/sql-server-powershell.md)  
  
