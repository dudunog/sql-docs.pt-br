---
title: Especificar opções de esquema para replicação do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- schemas [SQL Server replication], options
- articles [SQL Server replication], transactional replication options
- articles [SQL Server replication], merge replication options
- articles [SQL Server replication], schema options
ms.assetid: 1f85a479-bd6e-4023-abf7-7435a7e5b567
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 1ce8df82856f7a6a495fdd026dec0d46eaba4c89
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76287517"
---
# <a name="specify-schema-options-for-sql-server-replication"></a>Especificar opções de esquema para replicação do SQL Server
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Este tópico descreve como especificar opções de esquema no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Ao publicar uma tabela ou exibição, você pode controlar as opções de criação de objeto que são replicadas para o objeto publicado. Você pode definir esta opção quando o artigo é criado, e você também pode alterá-los mais tarde. Se você não especificar essas opções explicitamente para um artigo, um conjunto padrão de opções será definido.  
  
> [!NOTE]  
>  As opções de esquema padrão ao usar procedimentos armazenados de replicação podem diferir das opções padrão quando forem adicionados artigos usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
-   **Para especificar opções de esquema, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Para alterar opções de esquema após a criação da publicação, gere um novo instantâneo.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Para obter a lista completa de opções de esquema, consulte o parâmetro `@schema_option` de [sp_addarticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) e [sp_addmergearticle &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 Especifique opções de esquema, como copiar ou não restrições e gatilhos para Assinantes, na guia **Propriedades** da caixa de diálogo **Propriedades do Artigo – \<Artigo>** . Essa guia está disponível no Assistente para Nova Publicação e na caixa de diálogo **Propriedades da Publicação – \<Publicação>** . Para obter mais informações sobre como usar o assistente e acessar a caixa de diálogo, consulte [Criar uma publicação](../../../relational-databases/replication/publish/create-a-publication.md) e [Exibir e modificar as propriedades da publicação](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md).  
  
#### <a name="to-specify-schema-options"></a>Para especificar opções de esquema  
  
1.  Na página **Artigos** do Assistente para Nova Publicação ou na caixa de diálogo **Propriedades da Publicação – \<Publicação>** , selecione um artigo e clique em **Propriedades do Artigo**.  
  
2.  Selecione quais alterações de opção de esquema de artigos devem ser aplicar a:  
  
    -   Clique em **Definir as Propriedades do Artigo \<ObjectType> Realçado** para iniciar a caixa de diálogo **Propriedades do Artigo – \<ObjectName >** . As alterações de propriedade feitas nessa caixa de diálogo são aplicadas somente ao objeto que está realçado no painel de objetos na página **Artigos**.  
  
    -   Clique em **Definir as Propriedades de Todos os Artigos \<ObjectType>** , para abrir a caixa de diálogo **Propriedades de Todos os Artigos \<ObjectType>** ; as alterações na propriedade feitas nessa caixa de diálogo são aplicadas a todos os objetos desse tipo, no painel de objetos da página **Artigos**, incluindo aqueles ainda não selecionados para publicação.  
  
        > [!NOTE]  
        >  Alterações de propriedade feitas na caixa de diálogo **Propriedades para Todos os Artigos \<ObjectType>** substituem todas as alterações feitas anteriormente na caixa de diálogo **Propriedades do Artigo – \<ObjectName>** . Se, por exemplo, você quiser definir um número de padrões para todos os artigos de um tipo de objeto, mas também quer definir algumas propriedades para objetos individuais, defina primeiro os padrões para todos os artigos. Em seguida, defina as propriedades para os objetos individuais.  
  
3.  Nas seções **Copiar Objetos e Configurações no Assinante** e **Objeto de Destino** da guia **Propriedades** da caixa de diálogo **Propriedades do Artigo – \<Artigo>** , especifique valores para as opções.  
  
4.  Modifique propriedades, se necessário, depois clique em **OK**.  
  
5.  Se você estiver na caixa de diálogo **Propriedades da Publicação – \<Publicação>** , clique em **OK** para salvar e fechar a caixa de diálogo.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 As opções de esquema são especificadas como um valor hexadecimal que é o resultado [| (OR bit a bit)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) de uma ou mais opções. Para obter mais informações, consulte [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) e [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md).  
  
> [!NOTE]  
>  Você deve converter valores de opção de esquema de **binary** para **int** antes de executar uma operação bit a bit. Para obter mais informações, veja [CAST e CONVERT &#40;Transact-SQL&#41;](../../../t-sql/functions/cast-and-convert-transact-sql.md).  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-snapshot-or-transactional-publication"></a>Para especificar opções de esquema ao definir um artigo para uma publicação de instantâneo ou transacional  
  
1.  No Publicador do banco de dados de publicação, execute [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para `@publication`, um nome para o artigo para `@article`, o objeto de banco de dados a ser publicado para `@source_object`, o tipo de objeto de banco de dados para `@type` e o resultado [| (OR bit a bit)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) de uma ou mais opções de esquema para `@schema_option`. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### <a name="to-specify-schema-options-when-defining-an-article-for-a-merge-publication"></a>Para especificar opções de esquema ao definir um artigo para uma publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute o [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para `@publication`, um nome para o artigo para `@article`, o objeto de banco de dados a ser publicado para `@source_object` e o resultado [| (OR bit a bit)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) de uma ou mais opções de esquema para `@schema_option`. Para obter mais informações, consulte [Define an Article](../../../relational-databases/replication/publish/define-an-article.md).  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-snapshot-or-transactional-publication"></a>Para alterar opções de esquema para um artigo existente em uma publicação de instantâneo ou transacional  
  
1.  No Publicador do banco de dados de publicação, execute [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para `@publication` e o nome do artigo para `@article`. Observe o valor da coluna `schema_option` no conjunto de resultados.  
  
2.  Execute uma operação [& (AND bit a bit)](../../../t-sql/language-elements/bitwise-and-transact-sql.md) usando o valor da etapa 1 e o valor da opção de esquema desejado para determinar se a opção está definida.  
  
    -   Se o resultado for **0**, a opção não está definida.  
  
    -   Se o resultado for o valor da opção, a opção já está definida.  
  
3.  Se a opção não estiver definida, execute uma operação [| (OR de bit a bit)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) usando o valor da etapa 1 e o valor de opção de esquema desejado.  
  
4.  No Publicador do banco de dados de publicação, execute [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para `@publication`, o nome do artigo para `@article`, um valor de `schema_option` para `@property` e o resultado hexadecimal da etapa 3 para `@value`.  
  
5.  Execute o Agente de Instantâneo para gerar um novo instantâneo. Para obter mais informações, consulte [Criar e aplicar o instantâneo inicial](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
#### <a name="to-change-schema-options-for-an-existing-article-in-a-merge-publication"></a>Para alterar opções de esquema para um artigo existente em uma publicação de mesclagem  
  
1.  No Publicador do banco de dados de publicação, execute [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para `@publication` e o nome do artigo para `@article`. Observe o valor da coluna **schema_option** no conjunto de resultados.  
  
2.  Execute uma operação [& (AND bit a bit)](../../../t-sql/language-elements/bitwise-and-transact-sql.md) usando o valor da etapa 1 e o valor da opção de esquema desejado para determinar se a opção está definida.  
  
    -   Se o resultado for **0**, a opção não está definida.  
  
    -   Se o resultado for o valor da opção, a opção já está definida.  
  
3.  Se a opção não estiver definida, execute uma operação [| (OR de bit a bit)](../../../t-sql/language-elements/bitwise-or-transact-sql.md) usando o valor da etapa 1 e o valor de opção de esquema desejado.  
  
4.  No Publicador do banco de dados de publicação, execute [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md). Especifique o nome da publicação à qual o artigo pertence para `@publication`, o nome do artigo para `@article`, um valor de `schema_option` para `@property` e o resultado hexadecimal da etapa 3 para `@value`.  
  
5.  Execute o Agente de Instantâneo para gerar um novo instantâneo. Para obter mais informações, consulte [Criar e aplicar o instantâneo inicial](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Publicar dados e objetos de banco de dados](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Article Options for Transactional Replication](../../../relational-databases/replication/transactional/article-options-for-transactional-replication.md)  
  
  
