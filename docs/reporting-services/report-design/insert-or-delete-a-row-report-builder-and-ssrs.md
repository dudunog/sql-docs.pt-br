---
title: Inserir ou excluir uma linha (Construtor de Relatórios) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: b9642af3-b3ae-4f78-b0be-8f96b79fc313
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6bdec71e808d577a764d2b0cc3fa99fc9cd522fd
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77082024"
---
# <a name="insert-or-delete-a-row-report-builder-and-ssrs"></a>Inserir ou excluir uma linha (Construtor de Relatórios e SSRS)
Você pode adicionar ou excluir linhas em uma região de dados tablix em um relatório paginado do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Essa região pode ser uma tabela, uma matriz ou uma lista. Os procedimentos a seguir não se aplicam às regiões de dados de gráficos e medidores.  
  
 Na região de dados Tablix, você pode adicionar linhas associadas a um grupo (dentro de um grupo) ou que não estão associadas a um grupo (fora de um grupo). Uma linha que está dentro de um grupo é repetida uma vez por valor de grupo único. Por exemplo, uma linha dentro de um grupo com base em valor em uma coluna de dados que contém nomes de cores é repetida uma vez por nome de cor distinto. Para grupos aninhados, uma linha pode estar fora do grupo filho, mas dentro do grupo pai. Nesse caso, a linha se repete uma vez para cada valor único no grupo pai.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="to-select-a-data-region-so-the-row-and-column-handles-appear"></a>Para selecionar uma região de dados para que os identificadores de linha e coluna sejam exibidos  
  
-   No modo Design, clique no canto superior esquerdo da região de dados Tablix para que os indicadores de linha e coluna sejam exibidos acima ou próximo dele.  
  
     Para obter mais informações sobre áreas de regiões de dados, consulte [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md).  
  
## <a name="to-insert-a-row-in-a-selected-data-region"></a>Para inserir uma linha em uma região de dados selecionada  
  
-   Clique com o botão direito do mouse no identificador de linha no qual você deseja inserir uma linha, clique em **Inserir Linha**e depois em **Acima** ou **Abaixo**.  
  
     \- ou –  
  
-   Clique com o botão direito do mouse em uma célula na região de dados na qual você deseja inserir uma linha, clique em **Inserir Linha**e depois em **Acima** ou **Abaixo**.  
  
## <a name="to-delete-a-row-from-a-selected-data-region"></a>Para excluir uma linha de uma região de dados selecionada  
  
-   Selecione uma ou mais linhas a serem excluídas, clique com o botão direito do mouse no identificador de uma das linhas selecionadas e clique em **Excluir Linhas**.  
  
     \- ou –  
  
-   Clique com o botão direito do mouse em uma célula na região de dados na qual você deseja excluir uma linha e clique em **Excluir Linhas**.  
  
## <a name="to-insert-a-row-in-a-group-in-a-selected-data-region"></a>Para inserir uma linha em um grupo em uma região de dados selecionada  
  
-   Clique com o botão direito do mouse em uma célula de grupo de linhas na área de grupo de linhas de uma região de dados Tablix na qual deseja inserir uma linha, clique em **Inserir Linha**e depois em **Acima – Fora do Grupo**, **Acima – Dentro do Grupo**, **Abaixo – Dentro do Grupo**ou **Abaixo – Fora do Grupo**.  
  
     Uma linha é adicionada dentro ou fora do grupo representado pela célula do grupo de linhas na qual você clicou.  
  
## <a name="to-delete-a-row-from-a-group-in-a-selected-data-region"></a>Para excluir uma linha de um grupo em uma região de dados selecionada  
  
-   Clique com o botão direito do mouse em uma célula do grupo de linhas na área do grupo de colunas de uma região de dados Tablix na qual você deseja excluir uma linha e clique em **Excluir Linhas**.  
  
## <a name="see-also"></a>Consulte Também  
 [Região de dados Tablix &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tablix-data-region-report-builder-and-ssrs.md)   
 [Noções básicas sobre grupos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/understanding-groups-report-builder-and-ssrs.md)   
 [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md)   
 [Matrizes &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/create-a-matrix-report-builder-and-ssrs.md)   
 [Listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md)     
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
