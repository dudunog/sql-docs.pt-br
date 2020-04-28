---
title: Gerenciar colunas de identidade | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- identity values [SQL Server replication]
- merge replication [SQL Server replication], identity range management
- publishing [SQL Server replication], identity columns
- transactional replication, identity range management
- identity columns [SQL Server], replication
ms.assetid: 98892836-cf63-494a-bd5d-6577d9810ddf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cbfad718850df4c66572999735fbee58fb530424
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73882299"
---
# <a name="manage-identity-columns"></a>Gerenciar colunas de identidade
  Este tópico descreve como gerenciar colunas de identidade no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Quando as inserções de Assinante são replicadas de volta ao Publicador, as colunas de identidade devem ser gerenciadas para evitar a atribuição do mesmo valor de identidade para o Assinante e o Publicador. A Replicação pode gerenciar intervalos de identidade automaticamente ou você pode escolher controlar o gerenciamento de intervalo de identidade manualmente.  Para obter informações sobre as opções de gerenciamento de intervalos de identidade fornecidas pela replicação, consulte [Replicar colunas de identidade](replicate-identity-columns.md).  
  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Ao publicar uma tabela em mais de uma publicação, você deve especificar as mesmas opções de gerenciamento do intervalo da identidade para ambas a publicações. Para obter mais informações, consulte “Publicando tabelas em mais de uma publicação” em [Publicar dados e objetos de banco de dados](publish-data-and-database-objects.md).  
  
-   Para criar um número incrementado automaticamente, que possa ser usado em várias tabelas ou ser chamado de aplicativos, sem referenciar tabelas, consulte [Números de Sequência](../../sequence-numbers/sequence-numbers.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Especifique uma opção de gerenciamento de colunas de identidade na guia **Propriedades** da caixa de diálogo **Propriedades do Artigo – \<Artigo>** do Assistente para Nova Publicação. Para obter mais informações sobre como usar esse assistente, consulte [Criar uma publicação](create-a-publication.md). No Assistente para Nova Publicação:  
  
-   Se você selecionar **Publicação de mesclagem** ou **Publicação transacional com assinaturas atualizáveis** na página **Tipo de Publicação** , selecione gerenciamento automático ou manual do intervalo de identidades (automático, o padrão, é o recomendado). Depois que a tabela é publicada, a propriedade não pode ser modificada, mas outras propriedades relacionadas a ela, sim.  
  
-   Se você selecionar outros tipos de publicação, o gerenciamento de intervalo de identidade deve ser definido como manual.  
  
 Modifique os intervalos e limites de identidade na guia **Propriedades** de **Propriedades do Artigo –\<Artigo>**, que está disponível na caixa de diálogo **Propriedades da Publicação – \<Publicação>**. Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-an-identity-column-management-option"></a>Para especificar uma opção de gerenciamento de coluna de identidade  
  
1.  Se o Publicador estiver executando uma versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anterior à [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], na página **Tipo de Publicação** do Assistente para Nova Publicação, selecione **Publicação de mesclagem** ou **Publicação transacional com assinaturas atualizáveis**.  
  
2.  Na página **Artigos** , selecione uma tabela com uma coluna de identidade.  
  
3.  Clique em **Propriedades do Artigo**e clique em **Definir Propriedades do Artigo Realçado da Tabela**.  
  
4.  Na guia **Propriedades** da caixa de diálogo **Propriedades do Artigo – \<Artigo>**, na seção **Gerenciamento de Intervalos de Identidade**, defina a propriedade **Gerenciar automaticamente os intervalos de identidades** como **Automático** ou **Manual** (para Publicadores que executam o [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] ou posterior) ou **Verdadeiro** ou **Falso** (para Publicadores que executam uma versão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anterior a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]).  
  
