---
title: Especificar propriedades de replicação de mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 11/29/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication [SQL Server replication], about merge replication
- merge replication [SQL Server replication]
ms.assetid: ff87c368-4c00-4e48-809d-ea752839551e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6513d018ee4dde665e18b986c4a8839cb7a995ec
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85005532"
---
# <a name="specify-merge-replication-properties"></a>Especificar propriedades de replicação de mesclagem
Este tópico explica como especificar várias propriedades para sua replicação de mesclagem. 


## <a name="download-only"></a>Somente download
  Esta seção descreve como especificar que um artigo de tabela de mesclagem é somente para download no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)] . Artigos de somente download são projetados para aplicativos com dados que não são atualizados nos Assinantes. Para obter mais informações, consulte [Otimizar o desempenho da replicação de mesclagem com artigos somente para download](../merge/optimize-merge-replication-performance-with-download-only-articles.md).  
 
  
###  <a name="limitations-and-restrictions"></a>Limitações e Restrições  
  
-   Se você especificar que um artigo é somente download, após a inicialização das assinaturas, todas as assinaturas de clientes que receberem o artigo deverão ser reincializadas. As assinaturas de servidor não têm que ser reinicializadas. Para obter mais informações sobre os efeitos das alterações de propriedades, consulte [Alterar propriedades da publicação e do artigo](change-publication-and-article-properties.md).  
  
