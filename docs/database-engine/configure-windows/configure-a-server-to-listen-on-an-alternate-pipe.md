---
title: Configurar um servidor para escutar em um pipe alternativo | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Named Pipes [SQL Server], configuring
- listening [SQL Server], pipes
- pipes [SQL Server], alternate
- alternate pipes [SQL Server]
ms.assetid: 914f7491-e2be-4b0d-b3aa-fe5409cdbafa
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: fd7a0ebf16733109e59aac74652d90e0b63a1d9d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68012914"
---
# <a name="configure-a-server-to-listen-on-an-alternate-pipe"></a>Configurar um servidor para escutar em um pipe alternativo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Este tópico descreve como configurar um servidor para escutar em um pipe alternativo no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o SQL Server Configuration Manager. Por padrão, a instância padrão do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] escuta em um pipe chamado \\\\.\pipe\sql\query. As instâncias nomeadas do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e do [!INCLUDE[ssEW](../../includes/ssew-md.md)] escutam em outros pipes.  
  
 Há três modos de se conectar a um pipe nomeado específico com um aplicativo cliente:  
  
-   Execute o serviço de navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no servidor.  
  
-   Crie um alias no cliente, especificando o pipe nomeado.  
  
-   Programe o cliente para se conectar usando uma cadeia de conexão personalizada.  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> Usando o SQL Server Configuration Manager  
  
#### <a name="to-configure-the-named-pipe-used-by-the-sql-server-database-engine"></a>Configurar o pipe nomeado usado pelo Mecanismo de Banco de Dados do SQL Server  
  
1.  No SQL Server Configuration Manager, no painel do console, expanda **Configuração de Rede do SQL Server** e, em seguida, clique nela para expandir **Protocolos de** *\<nome da instância>* .  
  
2.  No painel de detalhes, clique com o botão direito do mouse em **Pipes Nomeados**e clique em **Propriedades**.  
  
3.  Na guia **Protocolo** , na caixa **Nome do Pipe** , digite o pipe no qual você deseja que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] escute e clique em **OK**.  
  
4.  No painel do console, clique em **Serviços do SQL Server**.  
  
5.  No painel de detalhes, clique com o botão direito do mouse em **SQL Server (** \<instance name> **)** e, depois, clique em **Reiniciar** para parar e reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está escutando em um pipe alternativo, há três modos de se conectar a um pipe nomeado específico com um aplicativo cliente:  
  
-   Execute o serviço de navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no servidor.  
  
-   Crie um alias no cliente, especificando o pipe nomeado.  
  
-   Programe o cliente para se conectar usando uma cadeia de conexão personalizada.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar ou excluir um alias de servidor para ser usado por um cliente &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/create-or-delete-a-server-alias-for-use-by-a-client.md)   
 [Configuração de rede do servidor](../../database-engine/configure-windows/server-network-configuration.md)  
  
  
