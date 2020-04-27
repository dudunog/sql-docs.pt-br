---
title: Operadores unários em dimensões pai-filho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- UnaryOperatorColumn property
- attributes [Analysis Services], unary operators
- unary operators
ms.assetid: b8ef549c-5458-458a-bf1a-fd743a1417fd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 25c1acf7a1fadbc79b7781488143ce57881c81fc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66073452"
---
# <a name="unary-operators-in-parent-child-dimensions"></a>Operadores unários em dimensões pai-filho
  Em uma dimensão que contém uma relação pai-filho no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você especifica uma coluna de operador unário (ou rollup personalizado) que determina o rollup personalizado para todos os membros não calculados do atributo pai. O operador unário é aplicado aos membros sempre que os valores dos membros pai são avaliados. A **UnaryOperatorColumn** em um atributo pai (**Usage**=Pai) especifica a coluna de uma tabela da exibição da fonte de dados que contém operadores unários. Os valores dos operadores de acúmulo personalizado armazenados nessa coluna são aplicados a cada membro do atributo.  
  
 Você pode criar e especificar um cálculo nomeado em uma tabela de dimensões da exibição da fonte de dados como coluna de operador unário. A expressão mais simples, como '+', retorna o mesmo operador para todos os membros. Mas é possível usar qualquer expressão desde que ela retorne um operador para cada membro.  
  
 Você pode alterar a propriedade **UnaryOperatorColumn** manualmente em um atributo pai ou usar o aprimoramento de Definir Agregação Personalizada do Assistente de Business Intelligence para substituir a agregação padrão que é associada aos membros de uma dimensão. Para obter mais informações sobre como usar o Assistente de Business Intelligence para executar essa configuração, consulte [Adicionar uma agregação personalizada a uma dimensão](bi-wizard-add-a-custom-aggregation-to-a-dimension.md).  
  
 A configuração padrão para a propriedade **UnaryOperatorColumn** de um atributo pai é (nenhum), que desabilita os operadores de rollup personalizado. A tabela a seguir lista os operadores unários e descreve como eles se comportam quando são aplicados a um nível.  
  
|Operador unário|Descrição|  
|--------------------|-----------------|  
|+ (sinal de mais)|O valor do membro é adicionado ao valor de agregação dos membros irmãos que ocorrem antes do membro. Esse operador será o operador padrão se nenhuma coluna de operador unário for definida para um atributo.|  
|-(sinal de subtração)|O valor do membro é subtraído do valor de agregação dos membros irmãos que ocorrem antes do membro.|  
|* (asterisco)|O valor do membro é multiplicado pelo valor de agregação dos membros irmãos que ocorrem antes do membro.|  
|/ (barra)|O valor do membro é dividido pelo valor de agregação dos membros irmãos que ocorrem antes do membro.|  
|~ (til)|O valor do membro é ignorado.|  
  
 Valores em branco e outros valores que não forem encontrados na tabela serão tratados como o operador unário sinal de mais (+). Não há precedência de operador, portanto, a ordem dos membros conforme armazenados na coluna de operador unário determina a ordem de avaliação. Para alterar a ordem de avaliação, crie um novo atributo, configure sua propriedade **Type** como **Sequence**e atribua números consecutivos correspondentes à ordem de avaliação da propriedade **Source Column** . Você também deve ordenar os membros do atributo por esse atributo. Para obter informações sobre como usar o Assistente de Business Intelligence para ordenar os membros de um atributo, consulte [Definir a ordenação para uma dimensão](bi-wizard-define-the-ordering-for-a-dimension.md).  
  
 É possível usar a propriedade **UnaryOperatorColumn** para especificar um cálculo nomeado que retorna um operador unário como caractere literal para todos os membros do atributo. Para isso, basta digitar um caractere literal, como `'*'` , no cálculo nomeado. Ele substituiria o operador padrão, o sinal de mais (+), pelo operador de multiplicação, o asterisco (*), em todos os membros do atributo. Para obter mais informações, consulte [definir cálculos nomeados em uma exibição da fonte de dados &#40;Analysis Services&#41;](define-named-calculations-in-a-data-source-view-analysis-services.md).  
  
 Na guia **Navegador** do Designer de Dimensão, é possível exibir os operadores unários ao lado de cada membro de uma hierarquia. Também é possível alterar os operadores unários ao trabalhar com uma dimensão habilitada para gravação. Se a dimensão não estiver habilitada para gravação, use uma ferramenta para modificar diretamente a fonte de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de propriedades de atributo de dimensão](dimension-attribute-properties-reference.md)   
 [Operadores de rollup personalizado em dimensões pai-filho](parent-child-dimension-attributes-custom-rollup-operators.md)   
 [Iniciar o Assistente de Business Intelligence no Designer de Dimensão](database-dimensions-bi-wizard-in-dimension-designer.md)  
  
  
