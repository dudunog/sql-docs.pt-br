---
title: Acesso a dados PowerPivot | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 83dc82da-91fb-4e47-91a8-0e0db67339b8
author: minewiskan
ms.author: owend
ms.openlocfilehash: b43be7165898ab396e646dd5a3e13add86d8b114
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84540174"
---
# <a name="powerpivot-data-access"></a>Acesso a dados PowerPivot
  Este tópico descreve os modos nos quais os dados são recuperados de uma pastas de trabalho PowerPivot que é publicada em uma biblioteca do SharePoint.  
  
 Os dados PowerPivot são armazenados dentro de uma pasta de trabalho do Excel. A cadeia de conexão é uma URL para uma pasta de trabalho em um site do SharePoint.  
  
 Os dados PowerPivot são geralmente usados pela pasta de trabalho que os contém, como os dados por trás de Tabelas Dinâmicas e Gráficos Dinâmicos. Alternativamente, os dados PowerPivot também podem ser usados como uma fonte de dados externa, onde uma pasta de trabalho, painel ou relatório conecta-se a um arquivo do Excel separado (.xlsx) no SharePoint e recupera os dados para uso subsequente. As ferramentas de cliente que geralmente usam dados PowerPivot são Excel, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], outros relatórios do Reporting Services e PerformancePoint.  
  
 Na área de trabalho, o suplemento do PowerPivot usa o AMO e ADOMD.NET para criar, processar e consultar os dados PowerPivot no workspace de cliente.  
  
 Em um farm do SharePoint, os Serviços do Excel usam o provedor local de OLE DB do MSOLAP para conectar-se a dados PowerPivot. O provedor envia a solicitação de conexão para um servidor do PowerPivot para SharePoint no farm. Esse servidor carrega os dados, executa a consulta e retorna o conjunto de resultados.  
  
##  <a name="querying-powerpivot-data-in-sharepoint"></a><a name="queryproc"></a>Consultando dados PowerPivot no SharePoint  
 Quando você exibe uma pastas de trabalho PowerPivot em uma biblioteca do SharePoint, o dados PowerPivot que estão dentro da pasta de trabalho são detectados, extraídos e processados separadamente em instâncias de servidor do Analysis Services dentro do farm, enquanto os Serviços do Excel renderizam a camada de apresentação. Você pode exibir a pasta de trabalho totalmente processada em uma janela de navegador ou em um aplicativo de área de trabalho do Excel 2010 que tenha o suplemento do PowerPivot.  
  
 O diagrama a seguir mostra como uma solicitação de processamento de consulta se move pelo farm. Como os dados PowerPivot fazem parte de uma pasta de trabalho do Excel 2010, uma solicitação de processamento de consulta ocorre quando um usuário abre uma pasta de trabalho do Excel em uma biblioteca do SharePoint e interage com uma Tabela Dinâmica ou um Gráfico Dinâmico que contêm dados PowerPivot.  
  
 ![GMNI_DataProcReq](../media/gmni-dataprocreq.gif "GMNI_DataProcReq")  
  
 Os componentes dos Serviços do Excel e do PowerPivot para SharePoint processam partes diferentes do mesmo arquivo de pasta de trabalho (.xlsx). Os Serviços do Excel detectam os dados PowerPivot e solicitam o processamento em um servidor do PowerPivot no farm. O servidor do PowerPivot aloca a solicitação a uma instância do [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] que extrai os dados da pasta de trabalho na biblioteca de conteúdo e os carrega. Os dados armazenados na memória são mesclados de volta na pasta de trabalho renderizada e devolvidos ao Excel Web Access para apresentação em uma janela de navegador.  
  
 Nem todos os dados de uma pasta de trabalho do PowerPivot são tratados através de PowerPivot para SharePoint. Os Serviços do Excel processam tabelas e dados de células de uma planilha. Apenas Tabelas Dinâmicas, Gráficos Dinâmicos e Segmentações de Dados que vão de encontro aos dados PowerPivot são manipulados pelo PowerPivot para SharePoint.  
  
## <a name="see-also"></a>Consulte Também  
 [Conectar-se ao Analysis Services](../instances/connect-to-analysis-services.md)   
 [Acesso a dados de modelo de tabela](../tabular-models/tabular-model-data-access.md)  
  
  
