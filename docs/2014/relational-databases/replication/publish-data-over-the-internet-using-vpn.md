---
title: Publicar dados pela Internet usando a VPN | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- VPNs [SQL Server replication]
- Web publishing [SQL Server replication], VPNs
- Internet [SQL Server replication], VPNs
ms.assetid: 9ffb6546-9973-4574-aaa0-8fe0017e3601
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f090e48f97f4756f6c87b7cac2a6db64105ef265
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63021067"
---
# <a name="publish-data-over-the-internet-using-vpn"></a>Publicar dados pela Internet usando VPN
  A tecnologia VPN (rede virtual privada) permite que usuários que trabalham em casa, filiais, clientes remotos e outras empresas se conectem a uma rede corporativa pela Internet, mantendo comunicações seguras. Os usuários podem usar a Autenticação do Windows como se estivessem em uma LAN (rede local). Todos os tipos de replicação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem replicar dados por uma VPN; no entanto, considere o uso da sincronização da Web quando estiver usando a replicação de mesclagem, porque a sincronização da Web elimina a necessidade de uma VPN. Para obter mais informações, consulte [Web Synchronization for Merge Replication](web-synchronization-for-merge-replication.md).  
  
 A VPN inclui um software cliente de modo que os computadores são conectados pela Internet (ou, em casos especiais, até mesmo por uma intranet) a um software em um computador ou um servidor dedicado. Opcionalmente, se utiliza criptografia nas duas extremidades, assim como métodos de autenticação de usuário. A conexão VPN pela Internet opera logicamente como um link WAN (Rede de Longa Distância) entre os sites.  
  
 Uma VPN conecta os componentes de uma rede usando outra rede. Para conectar, o usuário trafega pela Internet ou outra rede pública usando um protocolo como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] PPTP (protocolo de encapsulamento ponto a ponto) ou L2TP (protocolo de encapsulamento de camada 2). Este processo provê a mesma segurança e os recursos previamente apenas disponíveis em uma rede privada. O PPTP é disponível com os sistemas operacionais Microsoft Windows NT versão 4.0 e o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 2000( e versões posteriores); o L2TP é disponível com o Windows 2000 e versões posteriores.  
  
 Para o usuário, a infraestrutura de roteamento intermediário da Internet não é visível e parece que os dados estão sendo enviados por um link privado dedicado. Para os usuários, a VPN é uma conexão ponto a ponto entre o computador do usuário e um servidor corporativo.  
  
 Depois de você ter configurado o seu cliente remoto para conectar usando uma VPN e o cliente tenha acesso à Internet e se registre à LAN corporativa, você pode configurar a replicação como se o cliente remoto estivesse conectado diretamente na LAN. Por motivos de segurança, é possível ter diferentes recursos de rede disponíveis aos usuários conectados pela VPN e àqueles conectados diretamente pela LAN.  
  
 Para obter mais informações sobre a configuração de uma VPN, consulte a documentação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação na Internet](replication-over-the-internet.md)  
  
  
