---
title: Recursos preteridos do SQL Server Reporting Services no SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, backward compatibility
- deprecated features [Reporting Services]
- HTML OWC rendering extension [Reporting Services]
- Report Server Web service, endpoints
ms.assetid: 3876c01e-f81d-4cce-9104-5106a8c369e6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d5cbef64cbed910018e7d2f8dae1844074aaa3f5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109348"
---
# <a name="deprecated-features-in-sql-server-reporting-services-in-sql-server-2014"></a>Recursos preteridos no SQL Server Reporting Services do SQL Server 2014
  Este tópico descreve os recursos preteridos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] . Os recursos ainda estão disponíveis na versão em que foram preteridos; porém, os recursos estão agendados para ser removidos em uma versão futura do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Recursos preteridos não devem ser usados em aplicativos novos.  
  
 Neste tópico:  
  
-   [Recursos preteridos no SQL Server 2014 Reporting Services](#bkmk_2014)  
  
-   [Recursos preteridos no SQL Server 2012 SP1 Reporting Services](#bkmk_2012sp1)  
  
-   [Recursos preteridos no SQL Server 2012 Reporting Services](#bkmk_2012)  
  
-   [Recursos preteridos no SQL Server 2008 R2 Reporting Services](#bkmk_kj)  
  
##  <a name="sql-server-2014-reporting-services-deprecated-features"></a><a name="bkmk_2014"></a>SQL Server 2014 Reporting Services recursos preteridos  
  
### <a name="features-not-supported-in-the-next-version-of-sql-server"></a>Recursos sem suporte na próxima versão do SQL Server  
 Os recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] a seguir não terão suporte na **próxima** versão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Não use esses recursos em novo trabalho de desenvolvimento e, assim que possível, modifique os aplicativos que os utilizam atualmente.  
  
#### <a name="html-rendering-extension-device-information-settings"></a>Configurações de informações de dispositivos para extensões de renderização HTML  
 As configurações de informações de dispositivos da extensão de renderização HTML a seguir foram preteridas.  
  
-   ActionScript  
  
-   ActiveXControls  
  
-   GetImage  
  
-   OnlyVisibleStyles  
  
-   ReplacementRoot  
  
-   ResourceStreamRoot  
  
-   StreamRoot  
  
-   UsePx  
  
-   Zoom  
  
 Para obter mais informações sobre a extensão de renderização HTML, consulte [HTML Device Information Settings](html-device-information-settings.md)  
  
#### <a name="microsoft-word-and-microsoft-excel-1997-2003-rendering"></a>Renderização do Microsoft Word e do Microsoft Excel 1997-2003  
 As[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] extensões [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] de renderização BIFF8 são relatadas para o formato de arquivo de intercâmbio binário do [!INCLUDE[msCoName](../includes/msconame-md.md)] Word e [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 1997-2003. [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]inclui extensões que são renderizadas [!INCLUDE[msCoName](../includes/msconame-md.md)] no formato XML aberto do Office 2007-2010.  
  
#### <a name="report-definition-language-rdl-2005-and-earlier"></a>Linguagem RDL 2005 e versões anteriores  
 A linguagem RDL 2005 e as versões anteriores foram preteridos. Para obter mais informações sobre o RDL, consulte [linguagem de definição de relatório &#40;&#41;SSRS ](reports/report-definition-language-ssrs.md).  
  
 Para obter mais informações como atualizar relatórios, consulte [Upgrade Reports](install-windows/upgrade-reports.md).  
  
#### <a name="sql-server-2005-and-earlier-custom-report-items"></a>Itens de relatório personalizados do SQL Server 2005 e versões anteriores  
 Os itens de relatório personalizados (CRI) [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] compilados para 2005 e anteriores foram preteridos.  
  
#### <a name="reporting-services-snapshots-2005-and-earlier"></a>Instantâneos do Reporting Services 2005 e versões anteriores  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]os instantâneos renderizados com [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 e anteriores são preteridos.  
  
#### <a name="report-models"></a>Modelos de relatório  
 Os modelos de relatório SMDL (linguagem de modelagem semântica) foram preteridos. Embora você possa continuar usando modelos de relatório existentes como fontes de dados em [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] relatórios, você deve considerar atualizar seus relatórios para remover sua dependência em modelos de relatório.  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não inclui ferramentas para criar ou atualizar modelos de relatório. Para obter mais informações, consulte [alterações significativas em SQL Server Reporting Services no SQL Server 2014](breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md).  
  
#### <a name="deprecated-methods-in-the-web-service-endpoint"></a>Métodos preteridos no ponto de extremidade de serviço Web  
 As operações a seguir foram preteridas no ponto de extremidade do serviço Web do <xref:ReportService2010.ReportingService2010>:  
  
-   <xref:ReportService2010.ReportingService2010.GetProperties%2A>  
  
-   <xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>  
  
#### <a name="sharepoint-web-parts"></a>Web Parts do SharePoint  
 O arquivo de gabinete de instalação **RSWebParts.cab** e as Web Parts do SharePoint que podem ser extraídos do arquivo cab são preteridos. As Web Parts preteridas são o Gerenciador de relatórios (**comexplorer. dwp**) e o Visualizador de relatórios (**comviewer. dwp**).  
  
 Para obter mais informações sobre as Web Parts preteridas, consulte [Exibir e explorar relatórios de modo nativo usando o SharePoint Web Parts (SSRS)](https://msdn.microsoft.com/library/ms159772.aspx)  
  
### <a name="features-not-supported-in-a-future-version-of-sql-server"></a>Recursos sem suporte em uma versão futura do SQL Server  
 Os recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] a seguir terão suporte na próxima versão do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], mas serão removidos em uma versão posterior. A versão específica do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] não foi determinada.  
  
 Nenhum recurso do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] foi preterido no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
##  <a name="sql-server-2012-sp1-reporting-services-deprecated-features"></a><a name="bkmk_2012sp1"></a>SQL Server 2012 SP1 Reporting Services recursos preteridos  
 Esta seção descreve os recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] preteridos no [!INCLUDE[ssSQL11SP1](../includes/sssql11sp1-md.md)]. Os recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] a seguir terão suporte na próxima versão do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], mas serão removidos em uma versão posterior. A versão específica do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não foi determinada.  
  