### <a name="using-sql-server-management-studio"></a>Como usar o SQL Server Management Studio.  
 Especifique que um artigo é somente para download na página **artigos** do assistente para nova publicação ou na guia **Propriedades** da caixa de diálogo **Propriedades \<Article> do artigo** . Essa caixa de diálogo está disponível no Assistente para nova publicação e na caixa de diálogo **Propriedades da publicação – \<Publication> ** . Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma publicação](../publish/create-a-publication.md) e [Exibir e modificar as propriedades da publicação](../publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-articles-page"></a>Para especificar que um artigo seja somente download na página Artigos  
  
-   Na página **Artigos** do Assistente para Nova Publicação, selecione uma tabela, depois marque a caixa de seleção **A tabela realçada é somente para download**. 
  
#### <a name="to-specify-that-an-article-is-download-only-on-the-properties-tab-of-the-article-properties---article-dialog-box"></a>Para especificar que um artigo é somente para download na guia Propriedades da caixa de diálogo Propriedades do artigo – \<Article>  
  
1.  Na página **artigos** do assistente para nova publicação ou na caixa de diálogo ** \<Publication> Propriedades da publicação** , selecione uma tabela e clique em **Propriedades do artigo**.    
2.  Clique em **Definir Propriedades do Artigo Realçado na Tabela** ou **Definir as Propriedades de Todos os Artigos de Tabela**.    
3.  Na seção **objeto de destino** da guia **Propriedades** da caixa de diálogo **Propriedades do \<Article> artigo –** , especifique um dos seguintes valores para **direção de sincronização**:    
    -   **Download para Assinante, proibir alterações do Assinante**    
    -   **Download para Assinante, permitir alterações do Assinante**  
  
4.  Se você estiver na caixa de diálogo **Propriedades \<Publication> da publicação –** , clique em **OK** para salvar e fechar a caixa de diálogo.    

###  <a name="using-transact-sql"></a>Usando o Transact-SQL  
  
#### <a name="to-specify-that-a-new-merge-table-article-is-download-only"></a>Para especificar que um novo artigo de tabela de mesclagem é somente download    
1.  Execute [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql), especificando um valor de **1** ou **2** para o parâmetro ** \@ subscriber_upload_options**. Os números correspondem ao seguinte comportamento:  
  
    -   **0** - Nenhuma restrição (padrão). As alterações feitas no Assinante são carregadas no Publicador.    
    -   **1** - As alterações são permitidas no Assinante, mas não são carregadas no Publicador.    
    -   **2** - As alterações não são permitidas no Assinante.  
  
        > [!NOTE]  
        >  Se a tabela de origem de um artigo já estiver publicada em outra publicação, o valor de ** \@ subscriber_upload_options** deverá ser o mesmo para ambos os artigos.  
  
#### <a name="to-modify-an-existing-merge-table-article-to-be-download-only"></a>Para modificar um artigo de tabela de mesclagem existente para que seja de somente download  
  
1.  Para determinar se um artigo é de somente download, execute [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql). Observe o valor de **upload_options** para o artigo no conjunto de resultados.    
2.  Se o valor retornado na etapa 1 for **0**, execute [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql), especificando um valor de **subscriber_upload_options** para ** \@ Propriedade**, um valor de **1** para ** \@ force_invalidate_snapshot** e ** \@ force_reinit_subscription**e um valor de **1** ou **2** para ** \@ valor**, que corresponde ao seguinte comportamento:  
  
    -   **1** - As alterações são permitidas no Assinante, mas não são carregadas no Publicador.    
    -   **2** - As alterações não são permitidas no Assinante.  
  
        > [!NOTE]  
        >  Se a tabela de origem para um artigo já estiver publicada em outra publicação, o comportamento de somente download deve ser o mesmo para os dois artigos.  
 
## <a name=""></a><a name="interactive-conflict-resolution">Resolução interativa de conflitos</a>
[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]a replicação fornece um resolvedor interativo, que permite resolver conflitos manualmente durante a sincronização sob demanda no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Gerenciador de sincronização do Windows. Depois que a resolução interativa estiver habilitada, resolva os conflitos interativamente durante a sincronização, usando o Resolvedor Interativo. O Resolvedor Interativo está disponível pelo Gerenciador de Sincronização do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. Para obter mais informações, consulte [Como sincronizar uma assinatura usando o Gerenciador de Sincronização do Windows &#40;Gerenciador de Sincronização do Windows&#41;](../synchronize-a-subscription-using-windows-synchronization-manager.md).  
  
    
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Se uma sincronização for executada fora do Gerenciador de Sincronização do Windows (como sincronização agendada ou uma sincronização sob demanda no SQL Server Management Studio ou no Replication Monitor), os conflitos serão resolvidos automaticamente sem a intervenção de usuário, usando a resolução de conflitos padrão especificada para o artigo. Para obter mais informações, consulte [Resolução de conflito interativo](../merge/advanced-merge-replication-conflict-interactive-resolution.md).  
  
###  <a name="using-sql-server-management-studio"></a>Como usar o SQL Server Management Studio.  
  
#### <a name="enable-interactive-conflict-resolution-for-an-article"></a>Habilitar a resolução de conflitos interativa para um artigo  
  
1.  Na página **artigos** do assistente para nova publicação ou na caixa de diálogo **Propriedades \<Publication> da publicação –** , selecione uma tabela. Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma publicação](create-a-publication.md) e [Exibir e modificar as propriedades da publicação](view-and-modify-publication-properties.md).    
2.  Clique em **Propriedades de Artigos**e então clique em **Definir Propriedades do Artigo Realçado da Tabela** ou **Definir Propriedades de Todos os Artigos da Tabela**.    
3.  Na página **Propriedades do artigo \<Article> –** ou **Propriedades do \<ArticleType> artigo** , clique na guia **resolvedor** .    
4.  Selecione **Permitir que o Assinante resolva conflitos interativamente durante a sincronização sob demanda**    
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]    
6.  Se você estiver na caixa de diálogo **Propriedades \<Publication> da publicação –** , clique em **OK** para salvar e fechar a caixa de diálogo.  
  
#### <a name="to-specify-that-a-subscription-should-use-interactive-conflict-resolution"></a>Para especificar que uma assinatura deve usar a resolução interativa de conflito  
  
