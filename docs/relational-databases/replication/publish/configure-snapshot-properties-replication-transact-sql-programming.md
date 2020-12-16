---
title: Configurar propriedades de instantâneo (SP de Replicação)
description: Use procedimentos armazenados de replicação para configurar as propriedades de instantâneo para publicações transacionais ou de instantâneo.
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- snapshots [SQL Server replication], properties
ms.assetid: 978d150f-8971-458a-ab2b-3beba5937b46
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 8b072dec561882c8acd26cf36961a4802e886d05
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475657"
---
# <a name="configure-snapshot-properties-replication-transact-sql-programming"></a>Configurar propriedades de instantâneo (Programação Transact-SQL de replicação)
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  Propriedades de instantâneo podem ser definidas e modificadas de forma programada usando-se procedimentos armazenados de replicação, nos quais os procedimentos armazenados usados dependem do tipo de publicação.  
  
### <a name="to-configure-snapshot-properties-when-creating-a-snapshot-or-transactional-publication"></a>Para configurar propriedades de instantâneo ao criar uma publicação de instantâneo ou transacional  
  
1.  No Publicador, execute [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md). Especifique um nome de publicação para `@publication`, um valor de **instantâneo** ou **contínuo** para `@repl_freq` e um ou mais dos seguintes parâmetros relacionados a instantâneo:  
  
    -   `@alt_snapshot_folder` – especifique um caminho se o instantâneo para essa publicação for acessado daquele local em vez de ou além da pasta padrão de instantâneo.    
    -   `@compress_snapshot` – especifique um valor **true** se os arquivos de instantâneo na pasta de instantâneo alternativa forem compactados em formato de arquivo CAB [!INCLUDE[msCoName](../../../includes/msconame-md.md)].    
    -   `@pre_snapshot_script` – especifique o nome de arquivo e caminho completo de um arquivo **.sql** que será executado no Assinante durante a inicialização antes que o instantâneo inicial seja aplicado.    
    -   `@post_snapshot_script` – especifique o nome de arquivo e caminho completo de um arquivo **.sql** que será executado no Assinante durante a inicialização depois que o instantâneo inicial for aplicado.    
    -   `@snapshot_in_defaultfolder` – especifique um valor **false** se o instantâneo só estiver disponível em um local não padrão.  
  
     Para obter mais informações sobre como criar publicações, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
### <a name="to-configure-snapshot-properties-when-creating-a-merge-publication"></a>Para configurar propriedades de instantâneo ao criar uma publicação de mesclagem  
  
1.  No Publicador, execute [sp_addmergepublication](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md). Especifique um nome de publicação para `@publication`, um valor de **instantâneo** ou **contínuo** para `@repl_freq` e um ou mais dos seguintes parâmetros relacionados a instantâneo:  
  
    -   **alt_snapshot_folder** – especifique um caminho se o instantâneo para essa publicação for acessado daquele local em vez de ou além da pasta padrão de instantâneo.    
    -   `@compress_snapshot` – especifique um valor **true** se os arquivos de instantâneo na pasta de instantâneo alternativa forem compactados em formato de arquivo CAB.   
    -   `@pre_snapshot_script` – especifique o nome de arquivo e caminho completo de um arquivo **.sql** que será executado no Assinante durante a inicialização antes que o instantâneo inicial seja aplicado.    
    -   `@post_snapshot_script` – especifique o nome de arquivo e caminho completo de um arquivo **.sql** que será executado no Assinante durante a inicialização depois que o instantâneo inicial for aplicado.    
    -   `@snapshot_in_defaultfolder` – especifique um valor **false** se o instantâneo só estiver disponível em um local não padrão.  
  
2.  Para obter mais informações sobre como criar publicações, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
### <a name="to-modify-snapshot-properties-of-an-existing-snapshot-or-transactional-publication"></a>Para modificar as propriedades de instantâneo de uma publicação de instantâneo ou transacional existente  
  
