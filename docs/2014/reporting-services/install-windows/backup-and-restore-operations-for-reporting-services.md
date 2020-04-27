---
title: Operações de backup e restauração para o Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- databases [Reporting Services], backing up
- databases [Reporting Services], restoring
- databases [Reporting Services], moving
- backing up databases [Reporting Services]
- moving databases
- restoring databases [Reporting Services]
- files [Reporting Services], restoring
- files [Reporting Services], backing up
ms.assetid: 157bc376-ab72-4c99-8bde-7b12db70843a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8c992148017f6a3ecb383e85ad5bbfcc3a3ec3c8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108906"
---
# <a name="backup-and-restore-operations-for-reporting-services"></a>Operações de backup e restauração para o Reporting Services
  Este tópico fornece uma visão geral de todos os arquivos de dados usados em uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e descreve quando e como você deve fazer backup dos arquivos. O desenvolvimento de um plano de backup e restauração para os arquivos do banco de dados do servidor de relatório é a parte mais importante de uma estratégia de recuperação. No entanto, uma estratégia de recuperação mais abrangente inclui backups de chaves de criptografia, assemblies ou extensões personalizados, arquivos de configuração e arquivos de origem para relatórios e modelos.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]** Modo nativo do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] | Modo do SharePoint para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
 As operações de backup e restauração são usadas com frequência para mover todo ou parte de uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   Se estiver movendo apenas os bancos de dados do servidor de relatório, poderá usar o backup e restauração ou anexar e desanexar para realocar os bancos de dados em uma instância diferente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Movendo os bancos de dados do servidor de relatório para outro computador &#40;modo nativo do SSRS&#41;](../report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
-   Mover uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para um computador novo é chamado de migração. Quando você migra uma instalação, o Programa de Instalação é executado para instalar uma nova instância do servidor de relatório e, em seguida, os dados da instância são copiados para o novo computador. Para obter mais informações sobre como migrar uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , consulte os seguintes tópicos:  
  
    -   [Atualizar e migrar o Reporting Services](upgrade-and-migrate-reporting-services.md)  
  
    -   [Migrar uma instalação do Reporting Services &#40;modo do SharePoint&#41;](migrate-a-reporting-services-installation-sharepoint-mode.md)  
  
    -   [Migrar uma instalação do Reporting Services &#40;modo nativo&#41;](migrate-a-reporting-services-installation-native-mode.md)  
  
## <a name="backing-up-the-report-server-databases"></a>Fazendo backup dos bancos de dados do servidor de relatório  
 Uma vez que um servidor de relatório é um servidor sem monitoração de estado, os dados de todos os aplicativos são armazenados nos bancos de dados **reportserver** e **reportservertempdb** que são executados em uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Você pode fazer backup dos bancos de dados **reportserver** e **reportservertempdb** que usam um dos métodos com suporte para fazer backup dos bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . As recomendações específicas para os bancos de dados do servidor de relatório incluem:  
  
-   Use o modelo de recuperação completo para fazer backup do banco de dados **reportserver** .  
  
-   Use o modelo de recuperação simples para fazer backup do banco de dados **reportservertempdb** .  
  
-   Você pode usar agendas de backup diferentes para cada banco de dados. O único motivo para fazer backup do **reportservertempdb** é evitar ter que recriá-lo se houver uma falha de hardware. No caso de uma falha de hardware, não é necessário recuperar os dados no **reportservertempdb**, mas você precisará da estrutura da tabela. Se você perder o **reportservertempdb**, o único modo de reverter isso é recriar o banco de dados de servidor de relatório. Se você recriar o **reportservertempdb**, é importante que você tenha o mesmo nome que o banco de dados do servidor de relatório primário.  
  
 Para obter mais informações sobre backup e recuperação dos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados relacionais [Fazer backup e restaurar bancos de dados do SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
> [!IMPORTANT]  
>  Se seu servidor de relatório do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] estiver em modo do SharePoint, haverá bancos de dados adicionais com os quais se preocupar, inclusive bancos de dados de configuração do SharePoint e o banco de dados de alertas do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . No modo do SharePoint, três bancos de dados são criados para cada aplicativo de serviço do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Os bancos de dados **reportserver**, **reportservertempdb**e **dataalerting** . Para obter mais informações, consulte [Aplicativos de serviço SharePoint de backup e restauração do Reporting Services](../backup-and-restore-reporting-services-sharepoint-service-applications.md)  
  
## <a name="backing-up-the-encryption-keys"></a>Fazendo backup das chaves de criptografia  
 Você deve fazer backup das chaves de criptografia ao configurar uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pela primeira vez. Você também deve fazer backup das chaves sempre que alterar a identidade das contas de serviço ou renomear o computador. Para saber mais, confira [Back Up and Restore Reporting Services Encryption Keys](ssrs-encryption-keys-back-up-and-restore-encryption-keys.md). Para servidores de relatório no modo do SharePoint, consulte a seção "gerenciamento de chaves" de [gerenciar um aplicativo de serviço do Reporting Services SharePoint](../manage-a-reporting-services-sharepoint-service-application.md).  
  
## <a name="backing-up-the-configuration-files"></a>Fazendo backup dos arquivos de configuração  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa arquivos de configuração para armazenar as configurações do aplicativo. Você deve fazer backup dos arquivos quando configurar o servidor pela primeira vez e depois de implantar qualquer extensão personalizada. Os arquivos dos quais deve ser feito backup incluem:  
  
-   RSReportServer.config  
  
-   Rssvrpolicy.config  
  
-   Rsmgrpolicy.config  
  
-   Reportingservicesservice.exe.config  
  
-   Web.config para os aplicativos Servidor de Relatório e Gerenciador de Relatórios do [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]  
  
-   Machine.config para [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]  
  
## <a name="backing-up-data-files"></a>Fazendo backup de arquivos de dados  
 Faça backup dos arquivos criados e mantidos no Designer de Relatórios e Designer de Modelos. Eles incluem arquivos de definição de relatórios (.rdl), arquivos de modelo de relatórios (.smdl), arquivos de fontes de dados compartilhadas (.rds), arquivos de exibição de dados (.dv), arquivos de fonte de dados (.ds), arquivos de projeto do servidor de relatório (.rptproj) e arquivos de solução de relatórios (.sln).  
  
 Lembre-se de fazer backup de qualquer arquivo de script (.rss) criado para as tarefas de administração ou implantação.  
  
 Verifique se você tem uma cópia de backup de todas as extensões e assemblies personalizados que você está usando.  
  
## <a name="see-also"></a>Consulte Também  
 [Banco de dados do servidor de relatório &#40;modo nativo do SSRS&#41;](../report-server/report-server-database-ssrs-native-mode.md)   
 [Arquivos de configuração do Reporting Services](../report-server/reporting-services-configuration-files.md)   
 [Utilitário rskeymgmt &#40;SSRS&#41;](../tools/rskeymgmt-utility-ssrs.md)   
 [Copiar bancos de dados com backup e restauração](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [Administrar um banco de dados do servidor de relatório &#40;modo nativo do SSRS&#41;](../report-server/administer-a-report-server-database-ssrs-native-mode.md)   
 [Configurar e gerenciar chaves de criptografia &#40;SSRS Configuration Manager&#41;](ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
