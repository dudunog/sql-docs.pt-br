---
title: Definir referência de moeda local (Assistente de Business Intelligence) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.localcurrency.f1
ms.assetid: 74993b0d-dfca-476b-acba-d66c593680a5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 558e2c7d62edcb9fb314b49d41fd7bd15413218d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66082175"
---
# <a name="define-local-currency-reference-business-intelligence-wizard"></a>Definir Referência de Moeda Local (Assistente de Business Intelligence)
  Use a página **Definir Referência de Moeda Local** para definir as moedas locais para a funcionalidade de conversão de moedas que cobre os tipos de conversão muitos para muitos ou muitos para um especificados na página **Selecionar Tipo de Conversão** . Uma moeda local é a moeda na qual as transações de medidas selecionadas na página **Selecionar Medidas** estão armazenadas.  
  
> [!NOTE]  
>  Essa página não será exibida se o Assistente de Business Intelligence tiver sido iniciado no Designer de Dimensão ou clicando com o botão direito do mouse em uma dimensão no Gerenciador de Soluções no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Esta página também não será exibida se a opção **Um para Muitos** foi selecionada na página **Selecionar Tipo de Conversão** .  
  
## <a name="options"></a>Opções  
 **Identificadores da tabela de fatos**  
 Selecione para especificar um atributo que forneça identificadores de moedas locais em uma dimensão de moedas referenciada pela tabela de fatos que contém as medidas selecionadas na página **Selecionar Medidas** . (Uma dimensão de moeda em uma `Type` cuja propriedade é definida como *moeda*.)  
  
 Use esta opção quando a própria transação determinar a moeda local daquela transação. Por exemplo [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , no banco de dados de[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]exemplo –, o grupo de medidas Vendas pela Internet tem uma relação de dimensão regular com a dimensão moeda. A tabela de fatos desse grupo de medidas contém uma coluna de chave estrangeira que faz referência aos identificadores de moedas na tabela de dimensões daquela dimensão.  
  
 **Dimensão e atributo de moeda referenciados pelos dados de fato**  
 Selecione o atributo de moeda dentro de uma dimensão de moedas cujos membros representam identificadores de moedas locais. (Um atributo de moeda é aquele `Type` cuja propriedade é definida como *Currency*.)  
  
> [!NOTE]  
>   Esta opção não estará disponível se a opção **Identificadores da tabela de fatos** não estiver selecionada.  
  
 **Atributos da tabela de dimensões**  
 Selecione para especificar um atributo de uma dimensão relacionada ao grupo de medidas que contém identificadores de moedas locais.  
  
 Use esta opção quando a relação entre uma transação e outra entidade corporativa, como um local, determinar a moeda local daquela transação. Por exemplo, no banco [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de dados de[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]exemplo –, o grupo de medidas relatório financeiro tem uma relação de dimensão referenciada com a dimensão moeda por meio da dimensão organização. Isto é, a tabela de fatos do grupo de medidas Relatório Financeiro contém uma coluna de chave estrangeira que faz referência a membros na tabela de dimensões daquela dimensão. A tabela de dimensões da dimensão Organização, por sua vez, contém uma coluna de chave estrangeira que faz referência aos identificadores de moedas na tabela de dimensões Moeda.  
  
 **Atributo de dimensão que faz referência à moeda**  
 Selecione o atributo dentro de uma dimensão cujos membros fazem referência a identificadores de moeda local.  
  
> [!NOTE]  
>   Esta opção não estará disponível se a opção **Atributos da tabela de dimensões** não estiver selecionada.  
  
## <a name="see-also"></a>Consulte Também  
 [Ajuda F1 do assistente de Business Intelligence](business-intelligence-wizard-f1-help.md)   
 [O designer de cubo &#40;Analysis Services-dados multidimensionais&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [O designer de dimensão &#40;Analysis Services de dados multidimensionais&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
