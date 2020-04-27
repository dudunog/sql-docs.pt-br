---
title: Criar consultas de detalhamento usando DMX | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 42c896ee-e5ee-4017-b66e-31d1fe66d369
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f28d0503497fd066de2d328e75813f7b77026b2f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66085235"
---
# <a name="create-drillthrough-queries-using-dmx"></a>Criar consultas de detalhamento usando DMX
  Em todos os modelos com suporte ao detalhamento, você pode recuperar dados de caso e dados de estrutura criando uma consulta DMX no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou qualquer outro cliente que ofereça suporte a DMX.  
  
> [!WARNING]  
>  Para exibir os dados, o detalhamento precisa estar habilitado e você precisa ter as permissões necessárias.  
  
## <a name="specifying-drillthrough-options"></a>Especificando opções de detalhamento  
 A sintaxe geral é para recuperar casos de modelo e de estrutura como se segue:  
  
```  
SELECT <model column list>, StructureColumn('<structure column name') FROM <modelname>.CASES  
```  
  
 Para obter mais informações sobre como usar consultas DMX para retornar dados de caso, consulte [SELECT FROM &#60;model&#62;.CASES &#40;DMX&#41;](/sql/dmx/select-from-model-content-dmx) e [SELECT FROM &#60;structure&#62;.CASES](/sql/dmx/select-from-structure-cases).  
  
## <a name="examples"></a>Exemplos  
 A consulta DMX a seguir retorna os dados de caso para uma série de produtos específica, de um modelo de série temporal. A consulta também retorna a coluna `Amount`, que não foi usada no modelo, mas está disponível na estrutura de mineração.  
  
```  
SELECT [DateSeries], [Model Region], Quantity, StructureColumn('Amount') AS [M200 Pacific Amount]  
FROM Forecasting.CASES  
WHERE [Model Region] = 'M200 Pacific'  
```  
  
 Note que, neste exemplo, um alias foi usado para renomear a coluna de estrutura. Se você não atribuir um alias à coluna de estrutura, a coluna será retornada com o nome 'Expression'. Este é o comportamento padrão para todas as colunas sem nome.  
  
## <a name="see-also"></a>Consulte Também  
 [Consultas de detalhamento &#40;mineração de dados&#41;](drillthrough-queries-data-mining.md)   
 [Detalhamento em estruturas de mineração](drillthrough-on-mining-structures.md)  
  
  
