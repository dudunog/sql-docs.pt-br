---
title: Publicar um relatório em uma biblioteca do SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], reports in SharePoint integrated mode
- SharePoint integration [Reporting Services], publishing to a library
- publishing reports [Reporting Services], to a SharePoint library
ms.assetid: 3f6dfc28-50d8-4231-bd25-871b5f77cce6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1cc957af5596acbf2478d55645b1386283970e33
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66102524"
---
# <a name="publish-a-report-to-a-sharepoint-library"></a>Publicar um relatório em uma biblioteca do SharePoint
  Para publicar um relatório em um site do SharePoint configurado para integração do SharePoint, você deve definir as propriedades do projeto no Designer de Relatórios. Nas propriedades do projeto, todas as referências a servidores, relatórios e fontes de dados compartilhadas devem ser URLs totalmente qualificadas. Na definição de relatórios, todas as referências a sub-relatórios, relatórios detalhados e recursos como imagens com base na Web devem ser URLs totalmente qualificadas.  
  
 Você deve ter permissão de **Membro** ou **Proprietário** no site do SharePoint para definir as propriedades no projeto. Para obter mais informações, consulte [Exemplos de URL para itens de relatório publicados em um Servidor de Relatório no modo do SharePoint &#40;SSRS&#41;](../tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md).  
  
### <a name="to-publish-a-report-to-a-sharepoint-site"></a>Para publicar um relatório em um site do SharePoint  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra um projeto existente ou novo do Servidor de Relatório.  
  
2.  No menu **Projeto** , clique em **Propriedades**. A caixa de diálogo **páginas de propriedades** do _ \<projeto>_ é aberta.  
  
3.  Na lista **Configuração** , selecione o nome de uma configuração de build de solução a ser usado para criar e publicar seu relatório. A configuração atual é listada como **ativa**(*\<>de configuração *).  
  
4.  Para publicar fontes de dados compartilhadas no seu projeto e substituir as fontes de dados compartilhadas publicadas, defina **OverwriteDataSources** como **True**.  
  
5.  Adicional Para **TargetDataSourceFolder**, digite uma URL para uma biblioteca do SharePoint ou pasta de biblioteca (por *http://TestServer/TestSite/Documents/DataSources)* exemplo,.  
  
     Se você não especificar um valor, o valor **TargetReportFolder** será usado.  
  
6.  Para **TargetReportFolder**, digite uma URL para uma biblioteca ou pasta de biblioteca (por exemplo *http://TestServer/TestSite/Documents/Reports)*,.  
  
7.  Para **TargetServerURL**, digite uma URL em um site de nível superior ou subsite do SharePoint. Se você não especificar um site, o site de nível superior padrão será usado (por exemplo *http://servername* *http://servername/site*,, ou *http://servername/site/subsite*).  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. No Gerenciador de Soluções, clique com o botão direito do mouse no relatório que você quer publicar e clique em **Implantar**. O relatório será publicado no local especificado em **TargetReportFolder**. Erros de implantação são exibidos na janela Saída.  
  
## <a name="see-also"></a>Consulte Também  
 [Caixa de diálogo páginas de propriedades do projeto](../tools/project-property-pages-dialog-box.md)   
 [Definir propriedades de implantação &#40;Reporting Services&#41;](../tools/set-deployment-properties-reporting-services.md)   
 [Publicando relatórios em um servidor de relatório](publishing-reports-to-a-report-server.md)   
 [Exemplos de URL para itens de relatório publicados em um servidor de relatório no modo do SharePoint &#40;SSRS&#41;](../tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [Usar uma conexão de dados do Office &#40;.odc&#41; com relatórios &#40;Reporting Services no modo integrado do SharePoint&#41;](../report-data/use-an-office-data-connection-odc-with-reports.md)  
  
  
