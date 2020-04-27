---
title: Conectar-se a qualquer componente de SQL Server da SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- connections [SQL Server], SQL Server Management Studio
- saving connections
- components [SQL Server], connections
- SQL Server Management Studio [SQL Server], connections
ms.assetid: 5eeb41bd-b25b-4d3b-a005-a7d9e4b5978e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 342624645e9bd88d0a7afd08b3c18225fc2c14ce
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63245376"
---
# <a name="connect-to-any-sql-server-component-from-sql-server-management-studio"></a>Conectar a qualquer componente do SQL Server a partir do SQL Server Management Studio
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece funcionalidade para gerenciar todos os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Use o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para se conectar a:  
  
-   Uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Apesar de o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] permitir que você trabalhe com consultas sem primeiro estabelecer uma conexão com uma fonte de dados, a maioria das outras tarefas requer uma conexão. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] fornece a caixa de diálogo **Conectar ao Servidor** para configurar propriedades de conexão com componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] é iniciado, a caixa de diálogo **Conectar ao Servidor** é exibida e solicita a conexão com um servidor. A caixa de diálogo **Conectar ao Servidor** retém as configurações de conexão da última vez que foi utilizada.  
  
> [!NOTE]  
>  Esse recurso pode ser desativado de forma que nenhuma conexão seja iniciada automaticamente. Para obter mais informações, consulte [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
## <a name="saving-connections"></a>salvando conexões  
 Você pode salvar conexões com servidores específicos em Servidores Registrados ou pode salvar conexões em projetos com o Gerenciador de Soluções.  
  
### <a name="saving-connections-in-registered-servers"></a>Salvando conexões em Servidores Registrados  
 Ao registrar um servidor, o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] salva as informações de conexão em Servidores Registrados. Para conectar a um servidor registrado, clique duas vezes no nome do servidor em Servidores Registrados. O Pesquisador de Objetos abre uma conexão com o servidor.  
  
### <a name="saving-connections-in-solution-explorer"></a>Salvando conexões no Gerenciador de Soluções  
 O Gerenciador de Soluções permite o armazenamento de consultas relacionadas, scripts, conexões e outras informações associadas em um projeto. Cada projeto de script contém um nó denominado **Conexões**, no qual você pode salvar uma ou mais conexões. Para adicionar uma conexão, clique com o botão direito do mouse em **Conexões**e clique em **Nova Conexão**. Para acessar uma conexão salva, expanda **Conexões** e clique duas vezes na conexão. [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] abre uma janela de consulta associada àquela conexão. Quando salvos, os scripts retêm sua associação com uma conexão específica.  
  
## <a name="see-also"></a>Consulte Também  
 [Usar SQL Server Management Studio](../sql-server-management-studio-ssms.md)   
 [Pesquisador de Objetos](../object/object-explorer.md)  
  
  
