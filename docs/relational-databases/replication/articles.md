---
description: Artigos
title: Artigos | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.articles.f1
ms.assetid: 7c743dc6-6c6d-4c92-b711-842e1b0b273e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 5198b93db0372a1bd16fa99a7c0b65feeac70aa4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427998"
---
# <a name="articles"></a>Artigos
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  Na página **Artigos** , você especifica quais objetos de banco de dados incluir como artigos na publicação. Se você estiver publicando um objeto de banco de dados que depende de outros objetos de banco de dados, terá de publicar todos os objetos referenciados. Por exemplo, se você publicar uma exibição que depende de uma tabela, terá de publicar a tabela também.  
  
 Objetos que não podem ser publicados têm um ícone vermelho próximo a eles, com uma explicação no painel de informações na parte inferior da página do assistente. Os objetos seguintes não podem ser publicados:  
  
-   Objetos criptografados.  
  
-   Tabelas sem chaves primárias não podem ser publicadas em publicações transacionais.  
  
-   Tabelas não podem ser publicadas em uma publicação de mesclagem e em uma publicação transacional habilitadas para assinaturas de atualização enfileirada. Para obter mais informações sobre como publicar um artigo em mais de uma publicação, consulte a seção "Publishing Tables in More Than One Publication” (Publicando tabelas em mais de uma publicação) em [Publish Data and Database Objects](../../relational-databases/replication/publish/publish-data-and-database-objects.md) (Publicar dados e objetos de banco de dados).  
  
## <a name="oracle-publishers"></a>Publicadores Oracle  
 Há considerações adicionais para Publicadores Oracle:  
  
-   Para uma lista de objetos que podem ser publicados no Oracle, consulte [Design Considerations and Limitations for Oracle Publishers](../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md). Não são exibidos objetos que não podem ser publicados.  
  
-   Para uma lista de tipos de dados que podem ser publicados, consulte [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md). Colunas com tipos de dados que não podem ser publicados não são exibidas.  
  
## <a name="column-filters"></a>Filtros de coluna  
 Filtre colunas nessa página expandindo a tabela no painel **Objetos para publicação** e selecionando somente as colunas requeridas (linhas podem ser filtradas na página **Filtrar Linhas da Tabela** desse assistente). A filtragem de colunas é útil por várias razões, incluindo segurança (impedindo que dados sensíveis sejam replicados) e desempenho (evitando replicação de colunas BLOB (objeto binário grande), por exemplo). Para obter mais informações sobre filtragem de coluna, incluindo uma lista dos tipos de coluna que não podem ser filtrados, consulte [Filter Published Data](../../relational-databases/replication/publish/filter-published-data.md) (Filtrar dados publicados).  
  
## <a name="options"></a>Opções  
 O painel **Objetos para publicação** permite:  
  
-   Exibir todos os objetos disponíveis para replicação.  
  
-   Incluir um objeto em uma publicação marcando a caixa de seleção próxima àquele objeto.  
  
-   Incluir todos os objetos de um tipo específico (como uma tabela) na publicação, marcando a caixa de seleção próxima do tipo de objeto (como **Tabelas**).  
  
-   Expandir nós de tabela para ver as colunas na tabela.  
  
-   Filtrar colunas de tabela de uma publicação desmarcando a caixa de seleção próxima à coluna.  
  
-   Clique com o botão direito do mouse em um objeto no painel para consultar um menu de comandos para aquele objeto.  
  
 **Propriedades do Artigo**  
 Clique em **Propriedades do Artigo**e depois clique em uma das opções seguintes:  
  
-   Clique em **Definir as Propriedades do Artigo \<ObjectType> Realçado** para iniciar a caixa de diálogo **Propriedades do Artigo – \<ObjectName>** . As alterações de propriedade feitas nessa caixa de diálogo são aplicadas somente ao objeto que está realçado no painel de objetos na página **Artigos**.  
  
-   Clique em **Definir as Propriedades de Todos os Artigos \<ObjectType>** , para iniciar a caixa de diálogo **Propriedades de Todos os Artigos \<ObjectType>** ; as alterações à propriedade feitas nessa caixa de diálogo são aplicadas a todos os objetos desse tipo no painel de objetos da página **Artigos**, incluindo os ainda não selecionados para publicação.  
  
    > [!NOTE]  
    >  Alterações de propriedade feitas na caixa de diálogo **Propriedades para Todos os Artigos \<ObjectType>** substituem todas as alterações feitas anteriormente na caixa de diálogo **Propriedades do Artigo – \<ObjectName>** . Se, por exemplo, você quiser definir um número de padrões para todos os artigos de um tipo de objeto, mas também quer definir algumas propriedades para objetos individuais, defina primeiro os padrões para todos os artigos. Em seguida, defina as propriedades para os objetos individuais.  
  
 **A tabela realçada é somente para download**  
 Somente replicação de mesclagem. Somente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. Selecione para especificar que as alterações serão desabilitadas no Assinante se uma assinatura de cliente for usada. Como artigos somente para download não podem ser atualizados no Assinante, metadados de controle não são enviados aos Assinantes. Isso pode resultar em armazenamento reduzido nos Assinantes e em um benefício no desempenho, principalmente se a conexão de rede for lenta. Essa opção corresponde ao valor **Download somente para Assinante, proibir alterações do Assinante** para a opção **Direção de sincronização** na caixa de diálogo **Propriedades do Artigo** . Para obter mais informações, consulte [Otimizar o desempenho da replicação de mesclagem com artigos somente para download](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
 **Mostrar somente os artigos marcados na lista**  
 Marque essa caixa de seleção para mostrar somente os artigos selecionados no painel de objeto.  
  
## <a name="see-also"></a>Consulte Também  
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Exibir e modificar as propriedades da publicação](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
  
