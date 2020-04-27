---
title: Atualizar um banco de dados do servidor de relatório | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- upgrading databases
- report server database
- upgrading Reporting Services
ms.assetid: 4091cf87-9d97-4048-a393-67f1f9207401
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e3ba4d9ee2e0b92617c2d2bcadae3bf87c8b5414
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108635"
---
# <a name="upgrade-a-report-server-database"></a>Atualizar um banco de dados do servidor de relatório
  O banco de dados do servidor de relatório fornece armazenamento para uma ou mais instâncias do servidor de relatório. Como o esquema do banco de dados do servidor de relatório pode ser alterado a cada versão nova do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], é necessário que a versão do banco de dados corresponda à versão da instância do servidor de relatório que você está usando. Na maioria dos casos, um banco de dados do servidor de relatório pode ser atualizado automaticamente sem ação específica de sua parte.  
  
 **Modo nativo:** No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo nativo, o banco de dados do servidor de relatório é realmente composto de dois bancos de dados que têm nomes padrão "ReportServer e ReportServerTempDB".  
  
 **Modo do SharePoint:** No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modo do SharePoint, o banco de dados do servidor de relatório é, na verdade, uma coleção de bancos que [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é criada para cada instância do aplicativo de serviço.  
  
## <a name="ways-to-upgrade-a-native-mode-report-server-database"></a>Maneiras de atualizar um banco de dados do servidor de relatório de modo nativo  
 A seguinte lista identifica as condições nas quais um banco de dados do servidor de relatório é atualizado:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atualiza uma única instância de um servidor de relatório. O esquema de banco de dados do servidor de relatório é atualizado automaticamente após a inicialização do serviço, e o servidor de relatório determina que a versão do esquema de banco de dados não corresponde à do servidor.  
  
     Durante a inicialização do serviço, o servidor de relatório verifica se a versão do esquema de banco de dados corresponde à versão do servidor. Se a versão do esquema de banco de dados for mais antiga, ela será atualizada automaticamente para a versão de esquema exigida pelo servidor de relatório. A atualização automática é especialmente útil se você restaurou ou anexou um banco de dados de servidor de relatório mais antigo. Uma mensagem é inserida no arquivo de log de rastreamento do servidor de relatório, indicando que a versão do esquema de banco de dados foi atualizada.  
  
-   O Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] atualiza um banco de dados do servidor de relatório local ou remoto quando você seleciona uma versão mais antiga a ser usada com uma instância mais recente do servidor de relatório. Nesse caso, você deve confirmar a ação de atualização antes que ela aconteça.  
  
     O Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não fornece mais um botão Atualizar separado ou um script de atualização. Esses recursos ficaram obsoletos a partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] devido ao recurso de atualização automática do serviço Servidor de Relatório.  
  
 Depois que o esquema for atualizado, você não poderá reverter a atualização para uma versão anterior. Sempre faça backup do banco de dados do servidor de relatório, caso precise recriar uma instalação anterior.  
  
## <a name="how-the-schema-metadata-and-report-server-content-is-updated"></a>Como o esquema, os metadados e o conteúdo do servidor de relatório são atualizados  
 O banco de dados do servidor de relatório é atualizado em três estágios:  
  
1.  O esquema é atualizado automaticamente após a instalação e a inicialização do serviço ou quando você seleciona um banco de dados do servidor de relatório do modo nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Gerenciador de Configurações do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que é uma versão antiga. Além disso, o serviço do Servidor de Relatório verifica a versão do banco de dados durante a inicialização. Se o servidor de relatório estiver conectado a um banco de dados que seja de uma versão anterior, o servidor de relatório atualizará o banco de dados durante a inicialização.  
  
2.  Os descritores de segurança são atualizados durante o primeiro uso do banco de dados do servidor de relatório após a atualização do esquema.  
  
3.  Os relatórios publicados e os instantâneos de relatório compilados são atualizados durante o primeiro uso. Para obter mais informações, consulte [Upgrade Reports](upgrade-reports.md).  
  
 Além do banco de dados do servidor de relatório, um servidor de relatório também usa um banco de dados temporário. O banco de dados temporário é atualizado automaticamente quando você atualiza o banco de dados do servidor de relatório.  
  
## <a name="permissions-required-to-upgrade-a-report-server-database"></a>Permissões necessárias para atualizar um banco de dados do Servidor de Relatório  
 Se você estiver atualizando uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que contenha um banco de dados do servidor de relatório, poderá ver uma mensagem de erro se a atualização de banco de dados for executada com permissões insuficientes. Por padrão, a Instalação usa o token de segurança do usuário que está executando o programa Instalação para se conectar à instância remota do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e atualizar o esquema. Se você tiver permissões [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **sysadmin** no servidor de banco de dados que hospeda os bancos de dados do servidor de relatório, a atualização do banco de dados será bem-sucedida. Da mesma maneira, se você executar a Instalação no prompt de comando e especificar os argumentos RSUPGRADEDATABASEACCOUNT e RSUPGRADEPASSWORD para uma conta que tem a permissão de **sysadmin** para modificar o esquema no computador remoto, a atualização do banco de dados será bem-sucedida.  
  
 Todavia, se você não tiver permissão de **sysadmin** no banco de dados do computador remoto, a conexão será recusada com o seguinte erro:  
  
 `"Setup was not able to upgrade the report server database schema. You must update the database schema manually after setup is finished. To update the schema, run the Reporting Services Configuration Manager, open the Database Setup page, re-select the database, and click Apply. The database will be upgraded automatically."`  
  
 Nesse ponto, os arquivos de programas do servidor de relatório serão atualizados, mas o banco de dados do servidor de relatório estará no formato da versão anterior. O servidor de relatório ficará indisponível até que você conclua o processo de atualização por meio da atualização manual do banco de dados.  
  
#### <a name="to-upgrade-a-native-mode-database-with-scripts"></a>Para atualizar um banco de dados de modo nativo com scripts  
 Você pode usar scripts do WMI para atualizar um banco de dados do servidor de relatórios. Para obter mais informações, consulte [Método GenerateDatabaseUpgradeScript &#40;WMI MSReportServer_ConfigurationSetting&#41;](../wmi-provider-library-reference/configurationsetting-method-generatedatabaseupgradescript.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Criar um banco de dados do servidor de relatório &#40;Configuration Manager SSRS&#41;](../../sql-server/install/create-a-report-server-database-ssrs-configuration-manager.md)   
 [Assistente para alterar banco de dados &#40;modo nativo do SSRS&#41;](../../sql-server/install/change-database-wizard-ssrs-native-mode.md)   
 [Atualizar e migrar Reporting Services](upgrade-and-migrate-reporting-services.md)   
 [Migrar uma instalação do Reporting Services &#40;modo nativo&#41;](migrate-a-reporting-services-installation-native-mode.md)  
  
  