1.  No Publicador do banco de dados de publicação, execute [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md). Especifique um valor **1** para `@force_invalidate_snapshot` e um dos seguintes valores para `@property`:  
  
    -   **alt_snapshot_folder** – também especifique um caminho novo para a pasta de instantâneo alternativa para `@value`.    
    -   **compress_snapshot** – especifique também um valor de **verdadeiro** ou **falso** para `@value` para indicar se arquivos de instantâneo na pasta de instantâneo alternativa são compactados no formato de arquivo CAB.    
    -   **pre_snapshot_script** – também para `@value`, especifique o nome de arquivo e caminho completo de um arquivo **.sql** que será executado no Assinante durante a inicialização antes que o instantâneo inicial seja aplicado.    
    -   **post_snapshot_script** – também para `@value`, especifique o nome de arquivo e caminho completo de um arquivo **.sql** que será executado no Assinante durante a inicialização depois que o instantâneo inicial for aplicado.    
    -   **@snapshot_in_defaultfolder** - especifique também um valor de **verdadeiro** ou **falso** para indicar se o instantâneo está disponível apenas em um local não padrão.  
  
2.  (Opcional) No Publicador do banco de dados de publicação, execute [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md). Especifique `@publication` e um ou mais dos parâmetros de credencial de segurança ou agendamento que estão sendo alterados.  
  
    > [!IMPORTANT]  
    >  Quando possível, solicite que os usuários insiram as credenciais de segurança em tempo de execução. Se for necessário armazenar credenciais em um arquivo de script, você deverá proteger o arquivo para impedir acesso não autorizado.  
  
3.  Execute o [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) no prompt de comando ou inicie o trabalho do Agente de Instantâneo para gerar um instantâneo novo. Para obter mais informações, consulte [Criar e aplicar o instantâneo inicial](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
### <a name="to-modify-snapshot-properties-of-an-existing-merge-publication"></a>Para modificar as propriedades de instantâneo de uma publicação de mesclagem existente  
  
1.  No Publicador do banco de dados de publicação, execute [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md). Especifique um valor **1** para `@force_invalidate_snapshot` e um dos seguintes valores para `@property**`:  
  
    -   **alt_snapshot_folder** – também especifique um caminho novo para a pasta de instantâneo alternativa para `@value`.    
    -   **compress_snapshot** – especifique também um valor de **verdadeiro** ou **falso** para `@value` para indicar se arquivos de instantâneo na pasta de instantâneo alternativa são compactados no formato de arquivo CAB.    
    -   **pre_snapshot_script** – também para `@value`, especifique o nome de arquivo e caminho completo de um arquivo **.sql** que será executado no Assinante durante a inicialização antes que o instantâneo inicial seja aplicado.    
    -   **post_snapshot_script** – também para `@value`, especifique o nome de arquivo e caminho completo de um arquivo **.sql** que será executado no Assinante durante a inicialização depois que o instantâneo inicial for aplicado.    
    -   **@snapshot_in_defaultfolder** - especifique também um valor de **verdadeiro** ou **falso** para indicar se o instantâneo está disponível apenas em um local não padrão.  
  
2.  Execute o [Replication Snapshot Agent](../../../relational-databases/replication/agents/replication-snapshot-agent.md) no prompt de comando ou inicie o trabalho do Agente de Instantâneo para gerar um instantâneo novo. Para obter mais informações, consulte [Criar e aplicar o instantâneo inicial](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
## <a name="example"></a>Exemplo  
 Esse exemplo cria uma publicação que usa uma pasta de instantâneo alternativa e um instantâneo compactado.  
  
 [!code-sql[HowTo#sp_mergealtsnapshot](../../../relational-databases/replication/codesnippet/tsql/configure-snapshot-prope_1.sql)]  
  
## <a name="see-also"></a>Consulte Também  
 [Modificar opções de instantâneo](../../../relational-databases/replication/snapshot-options.md)   
 [Executar scripts antes e depois da aplicação do instantâneo](../../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)   
 [Replication System Stored Procedures Concepts](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [Transferir instantâneos pelo FTP](../../../relational-databases/replication//publish/deliver-a-snapshot-through-ftp.md)   
 [Alterar propriedades da publicação e do artigo](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)  
  
  
