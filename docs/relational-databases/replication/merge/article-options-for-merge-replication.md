---
description: Opções de artigo para replicação de mesclagem
title: Opções do artigo para replicação de mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], article options
- articles [SQL Server replication], merge replication options
ms.assetid: 670abd41-d204-4cd7-a371-7664e603a0ce
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: eb832433ad5274bf63467327fc6ad8273ff4cc35
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465206"
---
# <a name="article-options-for-merge-replication"></a>Opções de artigo para replicação de mesclagem
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Há muitas opções para a mesclagem de artigos de tabela que lhe possibilitam personalizar o comportamento de replicação para as necessidades de seus aplicativos. Usando a replicação de mesclagem, você pode fazer o seguinte:  
  
-   Usar filtros de linha, filtros de junção e filtros de coluna. Filtrar artigos de tabela lhe permite criar partições de dados a serem publicados. Para obter mais informações, consulte [Filter Published Data](../../../relational-databases/replication/publish/filter-published-data.md) (Filtrar dados publicados).  
  
-   Especificar se as alterações feitas ao Assinante foram carregadas no Publicador. Para aplicativos nos quais alguns ou todos os dados deverão ser somente leitura no Assinante, artigos de somente download melhoram o desempenho. Para obter mais informações, consulte [Otimizar o desempenho da replicação de mesclagem com artigos somente para download](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
-   Especificar quais exclusões para um ou mais artigos não deveriam ser rastreados por gatilhos de replicação e tabelas do sistema. Esta opção pode ser útil em muitos cenários de aplicativo. Estes, incluem cenários que usam exclusões de lote que não precisem ser reproduzidos. Para obter mais informações, consulte [Otimizar o desempenho da replicação de mesclagem com o controle de exclusão condicional](../../../relational-databases/replication/merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md).  
  
-   Especificar a ordem de processamento dos artigos para garantir que os artigos sejam processados na ordem requerida pelo seu aplicativo. Para obter mais informações, confira [Especificar opções de replicação de mesclagem](../../../relational-databases/replication/merge/specify-merge-replication-properties.md).  
  
-   Especificar que um conjunto de relatórios relacionados deva ser processado como uma unidade (por padrão, replicação de mesclagem processa alterações nas tabelas de linha a linha). Para obter mais informações, consulte [Agrupar alterações a linhas relacionadas com registros lógicos](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md).  
  
-   Usar detecção de conflito e resolução para casos em que os mesmos dados possam ser alterados em mais de um nó na topologia. Para obter mais informações, consulte [Detectar e resolver conflitos de replicação de mesclagem](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
-   Especificar opções de esquema se as restrições e os gatilhos são copiados para o Assinante. Para obter mais informações, veja [Especificar opções de esquema](../../../relational-databases/replication/publish/specify-schema-options.md).  
  
-   Use um manipulador de lógica de negócios para responder a muitas condições durante a sincronização. Que incluem alterações de dados, conflitos e erros. Para obter mais informações, consulte [Executar lógica de negócios durante a sincronizações de mesclagem](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
