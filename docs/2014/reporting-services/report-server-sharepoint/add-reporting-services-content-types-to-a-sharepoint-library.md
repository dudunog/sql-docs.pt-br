---
title: Adicionar a Web Part do Visualizador de relatórios a uma página da Web (Reporting Services no modo integrado do SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SharePoint integration [Reporting Services], viewing reports
- Web Parts [Reporting Services]
- SharePoint integration [Reporting Services], Web Parts
- Report Viewer Web Part [Reporting Services]
ms.assetid: cac75345-2380-467d-a394-0a2140908a5a
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 468acea55c334ffda169daff2b5da4c417348a3e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66104287"
---
# <a name="add-the-report-viewer-web-part-to-a-web-page-reporting-services-in-sharepoint-integrated-mode"></a>Adicionar a Web Part do Visualizador de Relatórios a uma página da Web (Reporting Services no modo integrado do SharePoint)
  É possível usar a Web Part do Visualizador de Relatórios para exibir relatórios executados no servidor de relatório configurado para execução no modo integrado do SharePoint. Você pode usar a Web Part para exibir arquivos de definição de relatório (.rdl) criados no Construtor de Relatórios ou Designer de Relatórios e carregados em uma biblioteca.  
  
 É possível adicionar a Web Part do Visualizador de Relatórios a uma página da Web se você quiser inserir um relatório nessa página.  
  
> [!NOTE]  
>  Apesar de terem nomes idênticos, a Web Part do Visualizador de Relatórios instalada pelo suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é diferente da Web Part do Visualizador de Relatórios incluída no arquivo RSWebParts.cab. As instruções neste tópico são específicas para a Web Part do Visualizador de Relatórios instalada pelo suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Para adicionar uma Web Part a uma página da Web é necessário ter a permissão Adicionar e Personalizar Páginas de site. Se você estiver usando as configurações de segurança padrão, essa permissão será concedida a membros do grupo **Proprietários** que tenham nível de permissão Controle Total.  
  
### <a name="to-embed-a-report-in-a-web-page"></a>Para inserir um relatório em uma página da Web  
  
1.  Abra ou crie uma página ou um painel da Web Part.  
  
2.  Em **Ações do Site**, clique em **Editar Página**.  
  
3.  Clique em **Adicionar uma Web Part**.  
  
4.  Na lista de categorias de web part, selecione a categoria **Diversas** e depois selecione **Visualizador de Relatórios do SQL Server Reporting Services**.  
  
5.  Clique em **Adicionar**. A Web Part será adicionada à parte superior da zona. Você pode arrastá-la para um local diferente na zona.  
  
6.  No visualizador, clique em **Clique aqui abrir o painel de ferramentas**.  
  
7.  Selecione um relatório de qualquer biblioteca na coleção de sites atuais clicando no botão Procurar (**...**). Você também pode digitar a URL do relatório. Para determinar a URL de um relatório, clique com o botão direito do mouse no relatório e selecione **Propriedades**. Não clique na seta para baixo ao lado do relatório; a URL do relatório não está indicada na página Exibir Propriedades do item. Se você copiar e colar a URL da caixa de diálogo **Propriedades** , substitua a codificação de URL "%20" por um espaço (por exemplo, "Company%20Sales" deverá ser "Company Sales").  
  
    > [!NOTE]  
    >  Cada Web Part do Visualizador de Relatórios contém um único relatório. É necessário que a URL seja totalmente qualificada para um relatório que está no site do SharePoint atual ou em um site no mesmo aplicativo ou farm da Web. A URL deve apontar para uma biblioteca de documentos ou para uma pasta em uma biblioteca de documentos que contenha o relatório. A URL do relatório deve incluir a extensão de arquivo .rdl. Se o relatório depender de um arquivo de fonte de dados compartilhados ou de modelo, não será necessário especificar esses arquivos na URL. O relatório contém referências aos arquivos necessários.  
  
8.  Enquanto o painel de ferramentas estiver aberto, você poderá definir propriedades para modificar a aparência e o layout padrão.  
  
9. Clique em **Aplicar** na parte inferior do painel de ferramentas e clique em **OK** para fechar esse painel.  
  
## <a name="see-also"></a>Consulte Também  
 [Web Part do Visualizador de relatórios em um site do SharePoint](../report-viewer-web-part-on-a-sharepoint-site.md)   
 [Personalizar a Web Part do Visualizador de relatórios](../customize-the-report-viewer-web-part.md)   
 [Concedendo permissões em itens do servidor de relatório em um site do SharePoint](../security/granting-permissions-on-report-server-items-on-a-sharepoint-site.md)   
 [Instalar ou desinstalar o suplemento Reporting Services para SharePoint &#40;SharePoint 2010 e SharePoint 2013&#41;](../install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)  
  
  