### <a name="sharepoint-web-parts"></a>Web Parts do SharePoint  
 O arquivo de gabinete de instalação **RSWebParts.cab** e as Web Parts do SharePoint que podem ser extraídos do arquivo cab são preteridos. As Web Parts preteridas são o Gerenciador de relatórios (**comexplorer. dwp**) e o Visualizador de relatórios (**comviewer. dwp**).  
  
 Para obter mais informações sobre as Web Parts preteridas, consulte [Exibir e explorar relatórios de modo nativo usando o SharePoint Web Parts (SSRS)](https://msdn.microsoft.com/library/ms159772.aspx)  
  
##  <a name="sql-server-2012-reporting-services-deprecated-features"></a><a name="bkmk_2012"></a>SQL Server 2012 Reporting Services recursos preteridos  
 Esta seção descreve os recursos do [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] preteridos no [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
### <a name="html-rendering-extension-device-information-settings"></a>Configurações de informações de dispositivos para extensões de renderização HTML  
 As configurações de informações de dispositivos da extensão de renderização HTML a seguir foram preteridas.  
  
-   ActionScript  
  
-   ActiveXControls  
  
-   GetImage  
  
-   OnlyVisibleStyles  
  
-   ReplacementRoot  
  
-   ResourceStreamRoot  
  
-   StreamRoot  
  
-   UsePx  
  
-   Zoom  
  
 Para obter mais informações sobre a extensão de renderização HTML, consulte [HTML Device Information Settings](html-device-information-settings.md)  
  
### <a name="microsoft-word-and-microsoft-excel-1997-2003-rendering"></a>Renderização do Microsoft Word e do Microsoft Excel 1997-2003  
 As[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] extensões [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] de renderização BIFF8 são relatadas para o formato de arquivo de intercâmbio binário do [!INCLUDE[msCoName](../includes/msconame-md.md)] Word e [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel 1997-2003. [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]inclui extensões que são renderizadas [!INCLUDE[msCoName](../includes/msconame-md.md)] no formato XML aberto do Office 2007-2010.  
  
### <a name="report-definition-language-rdl-2005-and-earlier"></a>Linguagem RDL 2005 e versões anteriores  
 A linguagem RDL 2005 e as versões anteriores foram preteridos. Para obter mais informações sobre o RDL, consulte [linguagem de definição de relatório &#40;&#41;SSRS ](reports/report-definition-language-ssrs.md).  
  
 Para obter mais informações como atualizar relatórios, consulte [Upgrade Reports](install-windows/upgrade-reports.md).  
  
### <a name="sql-server-2005-and-earlier-custom-report-items"></a>Itens de relatório personalizados do SQL Server 2005 e versões anteriores  
 Os itens de relatório personalizados (CRI) [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] compilados para 2005 e anteriores foram preteridos.  
  
### <a name="reporting-services-snapshots-2005-and-earlier"></a>Instantâneos do Reporting Services 2005 e versões anteriores  
 [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]os instantâneos renderizados com [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2005 e anteriores são preteridos.  
  
### <a name="report-models"></a>Modelos de relatório  
 Os modelos de relatório SMDL (linguagem de modelagem semântica) foram preteridos. Embora você possa continuar usando modelos de relatório existentes como fontes de dados em [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] relatórios, você deve considerar atualizar seus relatórios para remover sua dependência em modelos de relatório.  
  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] não inclui ferramentas para criar ou atualizar modelos de relatório. Para obter mais informações, consulte [alterações significativas em SQL Server Reporting Services no SQL Server 2014](breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md).  
  
### <a name="deprecated-methods-in-the-web-service-endpoint"></a>Métodos preteridos no ponto de extremidade de serviço Web  
 As operações a seguir foram preteridas no ponto de extremidade do serviço Web do <xref:ReportService2010.ReportingService2010>:  
  
-   <xref:ReportService2010.ReportingService2010.GetProperties%2A>  
  
-   <xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>  
  
##  <a name="sql-server-2008-r2-reporting-services-deprecated-features"></a><a name="bkmk_kj"></a>SQL Server 2008 R2 Reporting Services recursos preteridos  
  
> [!NOTE]  
>  Como o SQL Server 2008 R2 é uma atualização de versão secundária do SQL Server 2008, recomendamos que você também revise o conteúdo na seção do SQL Server 2008.  
  
### <a name="report-server-web-service-endpoints"></a>Pontos de extremidade do serviço Web Servidor de Relatórios  
 Os serviços Web <xref:ReportService2005.ReportingService2005> e <xref:ReportService2006.ReportingService2006> foram preteridos nessa versão. Estes pontos de extremidade foram substituídos por um novo ponto de extremidade: <xref:ReportService2010.ReportingService2010>.  
  
 O novo ponto de extremidade inclui toda a funcionalidade disponível nos pontos de extremidade preteridos e os novos recursos introduzidos no SQL Server 2008 R2.  
  
## <a name="see-also"></a>Consulte Também  
 [O que há de novo &#40;Reporting Services&#41;](what-s-new-reporting-services.md)   
 [Compatibilidade com versões anteriores](../getting-started/backward-compatibility.md)   
 [Alterações de comportamento para SQL Server Reporting Services no SQL Server 2014](behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
 [Funcionalidade descontinuada do SQL Server Reporting Services no SQL Server 2014](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  
  
  
