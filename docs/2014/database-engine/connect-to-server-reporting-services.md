---
title: Conectar ao servidor (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.connection.login.reportserver.f1
ms.assetid: ef81b658-8eb5-4636-ac81-eead10cc7b9f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 41e0ca3ee7ccaa7bb57e5667092c0660e35c4c52
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62808673"
---
# <a name="connect-to-server-reporting-services"></a>Conectar ao Servidor (Reporting Services)
  Use essa caixa de diálogo para exibir ou especificar opções ao se conectar ao [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
## <a name="options"></a>Opções  
 **Tipo de servidor**  
 Ao registrar um servidor do pesquisador de **objetos**, selecione o tipo de servidor ao qual se [!INCLUDE[ssDE](../includes/ssde-md.md)]conectar:, Analysis Services, Reporting Services ou Integration Services. O restante da caixa de diálogo mostra somente as opções que válidas ao tipo de servidor selecionado. Ao registrar um servidor de **servidores registrados**, a caixa **tipo de servidor** é somente leitura e corresponde ao tipo de servidor exibido no componente **servidores registrados** . Para registrar um tipo diferente de servidor, selecione [!INCLUDE[ssDE](../includes/ssde-md.md)], Analysis Services, Reporting Services ou Integration Services na barra de ferramentas **servidores registrados** antes de iniciar o registro de um novo servidor.  
  
 **Nome do servidor**  
 O modo de servidor da instância de servidor de relatório à qual você está se conectando determina o valor que você deve inserir.  
  
 Para um servidor de relatório executado no modo nativo, especifique a instância do servidor de relatório à qual se conectar. Se você estiver usando a instância padrão, geralmente, o nome do servidor será o nome do computador. Se você instalou uma instância nomeada, acrescente o nome da instância ao nome do servidor neste formato: \<servername \\><\>InstanceName. O Reporting Services usa o caractere de barra invertida para delimitar o nome da instância.  
  
 Para um servidor de relatório executado no SharePoint em modo integrado, especifique um site do SharePoint. Você pode especificar qualquer site de uma coleção de sites que foi integrada ao [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. O URL que você fornecer deve incluir o HTTP ou prefixo HTTPS. Você deve ter permissão para acessar o site do SharePoint para se conectar a ele no Management Studio. O nível de permissão que foi atribuído a você determinará quais itens você pode exibir e gerenciar. Para obter mais informações, consulte [Conectar-se a um servidor de relatório no Management Studio](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md).  
  
 **Autenticação**  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] pode ser configurado para aceitar solicitações de Autenticação do Windows ou de Autenticação de formulários que são manipulados por uma extensão de autenticação personalizada fornecida por você. Selecione um dos seguintes modos de autenticação ao se conectar ao [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]:  
  
 **Modo de Autenticação do Windows (Autenticação do Windows)**  
 Conecte-se à instância de servidor de relatório usando as credenciais do [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows.  
  
 **Autenticação básica**  
 Conecte-se usando a **Autenticação Básica** se a instalação do Reporting Services estiver configurada para usar a Autenticação Básica.  
  
 **Autenticação de Formulários**  
 Conecte-se usando a **Autenticação de Formulários** se a instalação do Reporting Services estiver configurada para usar uma extensão de autenticação personalizada.  
  
 **Nome de usuário**  
 Digite o nome de logon a ser usado na conexão. Essa opção estará disponível somente se você selecionou **Básica** ou **Autenticação de Formulários**.  
  
 **Senha**  
 Digite a senha para o nome de usuário. Essa opção só poderá ser editada se você selecionou **Básica** ou **Autenticação de Formulários**.  
  
 **Connect**  
 Clique para conectar-se com o servidor selecionado acima.  
  
 **Opções**  
 Clique para exibir opções de conexão de servidor adicionais, como registrar um servidor e lembrar a senha.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar uma conexão de banco de dados do servidor de relatório &#40;Configuration Manager SSRS&#41;](../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Conectar-se a um servidor de relatório no Management Studio](../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Autenticação com o servidor de relatório](../reporting-services/security/authentication-with-the-report-server.md)  
  
  
