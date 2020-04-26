---
title: Otimizar o desempenho da replicação de mesclagem com artigos de somente download | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], download-only articles
- articles [SQL Server replication], download-only
- download-only articles
ms.assetid: 8851faa6-e6df-4ea5-a6ea-2a3471680fa3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5ca661105c28cab2bf3e881cf262922e95da5eed
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "63250365"
---
# <a name="optimize-merge-replication-performance-with-download-only-articles"></a>Otimizar o desempenho de replicação de mesclagem com artigos de somente download
  A replicação de mesclagem oferece dois tipos de artigo diferentes para endereçar as diferentes necessidades de aplicativo. Publicações podem conter um ou mais destes tipos de artigo conforme for apropriado para o aplicativo:  
  
-   Artigos padrão  
  
-   artigos de somente download  
  
 Os artigos de somente download fornecem vantagens de desempenho sobre os artigos padrão e são usados onde apropriado.  
  
> [!NOTE]  
>  Para usar artigos de somente download, o nível de compatibilidade da publicação deve ser pelo menos 90RTM.  
  
## <a name="standard-articles"></a>Artigos padrão  
 Artigos padrão são o padrão, oferecendo o intervalo completo de recursos de replicação de mesclagem, inclusive avançada detecção de conflito e resolução. Artigos padrão são apropriados para tabelas que são atualizadas por Assinantes múltiplos; Objetos diferentes de tabelas, como procedimentos armazenados e exibições, são sempre publicados como artigos padrão.  
  
## <a name="download-only-articles"></a>artigos de somente download  
 Os artigos de somente download são projetados para aplicativos com dados que não são atualizados nos Assinantes, como um conjunto de artigos que faz parte de um catálogo de produto. Um catálogo de produto é normalmente atualizado ao Publicador, mas não nos Assinantes. Como artigos somente para download não podem ser atualizados no Assinante, metadados de controle não são enviados aos Assinantes. Isso pode resultar em armazenamento reduzido nos Assinantes e em um benefício no desempenho, principalmente se a conexão de rede for lenta.  
  
 Os artigos de somente download funcionam em conjunto com assinaturas de cliente: se um artigo for designado como somente para download, as linhas para esse artigo não podem ser inseridas, atualizadas ou excluídas nos Assinantes que usam assinaturas de cliente. Publicadores e Assinantes que usam tipo de assinatura de servidor (normalmente Assinantes que republicam dados de outros Assinantes) podem inserir, atualizar e excluir dados. Para obter mais informações sobre assinaturas de cliente, consulte [Assinar publicações](../subscribe-to-publications.md).  
  
 Para especificar que um artigo é somente download, consulte [Especificar que um novo artigo de tabela de mesclagem é somente download](../publish/specify-merge-replication-properties.md#download-only).  
  
## <a name="using-different-article-types-in-your-applications"></a>Usando tipos diferentes de artigos em seus aplicativos  
 Entendendo os requisitos de seu aplicativo, você pode alternar entre máxima flexibilidade e desempenho ideal. Por exemplo, aplicativos com vários conflitos e alterações tanto no Publicador quanto do Assinante usarão a publicação criada a partir de artigos padrão. Alguns aplicativos, como o aplicativo de automação de departamento de vendas, poderiam ter artigos com um potencial para conflitos, e outros artigos que têm a função de tabelas de pesquisa, que podem ser especificados como somente para download. Aplicativos de entrada de dados, como aplicativos de sistemas de ponto de venda e automação de campo, frequentemente particionam os dados de forma que os conflitos são eliminados, e os dados de um Assinante nunca vão a outro. Nessas situações, uma combinação de partições não sobrepostas, artigos de somente download e partições pré-computadas fornecem o melhor desempenho e escalabilidade. Para obter mais informações sobre partições não sobrepostas e partições pré-computadas, consulte [Parameterized Row Filters](parameterized-filters-parameterized-row-filters.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de artigo para replicação de mesclagem](article-options-for-merge-replication.md)   
 [Otimizar o desempenho da replicação de mesclagem com o controle de exclusão condicional](optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
  
  
