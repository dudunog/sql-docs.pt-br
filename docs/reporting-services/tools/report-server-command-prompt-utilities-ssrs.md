---
title: Utilitários de prompt de comando do servidor de relatório | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- rsconfig utility
- components [Reporting Services], command line utilities
- rs utility
- command prompt utilities [Reporting Services]
- rskeymgmt utility
ms.assetid: 68f2f9f4-f894-40ff-a71c-f9756bf4b68c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: db8be061664d720ba3be1a4f66ed05062bb1af21
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77081922"
---
# <a name="report-server-command-prompt-utilities-ssrs"></a>Utilitários de prompt de comando do servidor de relatório (SSRS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] inclui vários utilitários de linha de comando que podem ser usados para administrar um servidor de relatório. Esses utilitários são instalados automaticamente ao instalar um servidor de relatórios.  
  
|Nome|Arquivo de comandos|Modo de implantação com suporte|DESCRIÇÃO|  
|----------|------------------|-------------------------------|-----------------|  
|Utilitário RSS|rs.exe|Modo nativo e modo do SharePoint. A versão [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] introduziu suporte ao modo do SharePoint.|O [utilitário rs](../../reporting-services/tools/rs-exe-utility-ssrs.md) é um host de script que pode ser usado para executar operações de script. Use essa ferramenta para executar scripts do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] que copiam dados entre os bancos de dados do servidor de relatório, publicam relatórios, criam itens em um banco de dados do servidor de relatório e outras funções. Para saber mais sobre como usar scripts para administrar um servidor, consulte [Implantação de script e tarefas administrativas](../../reporting-services/tools/script-deployment-and-administrative-tasks.md).|  
|Cmdlets do PowerShell||Apenas SharePoint|Para obter uma lista dos cmdlets do PowerShell, consulte [PowerShell cmdlets for Reporting Services SharePoint Mode](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).|  
|utilitário rsconfig|rsconfig.exe|Apenas nativo|O [utilitário rsconfig](../../reporting-services/tools/rsconfig-utility-ssrs.md) é usado para configurar e gerenciar uma conexão de servidor de relatório com o banco de dados do servidor de relatório. Você também pode usá-lo para especificar uma conta de usuário a ser usada para processamento de relatório autônomo. Para obter mais informações, consulte [Servidor de relatório do Reporting Services &#40;Modo Nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md). Para saber mais sobre a configuração de conexão, consulte [Configurar uma conexão de banco de dados do servidor de relatório &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).|  
|Utilitário rskeymgmt|rskeymgmt.exe|Apenas nativo|O [utilitário rskeymgmt](../../reporting-services/tools/rskeymgmt-utility-ssrs.md) é uma ferramenta de gerenciamento de chaves de criptografia. Você pode usá-lo para fazer backup, aplicar, recriar e excluir chaves simétricas. Você também pode usar essa ferramenta para anexar uma instância do servidor de relatório a um banco de dados do servidor de relatório compartilhado. Rskeymgmt pode ser usado em operações de recuperação de banco de dados. É possível reutilizar um banco de dados existente em uma nova instalação aplicando uma cópia de backup da chave simétrica. Se as chaves não puderem ser recuperadas, essa ferramenta fornecerá uma maneira de excluir o conteúdo criptografado que não é mais usado. Para saber mais sobre o gerenciamento de chaves e o armazenamento de dados confidenciais, consulte [Armazenar dados criptografados do servidor de relatório &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md) e [Configurar e gerenciar chaves de criptografia &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
  
> [!NOTE]  
>  Se você preferir usar uma ferramenta que tenha uma interface gráfica do usuário, poderá usar o Gerenciador de Configurações do Reporting Services, em vez de **rsconfig** e **rskeymgmt**.  
  
## <a name="see-also"></a>Consulte Também  
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   
 [Ferramentas do Reporting Services](../../reporting-services/tools/reporting-services-tools.md)   
 [Servidor de Relatório do Reporting Services &#40;modo nativo&#41;](../../reporting-services/report-server/reporting-services-report-server-native-mode.md)  
  
  
