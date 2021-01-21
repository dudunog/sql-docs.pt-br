---
title: Implantação e suporte de versão no SSDT (SQL Server Data Tools) | Microsoft Docs
description: Saiba mais sobre as versões compatíveis para criar e publicar relatórios no SQL Server Data Tools e como definir as propriedades de configuração e implantação do projeto.
ms.date: 03/15/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
ms.assetid: 36f5686d-7e40-4f31-be81-bd197ca33a02
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c820c7a9e0cefaee2a22a401213754d0a3274152
ms.sourcegitcommit: d8cdbb719916805037a9167ac4e964abb89c3909
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/20/2021
ms.locfileid: "98596171"
---
# <a name="deployment-and-version-support-in-sql-server-data-tools-ssdt"></a>Implantação e suporte de versão no SSDT (SQL Server Data Tools)
  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] oferece suporte aos seguintes cenários:  
  
-   Abra as definições de relatório (*.rdl) e os projetos do servidor de relatório (\*.rptproj).  
  
-   Criar definições de relatório.  
  
-   Visualizar relatórios no Designer de Relatórios.  
  
-   Implantar relatórios nos servidores de relatório.  
  
##  <a name="configuration-and-deployment-properties"></a><a name="bkmk_ConfigurationandDeploymentProperties"></a> Propriedades e configuração e de implantação  
 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] dá suporte a configurações de projeto. Uma configuração de projeto consiste em um conjunto de propriedades que especificam locais e comportamentos quando um projeto é compilado como uma etapa de visualização ou implantação de relatórios. Para saber mais sobre configurações de projeto, consulte a documentação do Visual Studio.  
  
 Use as configurações de projeto para controlar a atualização de definições de relatório para versões de esquema compatíveis com os servidores de relatório de destino. As propriedades controladas por configurações de projeto incluem o servidor de relatório de destino, a pasta onde o processo de compilação armazena temporariamente as definições de relatórios para visualização e implantação e os níveis de erro.  
  
 Relatórios são compilados antes de serem renderizados como visualizações no Designer de Relatórios ou implantados no servidor de relatório.  
  
 Defina as propriedades de configuração na caixa de diálogo [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] **Propriedade do Projeto**.  
  
 As propriedades de compilação e implantação incluem:  
  
-   OutputPath é uma propriedade de build que identifica o caminho de pastas para armazenar a definição de relatório usada na verificação de build, na implantação e na visualização de relatórios.  
  
-   ErrorLevel é uma propriedade de build que identifica a severidade dos problemas de build relatados como erros. Problemas com níveis de severidade menor ou igual ao valor ErrorLevel são relatados como erros; caso contrário, os problemas são relatados como avisos. Para obter mais informações, confira a seção "Validação de relatório e níveis de erro" em [Criar relatórios com o Designer de Relatórios &#40;SSRS&#41;](../../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
-   TargetServerVersion é uma propriedade de implantação que identifica a versão esperada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que está instalada no servidor de relatório de destino especificado na propriedade TargetServerURL.  
  
 Quando você especifica a versão anterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] na caixa de diálogo **Propriedade do Projeto**, os relatórios não são revertidos automaticamente para a versão anterior. Dessa forma, um projeto do Servidor de Relatórios pode conter relatórios de duas versões diferentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Quando o projeto do Servidor de Relatório é implantado, todos os relatórios do projeto são convertidos para a versão especificada em TargetServerVersion.  
  
 Você pode adicionar mais de uma configuração de projeto a um projeto; cada uma é usada para um cenário diferente, como, por exemplo, implantação de versões diferentes de servidores de relatório. Para obter mais informações, consulte [Definir as propriedades da implantação &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md) e [Caixa de diálogo Páginas de Propriedades do Projeto](../../reporting-services/tools/project-property-pages-dialog-box.md).  
  
##  <a name="supported-versions"></a><a name="bkmk_SupportedVersions"></a> Versões com suporte  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], o ambiente de desenvolvimento de 32 bits para projetos do Servidor de Relatório, não foi projetado para execução em computadores baseados em [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)] e não é instalado em servidores baseados em [!INCLUDE[vcpritanium](../../includes/vcpritanium-md.md)]. Porém, o suporte para o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] está disponível em computadores baseados em x64.  
  
 A tabela a seguir descreve as versões com suporte para criação e publicação de relatórios em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
> [!NOTE]  
>  O esquema não foi alterado desde o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
|Tipo de Projeto ou Arquivo|Versão|Criar Relatórios|Publicar Relatórios|Observações|  
|--------------------------|-------------|--------------------|---------------------|-----------|  
|Projeto do Servidor de Relatório<br /><br /> ou<br /><br /> Projeto do Assistente do Servidor de Relatórios|[!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]|Esquema 2016 RDL|[!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]||  
|Projeto do Servidor de Relatório<br /><br /> ou<br /><br /> Projeto do Assistente do Servidor de Relatórios|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|Esquema 2014 RDL|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Projeto do Servidor de Relatório<br /><br /> ou<br /><br /> Projeto do Assistente do Servidor de Relatórios|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|Esquema 2012 RDL|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Projeto do Servidor de Relatório<br /><br /> ou<br /><br /> Projeto do Assistente do Servidor de Relatórios|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]|Esquema do 2008 R2 RDL|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]||  
|Projeto do Servidor de Relatório<br /><br /> ou<br /><br /> Projeto do Assistente do Servidor de Relatórios|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|Esquema 2008 RDL|Somente servidor de relatório [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Atualiza o 2003 RDL e o 2005 RDL localmente para o esquema 2008 RDL.|  
  
 Para obter mais informações sobre como abrir relatórios em uma versão anterior do esquema de definição de relatório, consulte [Atualizar relatórios](../../reporting-services/install-windows/upgrade-reports.md). Para obter mais informações sobre esquemas de definição de relatório específicos, consulte [Especificação de linguagem RDL](/openspecs/sql_server_protocols/ms-rdl/53287204-7cd0-4bc9-a5cd-d42a5925dca1).  
  
## <a name="see-also"></a>Consulte Também  
 [Publicar fontes de dados e relatórios](../../reporting-services/reports/publishing-data-sources-and-reports.md)  
  
