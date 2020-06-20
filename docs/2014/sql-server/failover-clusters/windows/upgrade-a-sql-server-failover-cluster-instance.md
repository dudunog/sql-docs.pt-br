---
title: Atualizar um cluster de failover do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading failover clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], upgrading
ms.assetid: daac41fe-7d0b-4f14-84c2-62952ad8cbfa
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6f2794fd33ee2210b99aead0f79fd3a3ab470c00
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85046094"
---
# <a name="upgrade-a-sql-server-failover-cluster"></a>Atualizar um cluster de failover do SQL Server
  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferece suporte à atualização do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] e do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] a partir de clusters de failover do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], do [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], do [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] e do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] separadamente em todos os nós de cluster de failover.  
  
 Os detalhes do suporte são os seguintes:  
  
-   A atualização tem suporte na interface do usuário e no prompt de comando. Para obter mais informações, consulte [Atualizar uma instância de cluster de failover do SQL Server &#40;Instalação&#41;](upgrade-a-sql-server-failover-cluster-instance-setup.md) e [Instalar o SQL Server 2014 do prompt de comando](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
-   Atualizando de [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] – você pode executar a atualização do prompt de comando em cada nó de cluster de failover ou usando a interface do usuário de instalação para atualizar cada nó de cluster. Se os recursos de pesquisa de texto completo e de Replicação não existirem na instância que está sendo atualizada, eles serão instalados automaticamente sem a opção para omiti-los.  
  
-   Instalação de service pack: você deve aplicar service packs e patches do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para os clusters de failover do [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] separadamente em todos os nós.  
  
-   Os cenários a seguir não têm suporte:  
  
    -   Não é possível migrar de uma instância autônoma do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para um cluster de failover.  
  
    -   Adicionar recursos a um cluster de failover. Por exemplo, você não pode adicionar o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] a um cluster de failover somente do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
    -   Você não pode fazer downgrade do nó de cluster de failover para uma instância autônoma.  
  
-   Para obter mais informações, consulte [Instâncias do Cluster de Failover do AlwaysOn (SQL Server)](always-on-failover-cluster-instances-sql-server.md).  
  
## <a name="upgrading-a-ssnoversion-multi-subnet-failover-cluster"></a>Atualizando um cluster de failover de várias sub-redes do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 Não é possível atualizar diretamente um cluster de failover que não seja de várias sub-redes [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cluster de failover de várias sub-redes. Para obter mais informações, consulte [Atualizar uma instância de cluster de failover do SQL Server &#40;instalação&#41;](upgrade-a-sql-server-failover-cluster-instance-setup.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Atualizações de versão e edição com suporte](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [Atualizar uma instância de cluster de failover SQL Server &#40;instalação&#41;](upgrade-a-sql-server-failover-cluster-instance-setup.md)   
 [Install SQL Server 2014 from the Command Prompt](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)  
  
  
