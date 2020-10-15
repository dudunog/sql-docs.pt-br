---
title: Tipo de conexão Analysis Services para DMX | Microsoft Docs
description: Saiba mais sobre o tipo de conexão Analysis Services para DMX e aprenda a usar o Designer de Consultas DMX para criar uma consulta DMX usando elementos gráficos.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- parameters [Reporting Services], DMX
- Data Mining Prediction [Reporting Services]
- query view [Reporting Services]
- DMX [Reporting Services]
- design view [Reporting Services]
- data mining [Reporting Services]
- passing parameters [Reporting Services]
ms.assetid: 2de825e9-6d8a-4128-add0-da15dc6cea3e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: acb81c5dc8533e4870b540dda7c091eb37542d2c
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891816"
---
# <a name="analysis-services-connection-type-for-dmx-ssrs"></a>Tipo de conexão Analysis Services para DMX (SSRS)
  Ao criar um conjunto de dados usando uma fonte de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o Designer de Relatórios exibirá o designer de consultas MDX (Multidimensional Expression) se ele detectar um cubo válido. Se nenhum cubo for detectado, mas um modelo de mineração de dados estiver disponível, o Designer de Relatórios exibirá o designer de consulta DMX. Para alternar entre os designers MDX e DMX, clique no botão **Tipo de Comando DMX** (![Alterar para a exibição de linguagem de consulta DMX](../../reporting-services/report-data/media/rsqdicon-commandtypedmx.gif "Alterar para o modo de exibição de linguagem de consulta DMX")) na barra de ferramentas. Use o Designer de Consulta DMX para criar de maneira interativa uma consulta DMX usando elementos gráficos. Para usar o Designer de Consulta DMX, a fonte de dados especificada já deve ter um modelo de mineração de dados que forneça os dados. Os resultados da consulta são convertidos em um conjunto de linhas bidimensional para ser usado no relatório.  
  
> [!NOTE]  
>  Você deve treinar seu modelo antes de criar seu relatório. Para obter mais informações, consulte [Soluções de mineração de dados](/analysis-services/data-mining/data-mining-solutions).  
  
## <a name="design-mode"></a>Modo Design  
 O designer de consulta DMX é aberto no modo Design. O modo Design inclui uma superfície de design gráfico usada para selecionar um único modelo de mineração de dados e tabela de entrada e uma grade usada para especificara a consulta de previsão. Há dois outros modos no designer de consultas DMX: modo Consulta e Resultado. No modo Consulta, a grade do modo Design é substituída por um painel Consulta, no qual você pode usar para consultas do tipo DMX. No modo Resultado, o conjunto de resultados retornado pela consulta é exibido em uma grade de dados.  
  
 Para alterar os modos do designer de consulta DMX, clique com o botão direito do mouse na superfície do design de consulta e selecione **Design**, **Consulta**ou **Resultado**. Para obter mais informações, consulte [Interface do usuário do Designer de Consultas DMX do Analysis Services](../../reporting-services/report-data/analysis-services-dmx-query-designer-user-interface.md) e [Recuperar dados de um modelo de mineração de dados &#40;DMX&#41; &#40;SSRS&#41;](../../reporting-services/report-data/retrieve-data-from-a-data-mining-model-dmx-ssrs.md).  
  
## <a name="designing-a-prediction-query"></a>Criando uma consulta de previsão  
 O painel Design de Consultas do modo Design contém duas janelas: **Modelo de Mineração** e **Selecionar Tabela de Entrada**. Use a janela **Modelo de Mineração** para selecionar o modelo de mineração a ser usado na consulta. Use a janela **Selecionar Tabela de Entrada** para selecionar a tabela na qual suas previsões devem se basear. Se quiser usar uma consulta singleton em vez de uma tabela de entrada, clique com o botão direito do mouse no painel Design de Consulta e selecione **Consulta Singleton**. A janela **Selecionar Tabela de Entrada** é substituída por uma janela **Entrada de Consulta Singleton** .  
  
 No modo Design, arraste os campos das janelas **Modelo de Mineração** e **Selecionar Tabela de Entrada** para a coluna **Campo** no painel Grade. Você também pode preencher as colunas restantes para especificar um alias, mostrar o campo nos resultados, agrupar os campos e especificar um operador para restringir o valor do campo para um determinado critério ou argumento. Se você estiver no modo Consulta, crie a consulta DMX arrastando os campos para o painel Consulta.  
  
## <a name="using-parameters"></a>Usando parâmetros  
 Você pode passar parâmetros de relatórios para um parâmetro de consulta DMX. Para fazer isso, você deve adicionar um parâmetro à sua consulta DMX, definir os parâmetros de consulta na caixa de diálogo **Parâmetros de Consulta** e modificar os parâmetros de relatório associados. Para definir um parâmetro de consulta, clique no botão **Parâmetros de Consulta** (![Ícone da caixa de diálogo Parâmetros de Consulta](../../reporting-services/report-data/media/iconqueryparameter.gif "Ícone da caixa de diálogo Parâmetros de Consulta")) na barra de ferramentas. Para exibir instruções sobre como definir parâmetros em uma consulta DMX, consulte [Definir parâmetros no Designer de Consulta MDX do Analysis Services &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/define-parameters-in-the-mdx-query-designer-for-analysis-services.md).  
  
 Para obter mais informações sobre como gerenciar a relação entre os parâmetros de relatório e de consulta, consulte [Associar um parâmetro de consulta a um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/associate-a-query-parameter-with-a-report-parameter-report-builder-and-ssrs.md). Para obter mais informações sobre parâmetros, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Soluções de mineração de dados](/analysis-services/data-mining/data-mining-solutions)   
 [Ferramentas de Design da Consulta &#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md)   
 [Criar cadeias de conexão de dados – Construtor de Relatórios e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
