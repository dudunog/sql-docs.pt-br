---
title: Caixa de diálogo Construtor de membros calculados (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.calculatedmemberbuilderdialog.f1
ms.assetid: 73b89a9f-f403-4ab8-99f7-e3ceb870c260
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8046d93f28c6d7c61899bb5f9aa3598f834c0ab3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66088379"
---
# <a name="calculated-member-builder-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Construtor de Membro Calculado (Analysis Services - Dados multidimensionais)
  Use a caixa de diálogo **Construtor de Membro Calculado** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para criar um membro calculado.  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**Nome**|Digite o nome do membro calculado.|  
|**Hierarquia pai**|Selecione a hierarquia na qual o membro calculado será criado.|  
|**Membro pai**|Essa opção estará habilitada se você selecionar uma hierarquia pai (diferente da dimensão `Measures`) que tem mais de um nível. Clique no botão de reticências (**...**) para selecionar um membro pai. O membro pai determina o local do membro calculado na estrutura de dimensão.|  
|**Expressão**|Digite a expressão MDX que será usada.|  
|**Verificação**|Clique em **Verificar** para testar a expressão MDX definida em **Expressão**.|  
|**Metadados**|Exibe metadados para o objeto [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] atual que pode ser incluído na expressão MDX definida em **Expressão**.<br /><br /> É possível copiar a sintaxe MDX do item selecionado clicando com o botão direito do mouse no item e selecionando **Copiar**ou arrastando o item selecionado para **Expressão**.|  
|**Funções**|Exibe as funções MDX disponíveis para a instância atual do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Os itens listados são recuperados do conjunto de linhas do esquema MDSCHEMA_FUNCTIONS.<br /><br /> É possível copiar a sintaxe MDX do item selecionado clicando com o botão direito do mouse no item e selecionando **Copiar**ou arrastando o item selecionado para **Expressão**.|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de expressões multidimensionais &#40;MDX&#41;](/sql/mdx/multidimensional-expressions-mdx-reference)  
  
  