1.  Na caixa de diálogo **Propriedades da assinatura- \<Subscriber> \<SubscriptionDatabase> :** , especifique um valor **true** para a opção **resolver conflitos interativamente** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Push Subscription Properties](../view-and-modify-push-subscription-properties.md) e [View and Modify Pull Subscription Properties](../view-and-modify-pull-subscription-properties.md). 
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="using-transact-sql"></a>Usando o Transact-SQL  
 É possível especificar de forma programada se um Assinante usará essa interface gráfica para resolver conflitos de artigos quando uma assinatura pull para uma publicação de mesclagem é criada. Só conflitos em artigos que têm suporte para esta opção serão exibidos no Resolvedor Interativo.  
  
#### <a name="create-a-merge-pull-subscription-that-uses-the-interactive-resolver"></a>Criar uma assinatura pull de mesclagem que usa o Resolvedor Interativo  
  
1.  No Publicador do banco de dados de publicação, execute [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql), especificando a ** \@ publicação**. Anote o valor de **allow_interactive_resolver** para cada artigo no conjunto de resultados para o qual o Resolvedor Interativo será usado.    
    -   Se este valor for **1**, o Resolver Interativo será usado.    
    -   Se este valor for **0**, você deverá primeiro habilitar o Resolvedor Interativo de cada artigo. Para fazer isso, execute [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql), especificando a ** \@ publicação**, o ** \@ artigo**, um valor de **allow_interactive_resolver** para ** \@ Propriedade**e um valor de **verdadeiro** para ** \@ valor**.    
2.  No Assinante, no banco de dados de assinatura, execute o [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql). Para obter mais informações, consulte [Create a Pull Subscription](../create-a-pull-subscription.md).    
3.  No Publicador do banco de dados de assinatura, execute o [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql), especificando os seguintes parâmetros:  
  
    -   ** \@ Editor**, ** \@ publisher_db** (o banco de dados publicado) e ** \@ publicação**.    
    -   Um valor de **true** para ** \@ enabled_for_syncmgr**.    
    -   Um valor de **true** para ** \@ use_interactive_resolver**.    
    -   As informações da conta de segurança requerida pelo Merge Agent. Para obter mais informações, consulte [Create a Pull Subscription](../create-a-pull-subscription.md).    
4.  No Publicador, no banco de dados da publicação, execute [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql).  
  
#### <a name="define-an-article-that-supports-the-interactive-resolver"></a>Definir um artigo que tem suporte para o Resolvedor Interativo  
  
No Publicador do banco de dados de publicação, execute o [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Especifique o nome da publicação à qual o artigo pertence para ** \@ publicação**, um nome para o artigo para o ** \@ artigo**, o objeto de banco de dados que está sendo publicado para ** \@ source_object**e um valor de **true** para ** \@ allow_interactive_resolver**. Para obter mais informações, consulte [Define an Article](define-an-article.md).  

## <a name="specify-the-conflict-tracking-and-resolution-level"></a>Especificar o nível de rastreamento e resolução de conflitos 
Quando uma assinatura em uma publicação de mesclagem é sincronizada, a replicação verifica os conflitos causados pelas alterações nos mesmos dados feitos no Publicador e no Assinante. Especifique se os conflitos serão detectados no nível da linha, onde todas as alterações de linha são consideradas conflito, ou no nível da coluna, onde apenas as alterações da mesma linha e da coluna são consideradas conflito. A resolução de conflitos para artigos é realizada no nível da linha. Para obter mais informações sobre a detecção e a resolução de conflitos quando registros lógicos são usados, consulte [Detecting and Resolving Conflicts in Logical Records](../merge/advanced-merge-replication-conflict-resolving-in-logical-record.md).  
  

  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Se você alterar o nível de controle depois de inicializadas as assinaturas, essas assinaturas deverão ser reinicializadas. Para obter mais informações sobre os efeitos das alterações de propriedades, consulte [Alterar propriedades da publicação e do artigo](../publish/change-publication-and-article-properties.md).    
-   Com controle em nível de linha e de coluna, a resolução de conflito é sempre feita em nível de linha: a linha vencedora substitui a perdedora. A replicação de mesclagem também permite especificar que os conflitos sejam rastreados e resolvidos em nível de registro lógico, mas essas opções não estão disponíveis no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]. Para obter informações sobre como definir essas opções de procedimentos armazenados de [replicação, consulte definir uma relação de registro lógico](../publish/define-a-logical-record-relationship-between-merge-table-articles.md)entre artigos de tabela de mesclagem.  
  
