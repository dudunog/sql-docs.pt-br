---
title: Propriedades da publicação, artigos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.pubproperties.articles.f1
ms.assetid: bdeea318-a153-44b8-9e51-9155f3bad18b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 55f938c8defeb418cda76b4efa0b182798a2e4e1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064608"
---
# <a name="publication-properties-articles"></a>Propriedades de Publicação, Artigos
  A caixa **Artigos** da caixa de diálogo **Propriedades de Publicação** contém informações sobre os artigos de uma publicação; permite adicionar e descartar artigos de publicações existentes; e permite alterar propriedades do artigo e filtragem de colunas.  
  
> [!NOTE]  
>  Depois que uma publicação é criada, algumas alterações de propriedade requerem um novo instantâneo. Se uma publicação tiver assinaturas, algumas alterações também exigirão que todas as assinaturas sejam reiniciadas. Para obter mais informações, consulte [Alterar propriedades da publicação e do artigo](publish/change-publication-and-article-properties.md) e [Add Articles to and Drop Articles from Existing Publications](publish/add-articles-to-and-drop-articles-from-existing-publications.md) (Adicionar e remover artigos para/de publicações existentes).  
  
 Se você estiver publicando um objeto de banco de dados que depende de outros objetos de banco de dados, terá de publicar todos os objetos referenciados. Por exemplo, se você publicar uma exibição que depende de uma tabela, terá de publicar a tabela também.  
  
 Objetos que não podem ser publicados têm um ícone vermelho próximo a eles, com uma explicação no painel de informações na parte inferior da página do assistente. Os objetos seguintes não podem ser publicados:  
  
-   Objetos criptografados.  
  
-   Exibições indexadas contendo colunas que permitem NULL.  
  
-   Tabelas sem chaves primárias não podem ser publicadas em publicações transacionais.  
  
-   Tabelas não podem ser publicadas em uma publicação de mesclagem e em uma publicação transacional habilitadas para assinaturas de atualização enfileirada. Para obter mais informações sobre como publicar um artigo em mais de uma publicação, consulte a seção "Publishing Tables in More Than One Publication” (Publicando tabelas em mais de uma publicação) em [Publish Data and Database Objects](publish/publish-data-and-database-objects.md) (Publicar dados e objetos de banco de dados).  
  
## <a name="oracle-publishers"></a>Publicadores Oracle  
 Há considerações adicionais para Publicadores Oracle:  
  
-   Para uma lista de objetos que podem ser publicados no Oracle, consulte [Design Considerations and Limitations for Oracle Publishers](non-sql/design-considerations-and-limitations-for-oracle-publishers.md). Não são exibidos objetos que não podem ser publicados.  
  
-   Para uma lista de tipos de dados que podem ser publicados, consulte [Data Type Mapping for Oracle Publishers](non-sql/data-type-mapping-for-oracle-publishers.md). Colunas com tipos de dados que não podem ser publicados não são exibidas.  
  
## <a name="column-filters"></a>Filtros de coluna  
 Filtre colunas nessa página expandindo a tabela no painel **Objetos para publicação** e selecionando somente as colunas requeridas (linhas podem ser filtradas na página **Filtrar Linhas da Tabela** desse assistente). A filtragem de colunas é útil por várias razões, incluindo segurança (impedindo que dados sensíveis sejam replicados) e desempenho (evitando replicação de colunas BLOB (objeto binário grande), por exemplo). Para obter mais informações sobre filtragem de coluna, incluindo uma lista dos tipos de coluna que não podem ser filtrados, consulte [Filter Published Data](publish/filter-published-data.md) (Filtrar dados publicados).  
  
## <a name="options"></a>Opções  
 O painel **Objetos para publicação** permite:  
  
-   Exibir todos os objetos disponíveis para replicação.  
  
-   Incluir um objeto em uma publicação marcando a caixa de seleção próxima àquele objeto.  
  
-   Descartar um artigo de uma publicação desmarcando a caixa de seleção próximo àquele objeto. Para obter informações sobre quando os artigos podem ser descartados, consulte [Add Articles to and Drop Articles from Existing Publications](publish/add-articles-to-and-drop-articles-from-existing-publications.md) (Adicionar e remover artigos para/de publicações existentes).  
  
-   Incluir todos os objetos de um tipo específico (como uma tabela) na publicação, marcando a caixa de seleção próxima do tipo de objeto (como **Tabelas**).  
  
-   Expandir nós de tabela para ver as colunas na tabela.  
  
-   Filtrar colunas de tabela de uma publicação, limpando a caixa de seleção próxima à coluna, ou incluir colunas não publicadas marcando a caixa de seleção.  
  
-   Clique com o botão direito do mouse em um objeto no painel para consultar um menu de comandos para aquele objeto.  
  
 **Propriedades do Artigo**  
 Clique em **Propriedades do Artigo** e depois clique em uma das opções seguintes:  
  
-   Clique em **definir propriedades do \<ObjectType> artigo realçado** para iniciar as **Propriedades do artigo – \<ObjectName> ** caixa de diálogo; as alterações de propriedade feitas nessa caixa de diálogo são aplicadas somente ao objeto que está realçado no painel objeto na página **artigos** .  
  
-   Clique em **definir propriedades de todos os \<ObjectType> artigos**para iniciar a caixa de diálogo **Propriedades de todos os \<ObjectType> artigos** . as alterações de propriedade feitas nessa caixa de diálogo são aplicadas a todos os objetos desse tipo no painel de objetos da página **artigos** , incluindo aqueles ainda não selecionados para publicação.  
  
    > [!NOTE]  
    >  As alterações de propriedade feitas na caixa de diálogo **Propriedades de todos os \<ObjectType> artigos** substituem as feitas anteriormente na caixa de diálogo **Propriedades do artigo – \<ObjectName> ** . Se, por exemplo, você quiser definir um número de padrões para todos os artigos de um tipo de objeto, mas também quer definir algumas propriedades para objetos individuais, defina primeiro os padrões para todos os artigos. Em seguida, defina as propriedades para os objetos individuais.  
  
 **A tabela realçada é somente para download**  
 Somente replicação de mesclagem. Somente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. Selecione para especificar que as alterações serão desabilitadas no Assinante se uma assinatura de cliente for usada. Como artigos somente para download não podem ser atualizados no Assinante, metadados de controle não são enviados aos Assinantes. Isso pode resultar em armazenamento reduzido nos Assinantes e em um benefício no desempenho, principalmente se a conexão de rede for lenta. Essa opção corresponde ao valor **Download somente para Assinante, proibir alterações do Assinante** para a opção **Direção de sincronização** na caixa de diálogo **Propriedades do Artigo** . Para obter mais informações, consulte [Otimizar o desempenho da replicação de mesclagem com artigos somente para download](merge/optimize-merge-replication-performance-with-download-only-articles.md).  
  
 **Mostrar somente os artigos marcados na lista**  
 Marque essa caixa de seleção para mostrar somente os artigos selecionados no painel de objeto.  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Publication](publish/create-a-publication.md)   
 [Exibir e modificar as propriedades da publicação](publish/view-and-modify-publication-properties.md)   
 [Criar e aplicar o instantâneo inicial](create-and-apply-the-initial-snapshot.md)   
 [Reinicializar uma assinatura](reinitialize-a-subscription.md)   
 [Publicar dados e objetos de banco de dados](publish/publish-data-and-database-objects.md)  
  
  
