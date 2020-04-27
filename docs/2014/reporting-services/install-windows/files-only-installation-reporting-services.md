---
title: Instalação somente de arquivos (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- files-only installation [Reporting Services]
- installation options [Reporting Services]
ms.assetid: bdc74a8f-046c-4aa0-bfbd-4f1711dfb9ce
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a854de693bce88fcba0de2f1c08e4b0fe296b512
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108838"
---
# <a name="files-only-installation-reporting-services"></a>Instalação somente de arquivos (Reporting Services)
  O termo*instalação somente de arquivos* refere-se a uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] em que a instalação cria a estrutura de pastas para os arquivos de programas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , copia os arquivos para o disco, registra o serviço Servidor de Relatório no computador local, configura a conta de serviço, concede permissões de arquivo a essa conta e registra o provedor WMI do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Uma instalação somente de arquivos inclui os seguintes recursos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] : serviço Servidor de Relatório (que hospeda o serviço Web Servidor de Relatório, o aplicativo de processamento em segundo plano e o Gerenciador de Relatórios), Construtor de Relatórios, a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e os utilitários de linha de comando do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (rsconfig.exe, rskeymgmt.exe e rs.exe). Ela não se aplica a recursos compartilhados, como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], que deverão ser especificados como itens separados se você quiser instalá-los.  
  
 Diferentemente de outros modos de instalação, um servidor de relatório que é instalado no modo somente arquivos não estará operacional quando a Instalação for concluída. Será necessária a configuração adicional para colocar o servidor de relatório online usando o [Gerenciador de Configurações do Reporting Services &#40;Modo Nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="when-to-select-files-only-installation-mode"></a>Quando selecionar o modo de instalação somente arquivos  
 Uma instalação somente arquivos deve ser executada quando:  
  
-   Você deseja conectar o servidor de relatório a um banco de dados de servidor de relatório remoto.  
  
-   Você deseja instalar o servidor de relatório como uma instância nomeada.  
  
-   Você tem requisitos de implantação que incluem o uso de configurações ou funcionalidade personalizada, e deseja controle total sobre quando e como o servidor é configurado.  
  
-   Instalar um cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que inclua o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="how-to-perform-a-files-only-installation"></a>Como executar uma instalação somente arquivos  
 A instalação somente de arquivos é o padrão para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 Você pode especificar uma instalação somente arquivos pela linha de comando ou no Assistente de Instalação. Os tópicos a seguir fornecem instruções passo a passo:  
  
-   [Instale o SQL Server 2014 do assistente de instalação &#40;&#41;de ](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)instalação.  
  
-   [Instale o SQL Server 2014 no prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
#### <a name="example-command-line-script"></a>Exemplo de script de linha de comando  
 Para maior clareza, o exemplo inclui /RSINSTALLMODE="FilesOnlyMode". Entretanto, como o modo somente arquivos é o padrão, você pode omitir isso e ainda obter uma instalação no modo somente arquivos.  
  
```  
setup /q /ACTION=install /FEATURES=RS /InstanceName=MSSQLSERVER /RSSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE" /RSINSTALLMODE="FilesOnlyMode"  
```  
  
#### <a name="installation-wizard"></a>Assistente de instalação  
 Quando você seleciona [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] na página Seleção de Recursos, a instalação apresenta uma página Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que permite especificar o modo de instalação. Para especificar uma instalação somente de arquivos, selecione **Instalar, mas não configurar o servidor de relatório** na página Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Verificar uma instalação do Reporting Services](verify-a-reporting-services-installation.md)   
 [Configurar a conta de serviço do servidor de relatório &#40;SSRS Configuration Manager&#41;](configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Configurar as URLs do servidor de relatório &#40;SSRS Configuration Manager&#41;](configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurar uma conexão de banco de dados do servidor de relatório &#40;Configuration Manager SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Reporting Services a instalação do modo do SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41;](install-reporting-services-sharepoint-mode.md)   
 [Instalar o servidor de relatórios de modo nativo do Reporting Services](install-reporting-services-native-mode-report-server.md)   
 [Ferramentas do Reporting Services](../tools/reporting-services-tools.md)  
  
  
