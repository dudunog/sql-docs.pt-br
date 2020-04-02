---
title: Gerar feeds de dados de um relatório (Construtor de Relatórios) | Microsoft Docs
description: É possível gerar feeds de dados em conformidade com o Atom com base em relatórios paginados. Use os feeds em aplicativos, como o Power Pivot ou o Power BI, que podem consumir feeds de dados.
ms.date: 05/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: e68baae2-9f2a-4f13-9179-9ac7f29111c5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6eedf7ae96f41a75a8690162de01473d7e2e5664
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "80342799"
---
# <a name="generate-data-feeds-from-a-report-report-builder-and-ssrs"></a>Gerar feeds de dados de um relatório (Construtor de Relatórios e SSRS)

Você pode gerar feeds de dados em conformidade com Atom com base em relatórios paginados e, depois, usar os feeds de dados em aplicativos, como o Power Pivot ou o Power BI, que pode consumir feeds de dados.  
  
 A extensão de renderização do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Atom gera um documento de serviço Atom que lista os feeds de dados disponíveis a partir de um relatório. O documento lista pelo menos um feed de dados para cada região no relatório. Dependendo do tipo de região de dados e dos dados que a região de dados exibe, o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] pode gerar vários feeds de dados de uma região de dados.  
  
 O documento de serviço Atom contém um identificador exclusivo para cada feed de dados e você usa o identificador em uma URL para exibir o conteúdo do feed de dados.  
  
 Para obter mais informações, consulte [Gerando feeds de dados de relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-generate-an-atom-service-document"></a>Para gerar um documento de serviço Atom  
  
1.  no Portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , navegue até o relatório para o qual você deseja gerar feeds de dados.  
  
2.  Clique no relatório.  
  
     O relatório é executado.  
  
3.  Na barra de ferramentas, clique no ícone **Exportar para Feed de Dados** .  
  
     Uma mensagem é exibida perguntando se você deseja salvar ou abrir o documento Atom que contém o feed de dados.  
  
4.  Clique em **Salvar** para salvar o documento no sistema de arquivos, ou clique em **Abrir** para exibir o conteúdo do documento antes de salvá-lo. **Por padrão, o documento é aberto em um navegador.**  
  
5.  Navegue até o local onde o documento será salvo.  
  
6.  Outra opção é alterar o nome do documento.  
  
    > [!NOTE]  
    >  Por padrão, o nome do documento é o nome do relatório.  
  
7.  Verifique se o tipo do documento é **Arquivo ATOMSVC**e clique em **Salvar**.  
  
8.  Opcionalmente, abra o arquivo .atomsvc em um navegador, editor de texto ou editor de XML.  
  
### <a name="to-view-an-atom-compliant-data-feed"></a>Para exibir um feed de dados compatível com Atom  
  
1.  Se o documento de serviço Atom ainda não estiver aberto, localize-o e abra-o em um navegador como o Internet Explorer.  
  
2.  Copie no navegador a URL do feed de dados a ser exibida a partir do documento de serviço Atom.  
  
     Este é o formato da URL:  
  
     `https://<server name>/ReportServer?%2f<ReportName>rs%3aCommand=Render&rs%3aFormat=ATOM&rc%3aDataFeed=<Identifier>`  
  
3.  Pressione ENTER.  
  
     Uma mensagem é exibida perguntando se você deseja salvar ou abrir o documento Atom que contém o feed de dados.  
  
4.  Clique em **Salvar** para salvar o documento no sistema de arquivos, ou clique em **Abrir** para exibir o feed de dados antes de salvar o documento.  
  
5.  Navegue até o local onde o documento será salvo.  
  
6.  Outra opção é alterar o nome do documento.  
  
    > [!NOTE]  
    >  Por padrão, o nome do documento é o nome do relatório. Se o documento de serviço Atom tiver vários feeds, por padrão todos usarão o mesmo nome, o nome do relatório. Para diferenciá-los, renomeie-os para usar nomes significativos.  
  
7.  Verifique se o tipo do documento é **Arquivo ATOM**e clique em **Salvar**.  
  
8.  Opcionalmente, abra o arquivo .atom em um navegador, editor de texto ou editor de XML.  

## <a name="next-steps"></a>Próximas etapas

[Exportar relatórios](../../reporting-services/report-builder/export-reports-report-builder-and-ssrs.md)  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
