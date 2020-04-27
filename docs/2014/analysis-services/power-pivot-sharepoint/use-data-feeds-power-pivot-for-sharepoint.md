---
title: Usar feeds de dados (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 50140fdf-6fd1-41a1-9c14-8ecfb97ba2e1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6efccad47f0d6670c87aeb1e9cc9ef9ec654a138
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66070912"
---
# <a name="use-data-feeds-powerpivot-for-sharepoint"></a>Usar feeds de dados (PowerPivot para SharePoint)
  Feeds de dados são um ou mais fluxos de dados gerados de uma fonte de dados online e transmitidos para um documento ou aplicativo de destino. Se você está usando o PowerPivot para Excel, os feeds de dados podem ajudá-lo a obter dados corporativos ou de negócios existentes de fontes de dados arbitrárias dentro da janela do PowerPivot na pasta de trabalho do Excel 2010. Depois de importar um feed de dados para uma pasta de trabalho, você poderá referenciá-lo posteriormente em qualquer operação de atualização de dados agendada em um servidor do SharePoint.  
  
 A maneira como você usa um feed de dados depende de você estar usando recursos de exportação internos em aplicativos que dão suporte a feeds de dados Atom ou estar criando e usando serviços de dados personalizados. Aplicativos que podem publicar e ler dados XML do Atom fornecem transferência de dados transparente que oculta as mecânicas dos feeds de dados e serviços de dados de usuários. Para um usuário, os dados são simplesmente movidos de um aplicativo para outro.  
  
 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e o Microsoft SharePoint 2010 fornecem feeds de dados que podem ser usados em pastas de trabalho PowerPivot. Você pode usar as informações deste tópico para aprender como acessar feeds de dados de relatórios e listas já existentes.  
  
 Este tópico contém as seguintes seções:  
  
 [Pré-requisitos](#prereq)  
  
 [Criar um feed de dados de uma lista do SharePoint](#sharepointlist)  
  
 [Criar um feed de dados de um relatório Reporting Services](#rsreport)  
  
 [Criar um feed de dados de um documento de serviço de dados](#dsdoc)  
  
##  <a name="prerequisites"></a><a name="prereq"></a> Pré-requisitos  
 Você deve ter o PowerPivot para Excel para importar um feed de dados para o Excel 2010.  
  
 Você deve ter um serviço Web ou um serviço de dados que forneça dados no formato Atom 1.0. Tanto [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o quanto o SharePoint 2010 podem fornecer dados nesse formato.  
  
 Antes de exportar uma lista do SharePoint como um feed de dados, você deve instalar os ADO.NET Data Services no servidor do SharePoint. Para obter mais informações, consulte [Instalar o ADO.NET Data Services para dar suporte a exportações do feed da dodos das listas do SharePoint](../../sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md).  
  
##  <a name="create-a-data-feed-from-a-sharepoint-list"></a><a name="sharepointlist"></a>Criar um feed de dados de uma lista do SharePoint  
 Em um farm do SharePoint 2010, uma lista do SharePoint tem um botão Exportar como Feed de Dados na faixa de opções da lista. Você pode clicar nesse botão para exportar a lista como um feed. Para obter os melhores resultados, você deve ter o Excel 2010 com o aplicativo cliente PowerPivot na estação de trabalho. O aplicativo cliente PowerPivot será iniciado em resposta à exportação do feed de dados criando uma nova tabela do PowerPivot que contém a lista.  
  
1.  Abra a lista no site do SharePoint.  
  
2.  Em Ferramentas de Lista, clique em **Lista**.  
  
3.  Em Conectar e Exportar, clique em **Exportar como Feed de Dados**.  
  
    > [!NOTE]  
    >  O botão **Exportar como feed de dados** é acrescentado ao SharePoint por meio do PowerPivot. Se você não tiver o PowerPivot para SharePoint instalado ou se você não ativou o recurso do PowerPivot, esse botão não estará disponível.  
  
4.  Clique em **Abrir** se o PowerPivot para Excel estiver instalado localmente, ou clique em **Salvar** para salvar o documento .atomsvc no seu disco rígido para operações de importação futuras.  
  
5.  Se você escolheu **Abrir**, use o Assistente de Importação de Tabela para importar o feed de dados para uma planilha. O feed de dados será adicionado como uma nova tabela na janela do PowerPivot.  
  
 Um erro ocorrerá se o ADO.NET Data Services 3.5.1 não estiver instalado no servidor do SharePoint. Para obter mais informações sobre o erro e como resolvê-lo, consulte [Instalar o ADO.NET Data Services para dar suporte a exportações do feed de dados das listas do SharePoint](../../sql-server/install/install-ado-net-data-services-to-support-data-feed-exports-of-sharepoint-lists.md).  
  
##  <a name="create-a-data-feed-from-a-reporting-services-report"></a><a name="rsreport"></a> Criar um feed de dados de um relatório do Reporting Services  
 Se você tiver uma implantação do SQL Server 2008 R2 Reporting Services, poderá usar a nova extensão de renderização Atom para gerar um feed de dados a partir de um relatório existente. Para obter os melhores resultados, você deve ter o Excel 2010 com o PowerPivot para Excel na estação de trabalho. O aplicativo cliente PowerPivot será iniciado em resposta à exportação do feed de dados, adicionando e relacionando automaticamente as tabelas e colunas à medida que elas são transmitidas.  
  
 Para obter instruções sobre como exportar um feed de dados de um relatório, consulte [Gerar feeds de dados de um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/generate-data-feeds-from-a-report-report-builder-and-ssrs.md) no [arquivo de Ajuda do Construtor de Relatórios](https://go.microsoft.com/fwlink/?LinkId=154494).  
  
> [!NOTE]  
>  Para configurar uma agenda de atualização de dados recorrente que reimporta dados de relatório em uma pasta de trabalho PowerPivot que é publicada em uma biblioteca do SharePoint, o servidor de relatório deve ser configurado para integração do SharePoint. Para obter mais informações sobre como usar PowerPivot para SharePoint e Reporting Services em conjunto, consulte [configuração e administração de um servidor de relatório &#40;Reporting Services modo do SharePoint&#41;](../../reporting-services/configure-administer-report-server-reporting-services-sharepoint-mode.md).  
  
##  <a name="create-a-data-feed-from-a-data-service-document"></a><a name="dsdoc"></a> Criar um feed de dados de um documento de serviço de dados  
 Se você tiver um serviço de dados personalizado que gere feeds Atom, poderá configurar um documento de serviço de dados como uma maneira de tornar os dados disponíveis a usuários e aplicativos. Um arquivo de *documento de serviço de dados* (.atomsvc) especifica uma ou mais conexões com fontes online que publicam dados no formato de conexão do Atom. Os documentos de serviço de dados podem ser criados em uma *biblioteca de feeds de dados*, que é uma biblioteca com finalidade especial que proporciona um ponto de acesso comum para a procura de documentos do serviço de dados que foram publicados em um servidor do SharePoint. Os operadores de informações que têm permissão para acessar documentos do serviço de dados na biblioteca de feed de dados podem referenciar a URL do SharePoint do documento para importar os feeds de dados para suas pastas de trabalho e aplicativos.  
  
1.  Abra uma biblioteca de feed de dados que foi criada pelo administrador do site. Para obter mais informações, consulte [criar ou personalizar uma biblioteca de feeds de dados &#40;PowerPivot para SharePoint&#41;](create-or-customize-a-data-feed-library-power-pivot-for-sharepoint.md).  
  
2.  Em Ferramentas de Biblioteca, clique em **Documentos**.  
  
3.  Clique em **Novo Documento**.  
  
4.  Forneça um nome de arquivo e uma descrição.  
  
5.  Especifique uma ou mais URLs que fornecem o feed:  
  
    1.  A**URL base** é opcional. Você deve especificar isto se um documento de serviço de dados fornecer vários feeds. A URL base deve especificar a parte da URL que é comum a todos os feeds (por exemplo, o nome do servidor e o site). Se você estiver criando um documento de serviço de dados para um relatório do Reporting Services, a URL de base será a URL do servidor de relatório e o relatório.  
  
    2.  A**URL do Serviço Web** é obrigatória. Sem a URL base, este valor deve incluir http:// ou https:// no endereço. Se você especificou uma URL base, a URL de serviço Web é a parte que segue a URL base. Por exemplo, se a URL completa for http://adventure-works/inventory/today.aspx, a URL base será http://adventure-works/inventory, e a URL do serviço Web seria/Today.aspx.  
  
         A URL de serviço Web pode incluir parâmetros que filtram ou selecionam um subconjunto de dados. O aplicativo ou serviço que fornecem o feed devem oferecer suporte a parâmetros que você especifica na URL.  
  
6.  Insira um **Nome de Tabela**, uma tabela para cada feed. Esse valor é necessário. O nome de tabela é usado por um aplicativo cliente que consome o feed de dados. No PowerPivot para Excel, o nome de tabela é usado para nomear tabelas na janela do PowerPivot que conterá os dados importados.  
  
## <a name="see-also"></a>Consulte Também  
 [Ativar a integração de recursos do PowerPivot para coleções de sites na administração central](activate-power-pivot-integration-for-site-collections-in-ca.md)   
 [Compartilhar feeds de dados usando uma biblioteca de feeds de dados &#40;PowerPivot para SharePoint&#41;](share-data-feeds-using-a-data-feed-library-power-pivot-for-sharepoint.md)  
  
  
