---
description: Otimizar filtros de linha com parâmetros
title: Otimizar filtros de linha com parâmetros | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- precomputed partitions [SQL Server replication]
- filters [SQL Server replication], parameterized
- merge replication precomputed partitions [SQL Server replication], SQL Server Management Studio
- parameterized filters [SQL Server replication], optimizing
ms.assetid: 49349605-ebd0-4757-95be-c0447f30ba13
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9a8915894340e031629992f11a4556bbbafd6077
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465026"
---
# <a name="optimize-parameterized-row-filters"></a>Otimizar filtros de linha com parâmetros
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como otimizar filtros de linha com parâmetros no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Recomendações](#Recommendations)  
  
-   **Para otimizar filtros de linha com parâmetros, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Quando você usar filtros com parâmetros, será possível controlar como os filtros serão processados pela replicação de mesclagem, especificando a opção **use partition groups** ou a opção **keep partition changes** ao criar uma publicação. Essas opções melhoram o desempenho de sincronização para publicações com artigos filtrados, armazenando metadados adicionais no banco de dados de publicação. Você pode controlar como os dados serão compartilhados entre Assinantes definindo as **opções de partição** ao criar um artigo. Para obter mais informações sobre esses requisitos, consulte [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
     Com os assinantes do [!INCLUDE[ssEW](../../../includes/ssew-md.md)]SQL Server Compact, keep_partition_changes deve ser definido como true para assegurar que as exclusões sejam propagadas corretamente. Quando definido como falso, o assinante pode ter mais linhas do que o esperado.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 As configurações seguintes podem ser usadas para aperfeiçoar filtros de linha com parâmetros:  
  
 **Partition Options**  
 Defina essa opção na página **Propriedades** da caixa de diálogo **Propriedades do Artigo – \<Article>** ou na caixa de diálogo **Adicionar Filtro**. Ambas as caixas de diálogo estão no Assistente para Nova Publicação e a caixa de diálogo **Propriedades da Publicação – \<Publication>** . A caixa de diálogo **Propriedades do Artigo – \<Article>** permite que você especifique valores adicionais para essa opção que não estão disponíveis na caixa de diálogo **Adicionar Filtro**.  
  
 **Pré-calcular partições**  
 Essa opção é definida, por padrão, para **True** se os artigos em sua publicação aderem a um conjuntos de requisitos. Para obter mais informações sobre esses requisitos, consulte [Otimizar o desempenho de filtro com parâmetros com partições pré-computadas](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md). Modifique essa opção na página **Opções de Assinatura** da caixa de diálogo **Propriedades de Publicação – \<Publication>** .  
  
 **Otimizar sincronização**  
 Essa opção deve ser definida como **True** somente se **Pré-calcular Partições** estiver definida como **False**. Defina essa opção na página **Opções de Assinatura** da caixa de diálogo **Propriedades da Publicação – \<Publication>** .  
  
 Para obter mais informações sobre como usar o Assistente para Nova Publicação e acessar a caixa de diálogo **Propriedades da Publicação – \<Publication>** , confira [Criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar as propriedades da publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-set-partition-options-in-the-add-filter-or-edit-filter-dialog-box"></a>Para definir as opções de partição na caixa de diálogo Adicionar Filtro ou Editar Filtro  
  
1.  Na página **Filtrar Linhas da Tabela** do Assistente para Nova Publicação ou na página **Filtrar Linhas** da caixa de diálogo **Propriedades da Publicação – \<Publication>** , clique em **Adicionar** e em **Adicionar Filtro**.  
  
2.  Criar um filtro com parâmetros. Para obter mais informações, consulte [Definir e modificar um filtro de linha com parâmetros para um artigo de mesclagem](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md).  
  
3.  Selecione a opção que corresponde ao modo em que os dados serão compartilhados entre Assinantes:  
  
    -   **Uma linha dessa tabela irá para múltiplas assinaturas**  
  
    -   **Uma linha dessa tabela irá para apenas uma assinatura**  
  
     Se você selecionar **Uma linha desta tabela irá para apenas uma assinatura**, a replicação de mesclagem pode otimizar o desempenho armazenando e processando uma quantia menor de metadados. No entanto, será necessário certificar-se de que os dados são particionados de forma que uma linha não seja replicada em mais de um Assinante. Para obter mais informações, consulte a seção "Configurando opções de partição" no tópico [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Se você estiver na caixa de diálogo **Propriedades da Publicação – \<Publication>** , clique em **OK** para salvar e fechar a caixa de diálogo.  
  
#### <a name="to-set-partition-options-in-the-article-properties---article-dialog-box"></a>Para definir as Opções de Partição na caixa de diálogo Propriedades do Artigo – \<Article>  
  
1.  Na página **Artigos** do Assistente para Nova Publicação ou na caixa de diálogo **Propriedades da Publicação – \<Publication>** , selecione uma tabela e clique em **Propriedades do Artigo**.  
  
2.  Clique em **Definir Propriedades do Artigo Realçado na Tabela** ou **Definir as Propriedades de Todos os Artigos de Tabela**.  
  
3.  Na seção **Objeto de Destino** da guia **Propriedades** da caixa de diálogo **Propriedades do Artigo – \<Article>** , especifique um dos seguintes valores para **Opções de Partição**:  
  
    -   **Com sobreposição**  
  
    -   **Com sobreposição, não permitir alterações de dados fora da partição**  
  
    -   **Sem-sobreposição, única assinatura**  
  
    -   **Sem-sobreposição, compartilhados entre assinaturas**  
  
     Para obter mais informações sobre essas opções e sobre como estão relacionadas às opções disponíveis nas caixas de diálogo **Adicionar Filtro** e **Editar Filtro** , consulte a seção "Definindo as opções de partição'" em [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md).  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Se você estiver na caixa de diálogo **Propriedades da Publicação – \<Publication>** , clique em **OK** para salvar e fechar a caixa de diálogo.  
  
#### <a name="to-set-precompute-partitions"></a>Para definir o Pré-calcular Partições  
  
1.  Na página **Opções de Assinatura** da caixa de diálogo **Propriedades da Publicação – \<Publication>** , selecione um valor para a opção **Pré-calcular Partições**. A propriedade é somente leitura se:  
  
    -   A publicação não satisfizer os requisitos para as partições pré-calculadas.  
  
    -   Um instantâneo ainda não tiver sido gerado para a publicação. Nesse caso, a opção exibe um valor de **Definir automaticamente quando um instantâneo é criado.**  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-set-optimize-synchronization"></a>Para definir o Otimizar Sincronização  
  
1.  Na página **Opções de Assinatura** da caixa de diálogo **Propriedades da Publicação – \<Publication>** , selecione o valor `True` para a opção **Otimizar Sincronização**.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Para definições sobre as opções de filtragem de `@keep_partition_changes` e `@use_partition_groups`, consulte [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md).  
  
#### <a name="to-specify-merge-filter-optimizations-when-creating-a-new-publication"></a>Para especificar otimizações de filtro de mesclagem ao criar uma nova publicação  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Especifique `@publication` e um valor de `true` para um dos seguintes parâmetros:  
  
    -   `@use_partition_groups`: – a otimização de desempenho mais alta, contanto que os artigos estejam em conformidade com os requisitos para partições pré-calculadas. Para obter mais informações, consulte [Optimize Parameterized Filter Performance with Precomputed Partitions](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md) (Otimizar o desempenho do filtro parametrizado com partições pré-computadas).  
  
    -   `@keep_partition_changes` – use essa otimização se as partições pré-calculadas não puderem ser usadas.  
  
2.  Adicione um trabalho de instantâneo para a publicação. Para obter mais informações, consulte [Criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md).  
  
3.  No Publicador do banco de dados de publicação, execute [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md), especificando os seguintes parâmetros:  
  
    -   `@publication` – o nome da publicação da etapa 1.  
  
    -   `@article` – um nome para o artigo  
  
    -   `@source_object` – o objeto de banco de dados sendo publicado.  
  
    -   `@subset_filterclause` – a cláusula de filtro com parâmetros opcional usada para filtrar o artigo horizontalmente.  
  
    -   `@partition_options` – as opções de partição para o artigo filtrado.  
  
4.  Repita a etapa 3 para cada artigo na publicação.  
  
5.  (Opcional) No Assinante do banco de dados de publicação, execute [sp_addmergefilter](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) para definir um filtro de junção entre dois artigos. Para obter mais informações, consulte [Definir e modificar um filtro de junção entre artigos de mesclagem](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
#### <a name="to-view-and-modify-merge-filter-behaviors-for-an-existing-publication"></a>Para visualizar e modificar comportamentos de filtro de mesclagem para uma publicação existente  
  
1.  (Opcional) No Assinante do banco de dados de publicação, execute [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), especificando `@publication`. Observe o valor de `keep_partition_changes` e `use_partition_groups` no conjunto de resultados.  
  
2.  (Opcional) No Publicador do banco de dados de publicação, execute [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md). Especifique um valor de `use_partition_groups` para `@property` e `true` ou `false` para `@value`.  
  
3.  (Opcional) No Publicador do banco de dados de publicação, execute [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md). Especifique um valor de `keep_partition_changes` para `@property` e `true` ou `false` para `@value`.  
  
    > [!NOTE]  
    >  Ao habilitar `keep_partition_changes`, primeiro você deve desabilitar `use_partition_groups` e especificar um valor de `1` para `@force_reinit_subscription`.  
  
4.  (Opcional) No Publicador do banco de dados de publicação, execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique um valor igual a `partition_options` para `@property` e o valor apropriado para `@value`. Consulte [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) para definições destas opções de filtragem.  
  
5.  (Opcional) Iniciar o Snapshot Agent para regenerar o instantâneo se necessário. Para obter informações sobre quais alterações exigem a criação de um novo instantâneo, consulte [Alterar as propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Gerar automaticamente um conjunto de filtros de junção entre artigos de mesclagem &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/automatically-generate-join-filters-between-merge-articles.md)   
 [Definir e modificar um filtro de linha parametrizado para um artigo de mesclagem](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [Parameterized Row Filters](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
