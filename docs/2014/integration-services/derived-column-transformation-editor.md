---
title: Editor de transformação coluna derivada | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.derivedcolumntransformation.f1
helpviewer_keywords:
- Derived Column Transformation Editor
ms.assetid: ff73923e-d245-43d8-bf24-af3bdc942e51
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3983e75bdde3379fac48a74a595959af2568a3ab
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84951646"
---
# <a name="derived-column-transformation-editor"></a>Editor de Transformação Colunas Derivadas
  Use a caixa de diálogo **Editor de Transformação Colunas Derivadas** para criar expressões que populem colunas novas ou de substituição.  
  
 Para saber mais sobre a transformação Coluna Derivada, consulte [Transformação Coluna Derivada](data-flow/transformations/derived-column-transformation.md).  
  
## <a name="options"></a>Opções  
 **Variáveis e Colunas**  
 Crie uma expressão que use uma variável ou uma coluna de entrada arrastando a variável ou coluna da lista de variáveis e colunas disponíveis para uma linha de tabela existente no painel abaixo, ou para uma linha nova no final da lista.  
  
 **Funções e operadores**  
 Crie uma expressão que use uma função ou um operador para avaliar dados de entrada e dados de saída diretos arrastando funções e operadores da lista para o painel abaixo.  
  
 **Nome da coluna derivada**  
 Forneça um nome de coluna derivada. O padrão é uma lista numerada de colunas derivadas; no entanto, é possível escolher qualquer nome descritivo exclusivo.  
  
 **Coluna derivada**  
 Selecione uma coluna derivada da lista. Escolha se deseja adicionar a coluna derivada como uma nova coluna de saída ou substituir os dados em uma coluna existente.  
  
 **Expressão**  
 Digite uma expressão ou compile uma arrastando da lista anterior de colunas, variáveis, funções e operadores disponíveis.  
  
 O valor dessa propriedade pode ser especificado com uma expressão de propriedades.  
  
 **Tópicos relacionados**: [Expressões do Integration Services &#40;SSIS&#41;](expressions/integration-services-ssis-expressions.md), [Operadores &#40;Expressão SSIS&#41;](expressions/operators-ssis-expression.md) e [Funções &#40;Expressão SSIS&#41;](expressions/functions-ssis-expression.md)  
  
 **Tipo de Dados**  
 Se acrescentar dados a uma nova coluna, a caixa de diálogo **TransformationEditor de Coluna Derivada** avaliará a expressão automaticamente e definirá o tipo de dados adequadamente. O valor desta coluna é somente leitura. Para obter mais informações, consulte [Integration Services Data Types](data-flow/integration-services-data-types.md).  
  
 **Comprimento**  
 Se acrescentar dados a uma nova coluna, a caixa de diálogo **TransformationEditor de Coluna Derivada** avaliará a expressão automaticamente e definirá a largura de coluna para os dados da cadeia de caracteres. O valor desta coluna é somente leitura.  
  
 **Precisão**  
 Se acrescentar dados a uma nova coluna, a caixa de diálogo **TransformationEditor de Coluna Derivada** automaticamente definirá a precisão de dados numéricos com base no tipo de dados. O valor desta coluna é somente leitura.  
  
 **Escala**  
 Se acrescentar dados a uma nova coluna, a caixa de diálogo **TransformationEditor de Coluna Derivada** automaticamente definirá a escala dos dados numéricos com base no tipo de dados. O valor desta coluna é somente leitura.  
  
 **Página de código**  
 Se acrescentar dados a uma nova coluna, a caixa de diálogo **TransformationEditor de Coluna Derivada** automaticamente definirá a página de código para o tipo de dados DT_STR. Será possível atualizar a **Página de Código**.  
  
 **Configurar saída de erro**  
 Especifique como tratar os erros usando a caixa de diálogo [Configurar Saída de Erro](../../2014/integration-services/configure-error-output.md) .  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Derivar valores de coluna por meio da transformação Coluna Derivada](data-flow/transformations/derive-column-values-by-using-the-derived-column-transformation.md)  
  
  