###  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Especifique o controle no nível de linha ou coluna para artigos de mesclagem na guia **Propriedades** da caixa de diálogo **Propriedades do artigo** , que está disponível no Assistente para nova publicação e na caixa de diálogo **Propriedades \<Publication> da publicação** . Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma publicação](create-a-publication.md) e [Exibir e modificar as propriedades da publicação](../publish/view-and-modify-publication-properties.md).  
  
#### <a name="specify-row--or-column-level-tracking"></a>Especificar acompanhamento em nível de linha ou de coluna  
  
1.  Na página **artigos** do assistente para nova publicação ou na caixa de diálogo **Propriedades \<Publication> da publicação –** , selecione uma tabela.    
2.  Clique em **Propriedades de Artigos**e então clique em **Definir Propriedades do Artigo Realçado da Tabela** ou **Definir Propriedades de Todos os Artigos da Tabela**.   
3.  Na guia **Propriedades** da caixa de diálogo **Propriedades \<Article> do artigo** , selecione um dos seguintes valores para a propriedade **nível de rastreamento** : **rastreamento de nível de linha** ou **controle no nível de coluna**.    
4.  Se você estiver na caixa de diálogo **Propriedades \<Publication> da publicação –** , clique em **OK** para salvar e fechar a caixa de diálogo.  
  
###  <a name="using-transact-sql"></a>Usando o Transact-SQL  
  
#### <a name="specify-conflict-tracking-options-for-a-new-merge-article"></a>Especificar opções de acompanhamento de conflitos para um novo artigo de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) e especifique um dos seguintes valores para ** \@ column_tracking**:  
  
    -   **true** - Use controle no nível da coluna para o artigo.    
    -   **false** - Use controle no nível da linha, que é o padrão.  
  
#### <a name="change-conflict-tracking-options-for-a-merge-article"></a>Alterar as opções de acompanhamento de conflito para um novo artigo de mesclagem  
  
