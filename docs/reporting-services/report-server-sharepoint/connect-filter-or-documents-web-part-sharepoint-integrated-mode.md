---
title: Conectar uma web part de Filtro ou de Documentos a uma web part do Visualizador de Relatórios do Reporting Services | Microsoft Docs
description: Em um produto do SharePoint, aprenda a criar uma Página de web part ou painel que inclui uma web part de Filtro ou Documentos e uma web part do Visualizador de Relatórios.
ms.date: 11/26/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f0e28fe003407c2f60792bcb9df09dc5d3cc6db0
ms.sourcegitcommit: 66a0672e47415dbd5cfd8d19075102c8c3973e70
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83767077"
---
# <a name="connect-filter-or-documents-web-part-with-a-reporting-services-report-viewer-web-part"></a>Conectar uma web part de Filtro ou de Documentos a uma web part do Visualizador de Relatórios do Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)]  [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-and-later](../../includes/ssrs-appliesto-sharepoint-2013-and-later.md)] [!INCLUDE[ssrs-appliesto-not-sharepoint-online](../../includes/ssrs-appliesto-not-sharepoint-online.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Se você estiver usando um produto do SharePoint, poderá criar um painel ou uma Página de web part que inclui uma web part de Filtro ou de Documentos e uma web part do Visualizador de Relatórios. As versões com suporte são [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] ou [!INCLUDE[SPS2010](../../includes/sps2010-md.md)]. Também há suporte para [!INCLUDE[winSPServ3](../../includes/winspserv3-md.md)] ou [!INCLUDE[offSPServ](../../includes/offspserv-md.md)] 2007. Ao conectarem uma web part de Filtro, os usuários que selecionam valores de filtro em uma web part de Filtro podem enviar o valor para um relatório parametrizado na mesma página. Ao conectarem uma web part de Documentos, os usuários que clicarem na biblioteca de Documentos podem exibir o relatório em uma web part do Visualizador de Relatórios adjacente.

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.

 A web part de Filtro é usada para enviar valores para um ou mais parâmetros em um relatório. Para usar uma web part de Filtro, o relatório deve ter parâmetros definidos para ela, compatíveis com os valores, o tipo de dados e o formato enviado pela web part.  
  
 A web part de Documentos é associada à biblioteca de Documentos do site Inicial. Para exibir, adicionar ou remover itens na Biblioteca de Documentos, clique em **Exibir Todo o Conteúdo do Site**. Em Bibliotecas, clique em **Documentos**. Você pode usar os menus **Novo**, **Carregar**e **Ações** para gerenciar os itens da Biblioteca de Documentos.  
  
## <a name="connect-a-filter-web-part"></a>Conectar uma web part de Filtragem
  
1.  Abra ou crie uma página ou um painel da web part.  
  
2.  No menu **Ações do Site** , clique em **Editar Página**.  
  
3.  Clique em **Adicionar uma web part**.  
  
4.  Em **Todas as web parts**, na categoria **Diversos**, selecione **Visualizador de Relatórios do SQL Server Reporting Services**.  
  
5.  Clique em **Adicionar**. A web part é adicionada à parte superior da zona.  
  
6.  Em outra zona da mesma página ou do mesmo painel da web part, clique em **Adicionar uma web part**.  
  
7.  Em **Todas as web parts**, na seção **Filtros**, selecione uma web part.  
  
8.  Clique em **Adicionar**. A web part é adicionada à parte superior da zona.  
  
9. Na zona que contém a web part, clique no menu **Editar** da web part, aponte para **Conexões**, para **Enviar Valores de Filtro Para** e, em seguida, selecione **Visualizador de Relatórios** - *nome do relatório*.  
  
10. Verifique suas alterações e salve a página.  
  
## <a name="connect-a-documents-web-part"></a>Conectar uma web part de Documentos  
  
1.  Abra ou crie uma página ou um painel da web part.  
  
2.  No menu **Ações do Site** , clique em **Editar Página**.  
  
3.  Clique em **Adicionar uma web part**.  
  
4.  Em **Todas as web parts**, na seção **Listas e Biblioteca**, selecione **Documentos.**  
  
5.  Clique em **Adicionar**. A web part é adicionada à parte superior da zona.  
  
6.  Clique em **Aplicar** na parte inferior do painel de ferramentas e clique em **OK** para fechar esse painel.  
  
7.  Em outra zona da mesma página ou do mesmo painel da web part, clique em **Adicionar uma web part**.  
  
8.  Em **Todas as web parts**, na categoria **Diversos**, selecione **Visualizador de Relatórios do SQL Server Reporting Services.**  
  
9. Clique em **Adicionar**. A web part é adicionada à parte superior da zona.  
  
10. Na zona que contém a web part, clique no menu **Editar** da web part, aponte para **Conexões**, para **Obter definições de relatório de** e, em seguida, selecione **Documentos**.  
  
11. Verifique suas alterações e salve a página.  
  
## <a name="see-also"></a>Confira também

 [Adicionar a web part do Visualizador de Relatórios a uma página da Web](../../reporting-services/report-server-sharepoint/add-the-report-viewer-web-part-to-a-web-page.md)   
 [Web part do Visualizador de Relatórios em um Site do SharePoint](../../reporting-services/report-server-sharepoint/report-viewer-web-part-on-a-sharepoint-site.md)   
 [Personalizar a Web Part do Visualizador de Relatórios](../../reporting-services/report-server-sharepoint/customize-the-report-viewer-web-part.md)  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
