---
title: Editor Resolver Referência de Coluna | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.resolvereferences.preview.F1
- sql13.dts.designer.resolvereferences.mapper.F1
ms.assetid: bb3ee33c-79c4-4c76-a82f-71581b4a60f1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 28ff4c49c2b1dadcde15171a2a5102f29e3ff438
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86915352"
---
# <a name="resolve-column-reference-editor"></a>Resolver editor de referência de coluna

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Quando um caminho de entrada é desconectado ou se houver qualquer coluna não mapeada no caminho, um ícone de erro será exibido ao lado do caminho de dados correspondente. Para simplificar a resolução de erros de referência de coluna, o editor Resolver Referências permite vincular colunas de saída não mapeadas com colunas de entrada não mapeadas para todos os caminhos da árvore de execução. O editor Resolver Referências também realçará os caminhos para indicar quais caminhos estão sendo resolvidos.  
  
> [!NOTE]  
>  É possível editar um componente até mesmo quando seu caminho de entrada está desconectado  
  
 Depois que todas as referências a coluna foram resolvidas, se não houver erros de caminho de dados, nenhum ícone de erro será exibido ao lado dos caminhos de dados.  
  
## <a name="options"></a>Opções  
 **Colunas de Saída Não Mapeadas (Origem)**     
 Colunas do caminho upstream que não estão mapeadas no momento  
  
**Colunas Mapeadas (Origem)**     
 Colunas do caminho upstream que estão mapeadas para colunas do caminho downstream  
  
**Colunas Mapeadas (Destino)**     
 Colunas do caminho upstream que estão mapeadas para colunas do caminho downstream  
  
**Colunas de Entrada Não Mapeadas (Destino)**     
 Colunas do caminho downstream que não estão mapeadas no momento  
  
**Excluir Colunas de Entrada Não Mapeadas**  
 Selecione Excluir Colunas de Entrada Não Mapeadas para ignorar colunas não mapeadas no destino do caminho de dados. O botão Visualizar Alterações exibe uma lista das alterações que ocorrerão quando você pressionar o botão OK.  
  
  
