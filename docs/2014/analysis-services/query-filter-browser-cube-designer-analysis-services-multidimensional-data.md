---
title: Consulta e filtro (guia navegador, designer de cubo) (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.browsecube.filterpane.f1
ms.assetid: f5cf0bb1-3afb-4856-a2ef-614deb4e7e49
author: minewiskan
ms.author: owend
ms.openlocfilehash: aa501e2a5b23f32fbd10d244788b1e6e938e938b
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84539728"
---
# <a name="query-and-filter-browser-tab-cube-designer-analysis-services---multidimensional-data"></a>Consulta e filtro (guia Navegador, Designer de Cubo) (Analysis Services - Dados Multidimensionais)
  Esta área da guia **Navegador** do Designer de Cubo contém uma área de consultas e filtros para ajudar a escolher dados do cubo para usar ao navegar ou em consultas. Você pode adicionar quantos objetos cubo desejar e então exibir os resultados na área de dados ou exportar os resultados para um relatório usando Analisar no Excel para visualizar como os dados seriam exibidos pelos usuários finais.  
  
> [!WARNING]  
>  Quando estiver trabalhando com dados nessa área, por padrão, o **Navegador** usará o modo de design gráfico. Porém, você pode editar a consulta diretamente usando o MDX, clicando no botão de alternância **Modo de Design** . Ao fazer isso, o painel que permite criar filtros em dimensões desaparece. Se desejar adicionar um filtro, você poderá alternar novamente para o modo de design gráfico.  
  
 Por padrão, as credenciais do usuário atual, e não as credenciais especificadas na página **Informações da Representação** , são usadas na conexão com a fonte de dados quando uma consulta é executada. Porém, você também pode alterar o contexto de usuário para a consulta ou relatório clicando em **Alterar Usuário** na **Barra de Ferramentas**.  
  
## <a name="options"></a>Opções  
 **Dimensões**  
 Selecione a dimensão na qual fatiar o subcubo.  
  
 **Hierarquia**  
 Selecione a hierarquia na qual fatiar o subcubo.  
  
 **Operador**  
 Selecione o operador que define como a expressão na **Expressão de Filtro** é aplicada à hierarquia selecionada. A tabela a seguir descreve os operadores disponíveis.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Igual**|Os resultados são restringidos ao conjunto definido na **Expressão de Filtro**.|  
|**Diferente de**|Os resultados são restringidos aos membros excluídos pelo conjunto definido na **Expressão de Filtro**.|  
|**Em**|Os resultados são restringidos ao conjunto nomeado escolhido na **Expressão de Filtro**.|  
|**Não está em**|Os resultados são restringidos aos membros excluídos pelo conjunto nomeado escolhido na **Expressão de Filtro**.|  
|**Terá**|Os resultados são restringidos aos membros cujos nomes contêm a sequência de caracteres na **Expressão de Filtro**.|  
|**Começa Com**|Os resultados são restringidos aos membros cujos nomes começam com a sequência de caracteres na **Expressão de Filtro**.|  
|**Intervalo (Inclusivo)**|Os resultados são restringidos ao intervalo escolhido na **Expressão de Filtro**.|  
|**Intervalo (Exclusivo)**|Os resultados são restringidos aos membros excluídos pelo intervalo escolhido na **Expressão de Filtro**.|  
|**MDX**|Os resultados são restringidos à expressão MDX definida na **Expressão de Filtro**.|  
  
 **Expressão de filtro**  
 Digite a expressão a ser avaliada pelo **Operador**que restringe os resultados a serem procurados.  
  
> [!NOTE]  
>  Este campo é um elemento de entrada de dados dinâmicos que altera a aparência para refletir os tipos de dados necessários para o operador selecionado.  
  
## <a name="see-also"></a>Consulte Também  
 [O designer de cubo &#40;Analysis Services-dados multidimensionais&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [Navegador &#40;designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](browser-cube-designer-analysis-services-multidimensional-data.md)   
 [Barra de ferramentas &#40;guia navegador, designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](toolbar-browser-tab-cube-designer-analysis-services-multidimensional-data.md)   
 [Analisar na guia navegador do Excel &#40;, designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](analyze-in-excel-browser-cube-designer-analysis-services-multidimensional-data.md)   
 [Guia do navegador de metadados &#40;, designer de cubo&#41; &#40;Analysis Services de dados multidimensionais&#41;](metadata-browser-tab-cube-designer-analysis-services-multidimensional-data.md)  
  
  