5.  Se você selecionou **Automático** ou **Verdadeiro** na etapa 4, digite valores para as opções na tabela a seguir. Para obter mais informações sobre como essas configurações são usadas, consulte a seção “Atribuindo intervalos de identidade” de [Replicar colunas de identidade](replicate-identity-columns.md).  
  
    |Opção|Valor|Descrição|  
    |------------|-----------|-----------------|  
    |**Tamanho do intervalo do Publicador**|Valor inteiro para o tamanho do intervalo (por exemplo, 20000).|Consulte a seção “Atribuindo intervalos de identidade” em [Replicar colunas de identidade](replicate-identity-columns.md).|  
    |**Tamanho do intervalo do assinante**|Valor inteiro para tamanho de intervalo (por exemplo, 10000).|Consulte a seção “Atribuindo intervalos de identidade” em [Replicar colunas de identidade](replicate-identity-columns.md).|  
    |**Porcentagem do limite de intervalo**|Valor inteiro para porcentagem do limite (por exemplo, 90 equivale a 90 por cento).|Porcentagem de valores de identidade totais usados em um nó antes que um novo intervalo de identidade seja atribuído.<br /><br /> Observação: esse valor deve ser especificado, mas é usado somente por: Assinantes usando assinaturas de atualização enfileiradas, e Assinantes para publicações de mesclagem executando [!INCLUDE[ssEW](../../../includes/ssew-md.md)] ou versões anteriores de outras edições do SQL Server. Para obter mais informações, consulte a seção “Atribuindo intervalos de identidade” de [Replicar colunas de identidade](replicate-identity-columns.md).|  
    |**Valor inicial do intervalo seguinte**|Valor inteiro. Somente leitura.|O valor no qual o próximo intervalo terá início. Por exemplo, se o intervalo atual for 5001-6000, esse valor será 6001.|  
    |**Valor de identidade máximo**|Valor inteiro. Somente leitura.|O valor maior para a coluna de identidade. Determinado pelo tipo de dados base da coluna.|  
    |**Progressiv**|Valor inteiro. Somente leitura.|A quantidade pela qual o número na coluna de identidade deve ser aumentado ou diminuído para cada inserção: normalmente definido como 1.|  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### <a name="to-modify-identity-ranges-and-thresholds-after-a-table-is-published"></a>Para modificar intervalos de identidade e limites depois que uma tabela é publicada  
  
1.  Na página **Artigos** da caixa de diálogo **Propriedades da Publicação – \<Publicação>**, selecione uma tabela com uma coluna de identidade.  
  
2.  Clique em **Propriedades do Artigo**e clique em **Definir Propriedades do Artigo Realçado da Tabela**.  
  
3.  Na guia **Propriedades** da caixa de diálogo **Propriedades do Artigo – \<Artigo>**, na seção **Gerenciamento de Intervalos de Identidade**, insira valores para uma ou mais das seguintes propriedades: **Tamanho do intervalo do Publicador**, **Tamanho do intervalo do Assinante** e **Percentual do limite de intervalo**.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
5.  Clique em **OK** na caixa de diálogo **Propriedades da Publicação – \<Publicação >**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 Você pode usar os procedimentos armazenados de replicação para especificar as opções de gerenciamento de intervalo da identidade, quando um artigo é criado.  
  
#### <a name="to-enable-automatic-identity-range-management-when-defining-articles-for-a-transactional-publication"></a>Para habilitar o gerenciamento automático de intervalo de identidade ao definir artigos para uma publicação transacional  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Se a tabela de origem que está sendo publicada tiver uma coluna de identidade, especifique um valor de **auto** para ** \@identityrangemanagementoption**, o intervalo de valores de identidade atribuídos ao Publicador para ** \@pub_identity_range**, o intervalo de valores de identidade atribuídos a cada Assinante para ** \@identity_range**e a porcentagem do total de valores de identidade usados antes que um novo intervalo de identidade seja atribuído para ** \@o limite**. Para obter mais informações sobre como definir artigos, consulte [Definir um artigo](define-an-article.md).  
  
    > [!NOTE]  
    >  Certifique-se de que os tipos de dados da coluna de identidade é grande o suficiente para oferece suporte a todos os intervalos de identidades atribuídas a todos os Assinantes.  
  
#### <a name="to-disable-automatic-identity-range-management-when-defining-articles-for-a-transactional-publication"></a>Para desabilitar o gerenciamento automático de intervalo de identidade ao definir artigos para uma publicação transacional  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addarticle](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql). Especifique um valor de **manual** para ** \@identityrangemanagementoption**. Para obter mais informações sobre como definir artigos, consulte [Definir um artigo](define-an-article.md).  
  
2.  Atribua intervalos às colunas de artigo de identidade no Assinante para evitar conflitos ao atualizar Assinantes. Para obter mais informações, consulte a seção sobre como atribuir intervalos para o gerenciamento manual de intervalos da identidade no tópico [Replicar colunas de identidade](replicate-identity-columns.md).  
  
