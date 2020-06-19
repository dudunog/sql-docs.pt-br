---
title: Iniciar o Monitor de Espelhamento de Banco de Dados (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- monitoring database mirroring [SQL Server]
- Database Mirroring Monitor [SQL Server], starting
- database mirroring [SQL Server], monitoring
ms.assetid: 53165335-97ca-4f88-8e78-22f1839dee98
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 807473ab743ed63acea8f18075f21ec09249bd45
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933907"
---
# <a name="start-database-mirroring-monitor-sql-server-management-studio"></a>Iniciar o Monitor de Espelhamento de Banco de Dados (SQL Server Management Studio)
  O Monitor de Espelhamento de Banco de Dados faz parte do Monitor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que é inicializado a partir do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!NOTE]  
>  O Monitor de Espelhamento de Banco de Dados não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
### <a name="to-launch-the-database-mirroring-monitor"></a>Para iniciar o Monitor de Espelhamento de Banco de Dados  
  
1.  Depois de se conectar à instância do servidor principal, no Pesquisador de Objetos, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda os **Bancos de Dados**e selecione o banco de dados a ser monitorado.  
  
3.  Clique com o botão direito do mouse no banco de dados, selecione **Tarefas**e clique em **Iniciar o Monitor de Espelhamento de Banco de Dados**.  
  
4.  Na caixa de diálogo **Monitor de Espelhamento de Banco de Dados** , clique em **Registrar Banco de Dados Espelho** para registrar um ou mais bancos de dados espelho.  
  
    > [!NOTE]  
    >  Ao registrar um banco de dados em um parceiro, o banco de dados será automaticamente registrado no outro parceiro. Se o monitor já tiver credenciais de conexão para a outra instância de parceiro, elas serão usadas para a conexão. Caso contrário o monitor tentará conectar usando a Autenticação do Windows. Se você quiser alterar as credenciais usadas para conectar-se a qualquer instância de servidor, clique em **Mostrar a caixa de diálogo Gerenciar de conexões do servidor quando eu clicar em OK**.  
  
 Para obter mais informações sobre o Monitor de Espelhamento de Banco de Dados, veja [Visão geral do Monitor de Espelhamento de Banco de Dados](database-mirroring-monitor-overview.md).  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server de espelhamento de banco de dados &#40;&#41;](database-mirroring-sql-server.md)   
 [Estabelecer uma sessão de espelhamento de banco de dados usando a Autenticação do Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
  
