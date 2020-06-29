---
title: 'Lição 4: adicionando o redirecionamento de fluxo de erro | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 0c8dbda2-75e3-4278-9b4e-dcd220c92522
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a8ebde9465a5f6f9f591e5d175aa7ed26c5c2fca
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440433"
---
# <a name="lesson-4-adding-error-flow-redirection"></a>Lição 4: Adicionar redirecionamento de fluxo de erro
  Para lidar com erros que podem ocorrer no processo de transformação, [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] o oferece a capacidade de decidir por componente e por coluna como manipular dados que não podem ser transformados. Você pode escolher ignorar uma falha em determinadas colunas, redirecionar toda a linha com falha ou apenas causar falha no componente. Por padrão, todos os componentes no [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] são configurados para falhar quando ocorrerem erros. Causar falha em um componente, por sua vez, faz com que o pacote falhe e todo o processamento subsequente pare.  
  
 Em vez de permitir que as falhas interrompam a execução do pacote, é bom configurar e tratar erros de processamento em potencial conforme ocorrem dentro da transformação. Como você pode escolher ignorar as falhas para garantir que seu pacote seja executado com êxito, frequentemente é melhor redirecionar a linha com falhas para outro caminho de processamento, em que os dados e o erro podem ser persistentes, examinados e reprocessados posteriormente.  
  
 Nesta lição, você criará uma cópia do pacote desenvolvido em [Lesson 3: Adding Logging](lesson-3-add-logging-with-ssis.md). Ao trabalhar com este pacote novo, você criará uma versão corrompida de um dos arquivos de dados de exemplo. O arquivo corrompido forçará a ocorrência de um erro de processamento quando você executar o pacote.  
  
 Para tratar os dados de erro, você adicionará e configurará um destino de Arquivo Simples que gravará qualquer linha que não localize um valor de pesquisa na transformação Pesquisa de Códigos de Moeda em um arquivo.  
  
 Antes que os dados de erro sejam gravados em um arquivo, você incluirá um componente Script que utiliza script para obter as descrições de erro. Você reconfigurará, então, a transformação Pesquisa de Códigos de Moeda para redirecionar qualquer dado que não possa ser processado para a transformação Script.  
  
> [!IMPORTANT]  
>  Este tutorial requer o banco de dados de exemplo **AdventureWorksDW2012** . Para obter mais informações sobre como instalar e implantar o **AdventureWorksDW2012**, consulte [Reporting Services Product Samples on CodePlex (Amostras de produto do Reporting Services no CodePlex)](https://go.microsoft.com/fwlink/p/?LinkId=526910).  
  
## <a name="tasks-in-lesson"></a>Tarefas da lição  
 Esta lição contém as seguintes tarefas:  
  
-   [Etapa 1: Copiar o pacote da Lição 3](lesson-4-1-copying-the-lesson-3-package.md)  
  
-   [Etapa 2: Criar um arquivo corrompido](lesson-4-2-creating-a-corrupted-file.md)  
  
-   [Etapa 3: Adicionar redirecionamento de fluxo de erro](lesson-4-3-adding-error-flow-redirection.md)  
  
-   [Etapa 4: Adicionar um destino de arquivo simples](lesson-4-4-adding-a-flat-file-destination.md)  
  
-   [Etapa 5: Testar o pacote de tutorial da Lição 4](lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar a lição  
 [Etapa 1: Copiar o pacote da Lição 3](lesson-4-1-copying-the-lesson-3-package.md)  
  
  
