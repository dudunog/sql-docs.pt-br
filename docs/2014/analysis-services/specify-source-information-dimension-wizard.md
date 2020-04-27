---
title: Especificar informações de origem (Assistente para dimensões) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.dimensionmaintable.f1
ms.assetid: 0538b490-5185-49e1-a783-4ce3539a0de5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 30234275a724dddce95cdad66e5e37a382a25e62
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66068176"
---
# <a name="specify-source-information-dimension-wizard"></a>Especificar Informações sobre a Origem (Assistente de Dimensão)
  Use a página **Selecionar a Tabela de Dimensões Principal** para selecionar a exibição da fonte de dados, a tabela de dimensões principal, as colunas de chave e a coluna de nome de membro para a dimensão a ser criada.  
  
 **Para abrir o Assistente para Dimensões**  
  
-   No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], no **Gerenciador de Soluções**, clique com o botão direito do mouse na pasta **Dimensões** de um projeto do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e clique em **Nova Dimensão**.  
  
## <a name="options"></a>Opções  
 **Exibição da fonte de dados**  
 Selecione uma exibição da fonte de dados.  
  
 **Tabela principal**  
 Selecione uma tabela da exibição da fonte de dados selecionada para usar como tabela principal para a dimensão.  
  
 **Colunas de chave**  
 Selecione as colunas de chave da tabela especificada na **Tabela Principal** para o atributo de chave da dimensão.  
  
> [!NOTE]  
>  Mais de uma coluna pode ser selecionada. Se a tabela contiver uma chave primária composta, selecione todas as colunas incluídas na chave primária composta. A ordem das colunas de chave é importante.  
  
 **Coluna de Nome**  
 Selecione a coluna da tabela especificada na **Tabela Principal** que oferece os nomes de membros para a dimensão. Uma coluna de nomes deve ser especificada quando uma chave composta for usada. Para criar uma coluna de nomes para uma chave composta, recomendamos criar um cálculo nomeado na exibição da fonte de dados que concatene as colunas de chave especificadas. Quando uma única chave for usada, a coluna de nome é opcional.  
  
## <a name="see-also"></a>Consulte Também  
 [Ajuda F1 do assistente para dimensões](dimension-wizard-f1-help.md)   
 [Dimensões &#40;Analysis Services de dados multidimensionais&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Dimensões em modelos multidimensionais](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