#### <a name="to-enable-automatic-identity-range-management-when-defining-articles-for-a-merge-publication"></a>Para habilitar o gerenciamento automático de intervalo de identidade ao definir artigos para uma publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute o [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Se a tabela de origem que está sendo publicada tiver uma coluna de identidade, especifique um valor de **auto** para ** \@identityrangemanagementoption**, o intervalo de valores de identidade atribuídos a uma assinatura de servidor para ** \@pub_identity_range**, o intervalo de valores de identidade atribuídos ao Publicador e a cada assinatura de cliente para ** \@identity_range**e a porcentagem do total de valores de identidade usados antes que um novo intervalo de identidade seja atribuído para ** \@o limite**. Para obter mais informações sobre quando novos intervalos de identidade são atribuídos, consulte Atribuindo intervalos de identidade no tópico [Replicar colunas de identidade](replicate-identity-columns.md). Para obter mais informações sobre como definir artigos, consulte [Definir um artigo](define-an-article.md).  
  
    > [!NOTE]  
    >  Certifique-se de que o tipo de dado da coluna de identidade é grande o suficiente para oferece suporte ao intervalo total de identidades atribuídas a todos os Assinantes, especialmente para Assinantes com assinaturas de servidor.  
  
#### <a name="to-disable-automatic-identity-range-management-when-defining-articles-for-a-merge-publication"></a>Para desabilitar o gerenciamento automático de intervalo de identidade ao definir artigos para uma publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute o [sp_addmergearticle](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql). Especifique um dos seguintes valores para ** \@identityrangemanagementoption**:  
  
    -   **manual** - Os intervalos de identidade devem ser atribuídos manualmente para atualizar os Assinantes.  
  
    -   **none** - As colunas de identidade no Publicador não serão definidas como colunas de identidade no Assinante.  
  
     Para obter mais informações sobre como definir artigos, consulte [Definir um artigo](define-an-article.md).  
  
2.  Atribua intervalos às colunas de artigo de identidade no Assinante para evitar conflitos ao atualizar Assinantes.  
  
#### <a name="to-change-automatic-identity-range-management-settings-for-an-existing-article-in-a-snapshot-or-transactional-publication"></a>Para alterar as configurações de gerenciamento de intervalo da identidade para um artigo existente em um instantâneo ou publicação transacional  
  
1.  No Publicador do banco de dados de publicação, execute [sp_helparticle](/sql/relational-databases/system-stored-procedures/sp-helparticle-transact-sql) e observe o valor de **identityrangemanagementoption** no conjunto de resultados. Se esse valor for **0**, o gerenciamento de intervalo de identidade automático não estará habilitado.  
  
2.  Se o valor de **identityrangemanagementoption** no conjunto de resultados for **1**, altere as configurações como segue:  
  
    -   Para alterar os intervalos de identidade atribuídos, execute [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql) no Publicador do banco de dados de publicação. Especifique um valor de **identity_range** ou **pub_identity_range** para ** \@Propriedade** e o novo valor de intervalo para ** \@valor**.  
  
    -   Para alterar o limite no qual os novos intervalos serão atribuídos, execute [sp_changearticle](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql) no Publicador do banco de dados de publicação. Especifique um valor de **limite** para ** \@a propriedade** e o novo valor de limite para ** \@valor**.  
  
#### <a name="to-change-automatic-identity-range-management-settings-for-an-existing-article-in-a-merge-publication"></a>Para alterar automaticamente as configurações de gerenciamento de intervalo da identidade para um artigo existente em uma publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute [sp_helpmergearticle](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql) e observe o valor de **identity_support** no conjunto de resultado. Se esse valor for **0**, o gerenciamento de intervalo de identidade automático não estará habilitado.  
  
2.  Se o valor de **identity_support** no conjunto de resultado é **1**, altere as configurações como segue:  
  
    -   Para alterar os intervalos de identidade atribuídos, execute [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) no Publicador do banco de dados de publicação. Especifique um valor de **identity_range** ou **pub_identity_range** para ** \@Propriedade** e o novo valor de intervalo para ** \@valor**.  
  
    -   Para alterar o limite no qual novos intervalos serão atribuídos, , execute [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) no Publicador do banco de dados de publicação. Especifique um valor de **limite** para ** \@a propriedade** e o novo valor de limite para ** \@valor**. Para obter mais informações sobre quando novos intervalos de identidade são atribuídos, consulte Atribuindo intervalos de identidade no tópico [Replicar colunas de identidade](replicate-identity-columns.md).  
  
    -   Para desabilitar o gerenciamento automático de intervalo de identidade, execute [sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) no Publicador do banco de dados de publicação. Especifique um valor de **identityrangemanagementoption** para ** \@Property** e **manual** ou **None** para ** \@Value**.  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação transacional ponto a ponto](../transactional/peer-to-peer-transactional-replication.md)   
 [Conceitos de procedimentos armazenados do sistema de replicação](../concepts/replication-system-stored-procedures-concepts.md)   
 [Replicar colunas de identidade](replicate-identity-columns.md)  
  
  
