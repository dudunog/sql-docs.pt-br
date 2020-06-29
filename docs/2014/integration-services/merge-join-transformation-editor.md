---
title: Editor de transformação junção de mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.mergejointransformation.f1
helpviewer_keywords:
- Merge Join Transformation Editor
ms.assetid: ac06f419-30b3-42aa-8b34-42000bec4285
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1b74b8cd3e010f372cf0c0a50f5c0e19054924d0
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85424593"
---
# <a name="merge-join-transformation-editor"></a>Editor de Transformação Mesclagem
  Use a caixa de diálogo **Editor de Transformação Mesclar Junção** para especificar o tipo de junção, as colunas de junção e as colunas de saída para mesclar duas entradas combinadas por uma junção.  
  
> [!IMPORTANT]  
>  A Transformação Junção de Mesclagem requer dados classificados para suas entradas. Para obter mais informações sobre este requisito importante, consulte [Classificar dados para as transformações Mesclagem e Junção de Mesclagem](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md).  
  
 Para saber mais sobre transformação Mesclagem de Junção, consulte [Merge Join Transformation](data-flow/transformations/merge-join-transformation.md).  
  
## <a name="options"></a>Opções  
 **Tipo de junção**  
 Especifique se você quer usar uma junção interna, externa esquerda ou completa.  
  
 **Trocar Entradas**  
 Troque a ordem entre entradas usando o botão **Trocar Entradas** . Essa seleção pode ser útil com a opção de Junção externa esquerda.  
  
 **Entrada**  
 Para cada coluna que você desejar na saída mesclada, selecione primeiro na lista de entradas disponíveis.  
  
 São exibidas entradas em duas tabelas separadas. Selecione colunas a serem incluídas na saída. Arraste colunas para criar uma junção entre as tabelas. Para excluir uma junção, selecione-a e pressione a tecla DELETE.  
  
 **Coluna de Entrada**  
 Selecione uma coluna a incluir na saída mesclada da lista de colunas disponíveis na entrada selecionada.  
  
 **Alias de saída**  
 Digite um alias para cada coluna de saída. O padrão é o nome da coluna de entrada; no entanto, é possível escolher qualquer nome descritivo exclusivo.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Classificar dados para as transformações mesclagem e junção de mesclagem](data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)   
 [Estender um conjunto de um DataSet usando a transformação junção de mesclagem](data-flow/transformations/extend-a-dataset-by-using-the-merge-join-transformation.md)   
 [Transformação Mesclar](data-flow/transformations/merge-transformation.md)   
 [Transformação Unir Tudo](data-flow/transformations/union-all-transformation.md)  
  
  
