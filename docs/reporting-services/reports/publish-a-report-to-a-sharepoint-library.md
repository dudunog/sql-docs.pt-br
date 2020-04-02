---
title: Publicar um relatório em uma biblioteca do SharePoint | Microsoft Docs
description: Saiba como publicar um relatório em uma biblioteca do SharePoint definindo as propriedades do projeto no Report Designer.
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], reports in SharePoint integrated mode
- SharePoint integration [Reporting Services], publishing to a library
- publishing reports [Reporting Services], to a SharePoint library
ms.assetid: 3f6dfc28-50d8-4231-bd25-871b5f77cce6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 093837d7d7d2c6833b4c7dce8fabbf554d634290
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79510107"
---
# <a name="publish-a-report-to-a-sharepoint-library"></a>Publicar um relatório em uma biblioteca do SharePoint
  Para publicar um relatório em um site do SharePoint configurado para integração do SharePoint, você deve definir as propriedades do projeto no Designer de Relatórios. Nas propriedades do projeto, todas as referências a servidores, relatórios e fontes de dados compartilhadas devem ser URLs totalmente qualificadas. Na definição de relatórios, todas as referências a sub-relatórios, relatórios detalhados e recursos como imagens com base na Web devem ser URLs totalmente qualificadas.  
  
 Você deve ter permissão de **Membro** ou **Proprietário** no site do SharePoint para definir as propriedades no projeto. Para obter mais informações, consulte [Exemplos de URL para itens de relatório publicados em um Servidor de Relatório no modo do SharePoint &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md).  
  
### <a name="to-publish-a-report-to-a-sharepoint-site"></a>Para publicar um relatório em um site do SharePoint  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra um projeto existente ou novo do Servidor de Relatório.  
  
2.  No menu **Projeto** , clique em **Propriedades**. A caixa de diálogo _\<project>_ **Páginas de Propriedades do**  será exibida.  
  
3.  Na lista **Configuração** , selecione o nome de uma configuração de build de solução a ser usado para criar e publicar seu relatório. A configuração atual está listada como **Ativa**( *\<configuration>* ).  
  
4.  Para publicar fontes de dados compartilhadas no seu projeto e substituir as fontes de dados compartilhadas publicadas, defina **OverwriteDataSources** como **True**.  
  
5.  (Opcional) Para **TargetDataSourceFolder**, digite uma URL para uma biblioteca do SharePoint ou pasta de biblioteca (por exemplo, `https://TestServer/TestSite/Documents/DataSources`).  
  
     Se você não especificar um valor, o valor **TargetReportFolder** será usado.  
  
6.  Para **TargetReportFolder**, digite uma URL para uma biblioteca ou pasta de biblioteca (por exemplo, `https://TestServer/TestSite/Documents/Reports`).  
  
7.  Para **TargetServerURL**, digite uma URL em um site de nível superior ou subsite do SharePoint. Se você não especificar um site, o site de nível superior padrão será usado (por exemplo, `https://servername`, `https://servername/site`ou `https://servername/site/subsite`).  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. No Gerenciador de Soluções, clique com o botão direito do mouse no relatório que você quer publicar e clique em **Implantar**. O relatório será publicado no local especificado em **TargetReportFolder**. Erros de implantação são exibidos na janela Saída.  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo Páginas de Propriedades do Projeto](../../reporting-services/tools/project-property-pages-dialog-box.md)   
 [Definir propriedades de implantação &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
 [Publicando relatórios em um servidor de relatório](../../reporting-services/reports/publishing-reports-to-a-report-server.md)   
 [Exemplos de URL para itens de relatório publicados em um Servidor de Relatório no modo do SharePoint &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [Usar uma conexão de dados do Office &#40;.odc&#41; com relatórios &#40;Reporting Services no modo integrado do SharePoint&#41;](../../reporting-services/report-data/use-an-office-data-connection-odc-with-reports.md)  
  
  