1.  Para determinar as opções de rastreamento de conflito para um artigo de mesclagem, execute [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql). Observe o valor da opção **column_tracking** no conjunto de resultados do artigo. Um valor de **1** significa que o controle no nível da coluna está em uso, e o valor de **0** significa que o controle no nível da linha está em uso.    
2.  No Publicador do banco de dados de publicação, execute [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Especifique um valor de **column_tracking** para ** \@ Propriedade** e um dos seguintes valores para ** \@ valor**:
    -   **true** - Use controle no nível da coluna para o artigo.
    -   **false** - Use controle no nível da linha, que é o padrão.  
  
     Especifique um valor de **1** para ** \@ force_invalidate_snapshot** e ** \@ force_reinit_subscription**.  

## <a name="tracking-deletes"></a>Acompanhamento de exclusões

> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  
 Por padrão, a replicação de mesclagem sincroniza comandos DELETE entre o Publicador e o Assinante. A replicação de mesclagem permite que as linhas sejam retidas no banco de dados de assinatura mesmo após terem sido excluídas da publicação e vice-versa. Especifique de forma programática que os comandos DELETE sejam ignorados durante a criação de um novo artigo ou habilite essa funcionalidade posteriormente, usando procedimentos armazenados de replicação.  
  
> [!IMPORTANT]  
>  Habilitar essa funcionalidade resultará em não convergência, o que significa que os dados presentes no Assinante não refletirão dados no Publicador da forma correta. É preciso implementar um mecanismo próprio para remover manualmente as linhas excluídas.  
  
### <a name="specify-that-deletes-be-ignored-for-a-new-merge-article"></a>Especificar que as exclusões sejam ignoradas para um novo artigo de mesclagem  
  
1.  No Publicador no banco de dados de publicação, execute o [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Especifique um valor de `false` para ** \@ delete_tracking**. Para obter mais informações, consulte [Define an Article](../publish/define-an-article.md).  
  
    > [!NOTE]  
    >  Se a tabela de fonte de um artigo já estiver publicada em outra publicação, o valor de **delete_tracking** deverá ser o mesmo de ambos os artigos.  
  
### <a name="specify-that-deletes-be-ignored-for-an-existing-merge-article"></a>Especificar que as exclusões sejam ignoradas para um artigo de mesclagem existente  
  
1.  Para determinar se a compensação de erro está habilitada para um artigo, execute [sp_helpmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql) e observe o valor de **delete_tracking** no conjunto de resultados. Se este valor for **0**, as exclusões já estão sendo ignoradas.    
2.  Se o valor da etapa 1 for **1**, execute [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) no Publicador do banco de dados de publicação. Especifique um valor de **delete_tracking** para ** \@ Propriedade**e um valor de `false` para ** \@ valor**.  
  
    > [!NOTE]  
    >  Se a tabela de fonte de um artigo já estiver publicada em outra publicação, o valor de **delete_tracking** deverá ser o mesmo de ambos os artigos.  
  
## <a name="processing-order"></a>Ordem de processamento
  A replicação de mesclagem permite que você especifique a ordem em que artigos são processados pelo Agente de Mesclagem durante o processo de sincronização. Você pode atribuir uma ordem a cada artigo programaticamente ao criar um artigo usando procedimentos armazenados de replicação. Os artigos são processados em ordem crescente de valores. Se dois artigos tiverem o mesmo valor, serão processados simultaneamente. Para obter mais informações, confira [propriedades de Especificar Replicação de Mesclagem](../publish/specify-merge-replication-properties.md).  

  A partir do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] , é possível substituir a ordem padrão de processamento de artigos para publicações de mesclagem. Isso é útil, por exemplo, se você definir a integridade referencial por meio de gatilhos e esses gatilhos precisarem ser acionados em uma determinada ordem. 

### <a name="how-processing-order-is-determined"></a>Como a ordem de processamento é determinada  
 Durante a sincronização da mesclagem, os artigos são, por padrão, processados na ordem exigida pelas dependências entre objetos, incluindo as limitações de integridade referencial declarativa (DRI) definidas nas tabelas de base. O processamento envolve a enumeração das alterações em uma tabela e depois a aplicação dessas alterações. Se não houver DRI presente, mas existirem filtros de junção ou registros lógicos entre artigos de tabela, os artigos serão processados na ordem exigida pelos filtros e registros lógicos. Os artigos que não se relacionam a nenhum outro artigo por meio de DRI, filtros de junção, registros lógicos ou outras dependências serão processados segundo o apelido do artigo na tabela do sistema do [sysmergearticles &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/sysmergearticles-transact-sql).  
  
 Considere uma publicação que inclua as tabelas **SalesOrderHeader** e **SalesOrderDetail** com uma coluna de chave primária **SalesOrderID** na tabela **SalesOrderHeader** e uma coluna de chave estrangeira correspondente **SalesOrderID** na tabela **SalesOrderDetail** . Durante a sincronização, a replicação de mesclagem impede violações de chave estrangeira ao inserir qualquer linha nova em **SalesOrderHeader** antes de inserir linhas associadas em **SalesOrderDetail**. Do mesmo modo, linhas são excluídas de **SalesOrderDetail** antes de a linha associada ser excluída de **SalesOrderHeader**.  
  
 Porém, em alguns aplicativos a integridade referencial é imposta por meio de gatilhos de banco de dados, ou no nível do aplicativo, e não por meio de DRI. Considerando a publicação descrita acima, em vez de DRI, a tabela **SalesOrderDetail** poderia ter um gatilho de inserção que garanta que a linha associada na tabela **SalesOrderHeader** existe antes de permitir uma inserção. **SalesOrderHeader** poderia ter um gatilho de exclusão que garante que não há nenhuma linha associada em **SalesOrderDetail** antes de permitir uma exclusão. A replicação de mesclagem não leva em conta os gatilhos ao determinar a ordem de processamento de artigos porque não pode determinar qual será o resultado do gatilho até que ele tenha sido acionado. Do mesmo modo, a replicação não pode levar em conta as restrições definidas no nível do aplicativo.  
  
 Quando a integridade referencial é mantida por meio de gatilhos ou no nível do aplicativo, você deve especificar a ordem em que os artigos devem ser processados. No exemplo com gatilhos, você especificaria que a tabela **SalesOrderHeader** deve ser processada antes de **SalesOrderDetail**, porque a ordem dos artigos é baseada na ordem de inserção. A replicação de mesclagem inverterá a ordem automaticamente para as exclusões. A replicação de mesclagem não apresentará falha sem a ordenação de artigos, porque o Merge Agent continua a processar os artigos se houver uma violação de restrição; depois do processamento de todos os outros artigos, ele tenta novamente as operações que apresentaram falha. Especificar a ordem de artigos simplesmente evita as novas tentativas e o processamento adicional associado a elas. Se você especificar uma ordem incorreta (por exemplo, uma que faça com que os registros detalhados sejam processados antes dos registros do cabeçalho), a replicação de mesclagem irá tentar o processamento repetidamente, até obter êxito.  

### <a name="new-article"></a>Novo artigo
  
1.  No Publicador no banco de dados de publicação, execute o [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Especifique um valor inteiro que representa a ordem de processamento do artigo para ** \@ processing_order**. Para obter mais informações, consulte [Define an Article](define-an-article.md).  
  
    > [!NOTE]  
    >  Ao criar artigos ordenados, você deverá deixar intervalos entre os valores de ordem de artigo. Isto facilitará a definição de novos valores no futuro. Por exemplo, se você tiver três artigos para os quais precisa especificar uma ordem de processamento fixa, defina o valor de ** \@ processing_order** como 10, 20 e 30 em vez de 1, 2 e 3, respectivamente.  
  
### <a name="existing-article"></a>Artigo existente
  
1.  Para determinar a ordem de processamento de um artigo, execute [sp_helpmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql) e observe o valor de **processing_order** no conjunto de resultados.  
  
2.  No Publicador no banco de dados de publicação, execute [sp_changemergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql). Especifique um valor de **processing_order** para ** \@ Propriedade** e um valor inteiro que representa a ordem de processamento para o ** \@ valor**.  



## <a name="see-also"></a>Consulte Também  
 [Otimizar o desempenho da replicação de mesclagem com o controle de exclusão condicional](../merge/optimize-merge-replication-performance-with-conditional-delete-tracking.md)  
 [Detectando e resolvendo conflitos em registros lógicos](../merge/advanced-merge-replication-conflict-resolving-in-logical-record.md)   
 [Definir uma relação de registro lógico entre artigos de tabela de mesclagem](define-a-logical-record-relationship-between-merge-table-articles.md)   
 [Detectar e resolver conflitos de replicação de mesclagem](../merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Otimizar o desempenho da replicação de mesclagem com artigos somente para download](../merge/optimize-merge-replication-performance-with-download-only-articles.md)   
 [Definir um artigo](define-an-article.md)   
 [Exibir e modificar as propriedades do artigo](view-and-modify-article-properties.md)  