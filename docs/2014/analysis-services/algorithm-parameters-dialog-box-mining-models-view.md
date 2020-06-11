---
title: Caixa de diálogo parâmetros de algoritmo (exibição de modelos de mineração) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.models.algorithmparameters.f1
helpviewer_keywords:
- Algorithm Parameters dialog box
ms.assetid: 57f9f6f8-8ca4-4a6e-8f18-85f0571b7060
author: minewiskan
ms.author: owend
ms.openlocfilehash: b942210e653bc3e0a7309a98a4e75e84c5f82168
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528132"
---
# <a name="algorithm-parameters-dialog-box-mining-models-view"></a>Caixa de diálogo Parâmetros de Algoritmo (Exibição de Modelos de Mineração)
  Use a caixa de diálogo **Parâmetros de Algoritmo** para ajustar os parâmetros de algoritmo que sejam específicos ao modelo selecionado. A alteração de um parâmetro de algoritmo geralmente altera os resultados do modelo de mineração. O modo como cada parâmetro afeta os resultados, depende do algoritmo que está sendo usado e dos dados. Para obter mais informações, consulte [Personalizar os modelos de mineração e a estrutura](data-mining/customize-mining-models-and-structure.md).  
  
## <a name="options"></a>Opções  
 **Parâmetros**  
 Lista os parâmetros disponíveis para o modelo de mineração selecionado.  
  
 A lista a seguir descreve as colunas disponíveis.  
  
|Coluna|Descrição|  
|------------|-----------------|  
|**Parâmetro**|Liste o nome do parâmetro.|  
|**Valor**|Digite um valor somente se desejar alterar o valor padrão do parâmetro.|  
|**Default**|Liste um valor padrão do parâmetro que o algoritmo utilizará caso você não forneça um valor na coluna **Valor** .|  
|**Range**|Liste o intervalo de possíveis valores que se pode digitar na coluna **Valor** . Os intervalos podem ser um dos seguintes:<br /><br /> Uma lista discreta, como 1, 2, 3<br /><br /> Um intervalo inclusivo, como [0, 100]<br /><br /> Um intervalo exclusivo, como (0,...)<br /><br /> Uma combinação, como [0,...)|  
  
 **Descrição**  
 Descreve o parâmetro selecionado na lista **Parâmetros** .  
  
 **Adicionar**  
 Clique para adicionar à lista os parâmetros específicos ao algoritmo complementar. Após adicionar o parâmetro, você pode digitar o nome correto na coluna **Parâmetro** e fornecer um valor na coluna **Valor** .  
  
 **Removerr**  
 Clique para excluir um parâmetro personalizado da lista.  
  
 Se você excluir da lista um dos parâmetros de algoritmo do Analysis Services padrão, o parâmetro ainda será usado no modelo, mas com os valores padrão daquele parâmetro. O parâmetro não é excluído permanentemente e aparecerá da próxima vez que você abrir a caixa de diálogo.  
  
## <a name="see-also"></a>Consulte Também  
 [Algoritmos de mineração de dados &#40;mineração de dados Analysis Services&#41;](data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Exibição de modelos de mineração &#40;designer de modelo de mineração de dados&#41;](mining-models-view-data-mining-model-designer.md)   
 [Movendo objetos de mineração de dados](data-mining/moving-data-mining-objects.md)  
  
  
