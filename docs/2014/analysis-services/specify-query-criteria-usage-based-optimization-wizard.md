---
title: Especificar critérios de consulta (Assistente de otimização com base no uso) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.usagebasedoptimizationwizard.specifyquerycriteria.f1
ms.assetid: 3193adc2-af9f-4234-a4cc-dea0c280a724
author: minewiskan
ms.author: owend
ms.openlocfilehash: ba9e131a8986b01a6bb897e35b2e45b2bb70ccd0
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940337"
---
# <a name="specify-query-criteria-usage-based-optimization-wizard"></a>Especificar Critérios de Consulta (Assistente de Otimização com Base no Uso)
  Use a página **Especificar Critérios de Consulta** para escolher uma ou mais opções de filtro para identificar as consultas a serem otimizadas.  
  
> [!NOTE]  
>  Essa página será desabilitada se o [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] não puder se conectar com o log de consultas.  
  
## <a name="options"></a>Opções  
 **Estatísticas de log de consultas**  
 Exibe informações sobre as consultas armazenadas no log de consultas das partições selecionadas. Os seguintes itens são exibidos:  
  
|Termo|Definição|  
|----------|----------------|  
|**Total de consultas**|Exibe o número total de consultas armazenadas no log de consultas das partições selecionadas.|  
|**Consultas distintas**|Exibe o número de consultas distintas armazenadas no log de consultas das partições selecionadas.|  
|**Usuários distintos**|Exibe o número total de usuários distintos associados às consultas armazenadas no log de consultas das partições selecionadas.|  
|**Tempo médio de resposta**|Exibe o tempo médio de resposta das consultas armazenadas no log de consultas das partições selecionadas.|  
  
 **Data de início**  
 Filtra consultas no log de consultas com base em uma data e hora de início. Escolha ou digite uma data na lista suspensa.  
  
> [!NOTE]  
>   Se a **Data de término** não for selecionada, todas as consultas no log de consultas na data e hora especificadas ou para essa opção ou posteriores serão consideradas.  
  
 **Data de término date**  
 Filtra consultas no log de consultas com base em uma data e hora de término. Escolha ou digite uma data na lista suspensa.  
  
> [!NOTE]  
>   Se a **Data de início** não for selecionada, todas as consultas no log de consultas antes ou na data e hora especificadas para essa opção serão consideradas.  
  
 **Usuários**  
 Filtra consultas no log de consultas com base em um conjunto de usuários especificado. Clique no botão de reticências (**...**) para exibir a caixa de diálogo **Seleção de Usuários** e escolher os usuários nos quais filtrar consultas. Para obter mais informações sobre a caixa de diálogo **Seleção de Usuários**, consulte [Caixa de diálogo Seleção de Usuários &#40;Analysis Services – Dados Multidimensionais&#41;](user-selection-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Consultas mais frequentes**  
 Filtra consultas no log de consultas com base na porcentagem mais alta de consultas distintas executadas com maior frequência para as partições selecionadas. Escolha ou digite um valor percentual na caixa de texto.  
  
## <a name="see-also"></a>Consulte Também  
 [Ajuda F1 do assistente de otimização com base no uso](usage-based-optimization-wizard-f1-help.md)   
 [Analysis Services assistentes &#40;dados multidimensionais&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
