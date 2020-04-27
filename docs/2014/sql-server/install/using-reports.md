---
title: Usando relatórios | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- displaying reports
- overriding reports
- Upgrade Advisor Report Viewer
- reports [Upgrade Advisor], about reports
- formatting reports
- resolved issues [Upgrade Advisor]
- distributing reports [Reporting Services]
- filtering reports [Reporting Services]
- removing report items
- viewing reports
- rerunning analysis
- information issues [Upgrade Advisor]
- deleting report items
- icons [Upgrade Advisor]
- Upgrade Advisor [SQL Server], reports
- sending reports
- blocking issues [Upgrade Advisor]
- sharing reports
- reports [Upgrade Advisor]
- SQL Server Upgrade Advisor, reports
- modifying reports
- distributing reports [Reporting Services], about report distribution
- warnings [Upgrade Advisor]
- analyzing system [Upgrade Advisor], reports
ms.assetid: 4a3cb94a-a7ac-4cec-94c7-db26fcf6d161
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fc3a08e707f6b51059145c69fdee15f78c933135
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66091226"
---
# <a name="using-reports"></a>Usando relatórios
  Um relatório único é gerado para cada componente e, se necessário, para cada instância analisada pelo Assistente para Análise do Supervisor de Atualização em um servidor. O relatório fornece detalhes sobre problemas conhecidos que podem afetar uma atualização. Ele também fornece links para informações e ações sugeridas para resolver os problemas identificados.  
  
> [!NOTE]  
>  Se o Visualizador de relatórios do supervisor de atualização não encontrar relatórios no diretório de relatórios padrão, você poderá carregar um relatório de um diretório diferente usando o link **abrir relatório** .  
  
## <a name="viewing-reports"></a>Exibindo relatórios  
 O Visualizador de Relatórios do Supervisor de Atualização é usado para exibir relatórios do Supervisor de Atualização. Para exibir relatórios, na página inicial do supervisor de atualização, clique em **Iniciar Visualizador de relatórios do supervisor de atualização**.  
  
 Depois de carregar um relatório no servidor, você pode selecionar um componente para o qual deseja verificar os problemas de atualização. Você pode aplicar um filtro da caixa **Filtrar por** para ver o seguinte:  
  
-   Todos os problemas  
  
-   Todos os problemas de atualização  
  
-   Problemas de pré-atualização  
  
-   Todos os problemas de migração  
  
-   Problemas resolvidos  
  
-   Problemas não resolvidos  
  
 Se o relatório tiver mais de 20 problemas, você poderá ir para o grupo de problemas seguinte ou anterior clicando em **avançar 20** ou **20** na parte superior ou inferior da lista de problemas.  
  
 Você pode exibir até cinco relatórios salvos selecionando os relatórios na caixa de listagem suspensa **relatório** . Os relatórios são listados pelo carimbo de data/hora de quando foram gerados.  
  
## <a name="report-format"></a>Formato de relatório  
 O visualizador de relatórios exibe os problemas em três colunas. Cada problema pode ser recolhido para que você possa ocultar a descrição ou exibir apenas informações fundamentais.  
  
 A primeira coluna é a coluna **importância** . Os ícones indicam a importância de cada problema. Um círculo vermelho com um X indica problemas importantes ou que podem impedir a atualização; um triângulo amarelo com um ponto de exclamação indica problemas com avisos ou informações. A segunda coluna, **quando corrigir**, indica quando você deve resolver o problema. Você pode classificar o relatório sobre a coluna **importância** ou **quando corrigir** . A terceira coluna, **Descrição**, lista o título do problema.  
  
 É possível expandir um problema para exibir informações adicionais, um link para informações detalhadas sobre como solucionar o problema e um link para exibir detalhes do problema. Ao clicar no link para acessar informações detalhadas do problema, o tópico da Ajuda com informações sobre o problema e instruções para solucioná-lo é exibido. Depois de corrigir um problema, ou de gerenciar seus itens de ação, você pode marcar problemas como concluídos marcando a caixa de seleção **este problema foi resolvido** . Se você quiser remover os problemas resolvidos da lista de problemas de atualização, clique em **Atualizar**. O problema não é exibido novamente até que você execute o assistente de análise do supervisor de atualização no mesmo componente ou aplique o filtro **problemas resolvidos** da opção **Filtrar por** .  
  
## <a name="report-files"></a>Arquivos de relatório  
 O assistente de análise do supervisor de atualização cria relatórios no\\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diretório meus documentos upgrade Advisor\110\Reports e cria um subdiretório para cada servidor que você analisa. Os arquivos de relatório estão no formato XML e seguem uma convenção de nomenclatura específica. Quando você inicia o Visualizador de Relatórios do Supervisor de Atualização, os arquivos de relatório do diretório padrão são exibidos. Se você copiar arquivos de relatório para essa pasta, eles deverão seguir a mesma convenção de nomenclatura ou o visualizador de relatórios não irá exibi-los automaticamente.  
  
 Se você quiser compartilhar a informações com outras pessoas, poderá enviar-lhes o relatório XML. Se preferir usar outro aplicativo, basta exportar o relatório para um arquivo CSV que pode ser usado para criar uma planilha, um arquivo de texto ou uma mensagem de email.  
  
## <a name="see-also"></a>Consulte Também  
 [Como exibir um relatório do supervisor de atualização](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)   
 [Como: exportar relatórios](../../../2014/sql-server/install/how-to-export-reports.md)   
 [Como filtrar relatórios](../../../2014/sql-server/install/how-to-filter-reports.md)   
 [Resolvendo problemas de atualização](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Supervisor de atualização do SQL Server 2014 &#91;novo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
