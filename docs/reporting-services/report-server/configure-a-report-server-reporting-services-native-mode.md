---
title: Configurar um servidor de relatório (modo nativo do Reporting Services) | Microsoft Docs
ms.date: 06/18/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
helpviewer_keywords:
- report server configuration
- report servers [Reporting Services], configuring
ms.assetid: ef84ce9d-9156-48e9-8073-7e0535476932
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5723122c76b02900f6906c03efb807e58ebcc6d9
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67313977"
---
# <a name="configure-a-report-server-reporting-services-native-mode"></a>Configurar um servidor de relatórios (modo nativo do Reporting Services)
  Dependendo das opções selecionadas durante a instalação, o Servidor de Relatórios possivelmente exigir uma configuração adicional para que você possa usá-lo. A configuração de um servidor de relatório é formada no mínimo por estes itens:  
  
-   Uma conta do serviço Servidor de Relatórios (configurada durante a instalação).  
  
-   Uma URL de serviço Web que dá acesso ao servidor de relatório.  
  
-   Um banco de dados de servidor de relatório que armazena dados de aplicativo, relatórios e outros itens.  
  
 A Instalação define as configurações mínimas quando você seleciona uma das seguintes opções: configuração padrão do modo Nativo ou configuração padrão do modo integrado do SharePoint. Se você tiver instalado o servidor de relatório no modo somente arquivos (a opção **Instalar, mas não configurar** do assistente de Instalação), será configurada apenas a conta de serviço. A URL do serviço Web e o banco de dados do servidor de relatório devem ser configurados após o término da instalação.  
  
É recomendável configurar o portal da Web para que você possa permitir acesso de usuário ao servidor de relatório e gerenciar o conteúdo do servidor de relatório. Se você implantar um servidor de relatório no modo integrado do SharePoint, use o front-end da Web de um servidor SharePoint para conceder acesso.  
  
 Recursos adicionais, como e-mail de servidor de relatório e a conta de execução autônoma, podem ser configurados conforme necessário. Para obter mais informações, consulte [Gerenciar um servidor de relatório de modo nativo do Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md).  
  
 Para configurar um servidor de relatório, use a ferramenta Configuração do Reporting Services.  
  
## <a name="to-minimally-configure-a-report-server-installation"></a>Para definir a configuração mínima de uma instalação de servidor de relatório  
  
1.  Inicie a ferramenta Configuração do Reporting Services e conecte-se à instância do servidor de relatório. Para obter instruções, veja [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).  
  
2.  Clique em **URL do Serviço da Web** para abrir a página e configurar uma URL para o servidor de relatório. Para obter instruções sobre como definir a URL, consulte [Configurar uma URL &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md).  
  
3.  Clique em **Banco de Dados** para criar o banco de dados do servidor de relatório. Para obter instruções, consulte [Criar um banco de dados de servidor de relatório no modo nativo &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
4.  Volte à página **URL do Serviço da Web** e clique na URL para verificar se ela está funcionando.  
  
5.  Siga as instruções descritas em "Próximas etapas" para concluir a implantação.  
  
## <a name="next-steps"></a>Próximas etapas  
 Para concluir a implantação, configure o portal da Web ou a integração com o SharePoint. Para obter mais informações, confira [Configurar o portal da Web](../../reporting-services/report-server/configure-web-portal.md).  
  
 Se o Firewall do Windows estiver ativado, a porta que o servidor de relatório está configurado para usar provavelmente estará fechada. Uma indicação de que uma porta pode estar fechada é uma página em branco quando você tenta abrir o portal da Web em um computador cliente remoto. Para obter informações sobre como configurar o firewall, consulte [Configure a Firewall for Report Server Access](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
 Se você estiver usando o Windows Vista ou o Windows Server 2008, etapas adicionais serão necessárias para abrir o portal da Web localmente. Para obter mais informações, consulte [Configurar um servidor de relatório no modo nativo para a Administração Local &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
 Verifique a instalação criando pastas, carregando itens e executando relatórios. Siga as instruções em [Verificar uma instalação do Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md) para verificar a instalação.  
  
## <a name="see-also"></a>Confira também  
 [Gerenciar um servidor de relatório de modo nativo do Reporting Services](../../reporting-services/report-server/manage-a-reporting-services-native-mode-report-server.md)   
 [Configurar um firewall para acesso ao servidor de relatório](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)   
 [Configurar um servidor de relatório no modo nativo para administração local &#40;SSRS&#41;](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)   
 [Configurar um servidor de relatório para administração remota](../../reporting-services/report-server/configure-a-report-server-for-remote-administration.md)   
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  
  
