---
title: Implementar um manipulador de lógica de negócios para um artigo de mesclagem | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], business logic handlers
- merge replication business logic handlers [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
- business logic handlers [SQL Server replication]
- BusinessLogicModule class
ms.assetid: ed477595-6d46-4fa2-b0d3-a5358903ec05
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 659bba7156ccc1c3a60bef38a51fd983554e4ead
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62721196"
---
# <a name="implement-a-business-logic-handler-for-a-merge-article"></a>Implementar um manipulador de lógica de negócios para um artigo de mesclagem
  Este tópico descreve como implementar um manipulador de lógica de negócios para um artigo de mesclagem no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a programação de replicação o RMO (Replication Management Objects).  
  
 O namespace <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> implementa uma interface que permite gravar lógicas comerciais complexas para manipular eventos que ocorrem durante o processo de sincronização da replicação de mesclagem. Os métodos do manipulador de lógica de negócios podem ser invocados pelo processo de replicação para cada linha alterada que seja replicada durante a sincronização.  
  
 O processo geral para implementar um manipulador de lógica de negócios é:  
  
1.  Crie o assembly de manipulador de lógica comercial.  
  
2.  Registre o assembly no Distribuidor.  
  
3.  Implante o assembly no servidor em que o Merge Agent executa. Para uma assinatura pull o agente é executado no Assinante e para uma assinatura push envio o agente é executado no Distribuidor. Durante o uso da sincronização da Web, o agente é executado no servidor da Web.  
  
4.  Crie um artigo que usa o manipulador de lógica de negócios ou modifique um artigo existente para usar o manipulador de lógica de negócios.  
  
 O manipulador de lógica de negócios que você especificar será executado para cada linha que for sincronizada. A lógica complexa e as chamadas para outros aplicativos ou serviços de rede podem comprometer o desempenho. Para mais informações sobre manipuladores de lógica de negócios, consulte [Executar lógica de negócios durante a sincronização de mesclagem](merge/execute-business-logic-during-merge-synchronization.md).  
  
 **Neste tópico**  
  
-   **Para implementar um manipulador de lógica de negócios para um artigo de mesclagem, usando:**  
  
     [Programação de replicação](#ReplProg)  
  
     [Replication Management Objects (RMO)](#RMOProcedure)  
  
##  <a name="using-replication-programming"></a><a name="ReplProg"></a> Usando a programação de replicação  
  
#### <a name="to-create-and-deploy-a-business-logic-handler"></a>Para criar e implantar um manipulador de lógica de negócios  
  
1.  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio, crie um novo projeto para o assembly .NET que contém o código que implementa o manipulador de lógica de negócios.  
  
2.  Adicione referências ao projeto para os seguintes namespaces.  
  
    |Referência de assembly|Local|  
    |------------------------|--------------|  
    |<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM (instalação padrão)|  
    |<xref:System.Data>|GAC (componente do .NET Framework)|  
    |<xref:System.Data.Common>|GAC (componente do .NET Framework)|  
  
3.  Adicione uma classe que substitua a classe <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> .  
  
4.  Implemente a propriedade <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.HandledChangeStates%2A> para indicar os tipos de alterações que são controladas.  
  
5.  Substitua um ou mais dos seguintes métodos da classe <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> :  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.CommitHandler%2A> - invocado quando uma alteração de dados é confirmada durante sincronização.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteErrorHandler%2A> - invocado ao ocorrer um erro enquanto uma instrução DELETE é carregada ou baixada.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteHandler%2A> - invocado quando instruções DELETE são carregadas ou baixadas.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertErrorHandler%2A> - invocado ao acontecer um erro enquanto uma instrução INSERT é carregada ou baixada.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertHandler%2A> - invocado quando instruções INSERT são carregadas ou baixadas.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateConflictsHandler%2A> - invocado quando ocorrem instruções UPDATE conflitantes no Publicador ou Assinante.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateDeleteConflictHandler%2A> - invocado quando instruções UPDATE entram em conflito com instruções DELETE no Publicador e no Assinante.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateErrorHandler%2A> - invocado ao ocorrer um erro enquanto uma instrução UPDATE é carregada ou baixada.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateHandler%2A> - invocado quando instruções UPDATE são carregadas ou baixadas.  
  
6.  Construa o projeto para criar o assembly de manipulador de lógica de negócios.  
  
7.  Implante o assembly no diretório que contém o arquivo executável do Merge Agent (replmerg.exe), que, para uma instalação padrão, é [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM, ou instale-o no cache de assembly global .NET (GAC). O assembly só deve ser instalado no GAC se outros aplicativos, além do Merge Agent, exigirem acesso para o assembly. O assembly pode ser instalado no GAC por meio da ferramenta de cache de assembly global (**Gacutil.exe)** fornecida no .NET Framework SDK.  
  
    > [!NOTE]  
    >  O manipulador de lógica de negócios precisa ser implantado em todos os servidores em que o Merge Agent é executado, incluindo-se o servidor IIS que hospeda o replisapi.dll durante o uso da sincronização da Web.  
  
#### <a name="to-register-a-business-logic-handler"></a>Para registrar um manipulador de lógica de negócios  
  
1.  No Publicador, execute [sp_enumcustomresolvers &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) para verificar se o assembly ainda não foi registrado como manipulador de lógica de negócios.  
  
2.  No distribuidor, execute [sp_registercustomresolver &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql), especificando um nome amigável para o manipulador de lógica de negócios **@article_resolver**para, um valor `true` de **@is_dotnet_assembly**para, o nome do assembly para **@dotnet_assembly_name**e o nome totalmente qualificado da classe que substitui <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> para. **@dotnet_class_name**  
  
    > [!NOTE]  
    >  Se o assembly não estiver implantado no mesmo diretório que o Agente de Mesclagem executável, no mesmo diretório que o aplicativo que inicia de forma síncrona o Agente de Mesclagem ou no GAC (cache de assembly global), você precisará especificar o caminho completo com o nome do **@dotnet_assembly_name**assembly para. Ao usar a sincronização da Web, especifique o local do assembly no servidor da Web.  
  
#### <a name="to-use-a-business-logic-handler-with-a-new-table-article"></a>Para usar um manipulador de lógica de negócios com um novo artigo de tabela  
  
1.  Execute [sp_addmergearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) para definir um artigo, especificando o nome amigável do manipulador de lógica de negócios para **@article_resolver**. Para obter mais informações, consulte [Define an Article](publish/define-an-article.md).  
  
#### <a name="to-use-a-business-logic-handler-with-an-existing-table-article"></a>Para usar um manipulador de lógica de negócios com um artigo de tabela existente  
  
1.  Execute [sp_changemergearticle &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql), especificando **@publication**, **@article**, um valor de **article_resolver** para **@property**e o nome amigável do manipulador de lógica de negócios para **@value**.  
  
###  <a name="examples-replication-programming"></a><a name="TsqlExample"></a>Exemplos (programação de replicação)  
 Esse exemplo mostra um manipulador de lógica de negócios que cria um log de auditoria.  
  
 [!code-csharp[HowTo#rmo_BusinessLogicCode](../../snippets/csharp/SQL15/replication/howto/cs/businesslogic.cs#rmo_businesslogiccode)]  
  
 [!code-vb[HowTo#rmo_vb_BusinessLogicCode](../../snippets/visualbasic/SQL15/replication/howto/vb/businesslogic.vb#rmo_vb_businesslogiccode)]  
  
 O exemplo a seguir registra um assembly de manipulador de lógica de negócios no Distribuidor e altera um artigo de mesclagem existente para usar essa lógica de negócios personalizada.  
  
 [!code-sql[HowTo#sp_RegisterBLH_10](../../snippets/tsql/SQL15/replication/howto/tsql/registerblh_10.sql#sp_registerblh_10)]  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> Usando o RMO (Replication Management Objects)  
  
#### <a name="to-create-a-business-logic-handler"></a>Para criar um manipulador de lógica de negócios  
  
1.  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio, crie um novo projeto para o assembly .NET que contém o código que implementa o manipulador de lógica de negócios.  
  
2.  Adicione referências ao projeto para os seguintes namespaces.  
  
    |Referência de assembly|Local|  
    |------------------------|--------------|  
    |<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM (instalação padrão)|  
    |<xref:System.Data>|GAC (componente do .NET Framework)|  
    |<xref:System.Data.Common>|GAC (componente do .NET Framework)|  
  
3.  Adicione uma classe que substitua a classe <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> .  
  
4.  Implemente a propriedade <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.HandledChangeStates%2A> para indicar os tipos de alterações que são controladas.  
  
5.  Substitua um ou mais dos seguintes métodos da classe <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> :  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.CommitHandler%2A> - invocado quando uma alteração de dados é confirmada durante sincronização.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteErrorHandler%2A> - invocado se um erro ocorrer enquanto uma instrução DELETE estiver sendo carregada ou baixada.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteHandler%2A> - invocado quando instruções DELETE são carregadas ou baixadas.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertErrorHandler%2A> - invocado se um erro ocorrer quando uma instrução INSERT estiver sendo carregada ou baixada.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertHandler%2A> - invocado quando instruções INSERT são carregadas ou baixadas.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateConflictsHandler%2A> - invocado quando ocorrem instruções UPDATE conflitantes no Publicador ou Assinante.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateDeleteConflictHandler%2A> - invocado quando instruções UPDATE entram em conflito com instruções DELETE no Publicador e no Assinante.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateErrorHandler%2A> - invocado se um erro ocorrer quando uma instrução UPDATE estiver sendo carregada ou baixada.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateHandler%2A> - invocado quando instruções UPDATE são carregadas ou baixadas.  
  
    > [!NOTE]  
    >  Qualquer conflito de artigo não explicitamente manipulado pela lógica corporativa personalizada que você utiliza são manipulados pelo resolvedor padrão para o artigo.  
  
6.  Construa o projeto para criar o assembly de manipulador de lógica de negócios.  
  
#### <a name="to-register-a-business-logic-handler"></a>Para registrar um manipulador de lógica de negócios  
  
1.  Crie uma conexão com o Distribuidor usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.ReplicationServer>. Passe o <xref:Microsoft.SqlServer.Management.Common.ServerConnection> da etapa 1.  
  
3.  Chame <xref:Microsoft.SqlServer.Replication.ReplicationServer.EnumBusinessLogicHandlers%2A> e verifique o objeto <xref:System.Collections.ArrayList> retornado para assegurar que o assembly não tenha sido já registrado como um manipulador de lógica de negócios.  
  
4.  Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler>. Especifique as seguintes propriedades:  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.DotNetAssemblyName%2A> - o nome do assembly .NET. Se o assembly não estiver implantado no mesmo diretório que o executável Merge Agent, no mesmo diretório que o aplicativo que inicia de forma síncrona o Merge Agent ou no GAC, você deve incluir o caminho completo com o nome do assembly. Você deve incluir o caminho completo com o nome do assembly ao usar um manipulador de lógica de negócios com sincronização da Web.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.DotNetClassName%2A> - o nome totalmente qualificado da classe que substitui <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> e implementa o manipulador de lógica de negócios.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A> - um nome amigável que você usa ao acessar o manipulador de lógica de negócios.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.IsDotNetAssembly%2A> - um valor de `true`.  
  
#### <a name="to-deploy-a-business-logic-handler"></a>Para implantar um manipulador de lógica de negócios  
  
1.  Implante o assembly no servidor em que o Merge Agent é executado no local do arquivo especificado quando o manipulador de lógica de negócios foi registrado no Distribuidor. Para uma assinatura pull o agente é executado no Assinante e para uma assinatura push envio o agente é executado no Distribuidor. Durante o uso da sincronização da Web, o agente é executado no servidor da Web. Se no caminho completo não tiver sido incluído com o nome do assembly quando o manipulador de lógica de negócios foi registrado, implante o assembly no mesmo diretório que o executável Merge Agent, no mesmo diretório que o aplicativo que inicia de forma síncrona o Merge Agent. Você pode instalar o assembly no GAC se houver múltiplos aplicativos que usem o mesmo assembly.  
  
#### <a name="to-use-a-business-logic-handler-with-a-new-table-article"></a>Para usar um manipulador de lógica de negócios com um novo artigo de tabela  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.MergeArticle>. Defina as seguintes propriedades:  
  
    -   Nome do artigo para <xref:Microsoft.SqlServer.Replication.Article.Name%2A>.  
  
    -   Nome da publicação para <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>.  
  
    -   O nome do banco de dados de publicação para <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A>.  
  
    -   O nome amigável do manipulador de lógica de negócios (<xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A>) para <xref:Microsoft.SqlServer.Replication.MergeArticle.ArticleResolver%2A>.  
  
3.  Chame o método <xref:Microsoft.SqlServer.Replication.Article.Create%2A> . Para obter mais informações, consulte [Define an Article](publish/define-an-article.md).  
  
#### <a name="to-use-a-business-logic-handler-with-an-existing-table-article"></a>Para usar um manipulador de lógica de negócios com um artigo de tabela existente  
  
1.  Crie uma conexão com o Publicador usando a classe <xref:Microsoft.SqlServer.Management.Common.ServerConnection> .  
  
2.  Criar uma instância da classe <xref:Microsoft.SqlServer.Replication.MergeArticle>.  
  
3.  Defina as propriedades <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>e <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> .  
  
4.  Defina a conexão da etapa 1 para a propriedade <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> .  
  
5.  Chame o método <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> para obter as propriedades do objeto. Se esse método retornar `false`, as propriedades de artigo na etapa 3 foram definidas incorretamente ou o artigo não existe. Para obter mais informações, consulte [View and Modify Article Properties](publish/view-and-modify-article-properties.md).  
  
6.  Defina o nome amigável do manipulador de lógica de negócios para <xref:Microsoft.SqlServer.Replication.MergeArticle.ArticleResolver%2A>. Esse é o valor da propriedade <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A> especificada ao registrar o manipulador de lógica de negócios.  
  
###  <a name="examples-rmo"></a><a name="PShellExample"></a> Exemplos (RMO)  
 Este exemplo é um manipulador de lógica de negócios que realiza log de informações sobre inserções, atualizações e exclusões no Assinante.  
  
 [!code-csharp[HowTo#rmo_BusinessLogicCode](../../snippets/csharp/SQL15/replication/howto/cs/businesslogic.cs#rmo_businesslogiccode)]  
  
 [!code-vb[HowTo#rmo_vb_BusinessLogicCode](../../snippets/visualbasic/SQL15/replication/howto/vb/businesslogic.vb#rmo_vb_businesslogiccode)]  
  
 Este exemplo registra um manipulador de lógica de negócios no Distribuidor.  
  
 [!code-csharp[HowTo#rmo_RegisterBLH_10](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_registerblh_10)]  
  
 [!code-vb[HowTo#rmo_vb_RegisterBLH_10](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_registerblh_10)]  
  
 Este exemplo altera um artigo existente para usar o manipulador de lógica de negócios.  
  
 [!code-csharp[HowTo#rmo_ChangeMergeArticle_BLH](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_changemergearticle_blh)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergeArticle_BLH](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_changemergearticle_blh)]  
  
## <a name="see-also"></a>Consulte Também  
 [Implementar um resolvedor de conflitos personalizado para um artigo de mesclagem](implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [Depurar um manipulador de lógica de negócios &#40;programação de replicação&#41;](debug-a-business-logic-handler-replication-programming.md)   
 [Práticas recomendadas de segurança de replicação](security/replication-security-best-practices.md)   
 [Conceitos de objetos de gerenciamento de replicação](concepts/replication-management-objects-concepts.md)  
  
  
