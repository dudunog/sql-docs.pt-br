---
title: Excluir uma coluna de um modelo de mineração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- excluding mining model columns
- mining models [Analysis Services], columns
- columns [data mining], excluding
ms.assetid: 404fe5fe-3ba2-4b9b-8780-0d02343d467f
author: minewiskan
ms.author: owend
ms.openlocfilehash: 30affebc143184c6287858f60b5d4f5d089c322a
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84522467"
---
# <a name="exclude-a-column-from-a-mining-model"></a>Excluir uma coluna de um modelo de mineração
  Ao criar um novo modelo de mineração, talvez você não queira usar todas as colunas existentes na estrutura de mineração em que o modelo é baseado. Por exemplo, você pode ter adicionado uma coluna de nome de cliente para detalhamento, mas não deseja usá-la para modelagem. Ou você pode decidir criar várias cópias de uma coluna com discretizações diferentes e usar apenas uma das cópias em cada modelo, ignorando as demais. Você também pode adicionar seletivamente colunas de entrada em vários modelos diferentes para ver como a variável adicionada afeta a coluna de saída.  
  
 Você não precisa criar uma nova estrutura de mineração para cada combinação de colunas; basta sinalizar uma coluna como não sendo usado em um modelo específico.  
  
### <a name="to-exclude-a-column-from-a-mining-model"></a>Para excluir uma coluna de um modelo de mineração  
  
1.  Na guia **Modelos de Mineração** no Designer de Mineração de Dados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], selecione a célula que corresponde à coluna que deseja excluir no modelo de mineração apropriado.  
  
2.  Selecione **Ignorar** na caixa de listagem suspensa.  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas e instruções do modelo de mineração](mining-model-tasks-and-how-tos.md)  
  
  
