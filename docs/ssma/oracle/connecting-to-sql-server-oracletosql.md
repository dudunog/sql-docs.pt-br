---
title: Conectando-se ao SQL Server (OracleToSQL) | Microsoft Docs
description: Saiba como se conectar ao SQL Server para migrar um banco de dados Oracle. O SSMA Obtém e exibe metadados para bancos de dados no SQL Server.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Connecting to SQL Server,Synchronizing SQL Server Metadata
ms.assetid: 1b2a8059-1829-4904-a82f-9c06de1e245f
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 34e357ce88d75942d4784dbbbb7b43ad40150fa3
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/29/2020
ms.locfileid: "87396655"
---
# <a name="connecting-to-sql-server-oracletosql"></a>Conectar-se ao SQL Server (OracleToSQL)
Para migrar bancos de dados Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 R2 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014, você deve se conectar a qualquer uma dessas instâncias de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando você se conecta, o SSMA obtém metadados sobre todos os bancos de dados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e exibe os metadados do banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados. O SSMA armazena informações sobre a qual instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] você está conectado, mas não armazena senhas.  
  
Sua conexão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permanecerá ativa até que você feche o projeto. Quando você reabrir o projeto, deverá se reconectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se quiser uma conexão ativa com o servidor. Você pode trabalhar offline até carregar os objetos de banco [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de dados no e migrar.  
  
Os metadados sobre a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não são sincronizados automaticamente. Em vez disso, para atualizar os metadados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, você deve atualizar manualmente os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados. Para obter mais informações, consulte a seção "sincronizando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] metadados" mais adiante neste tópico.  
  
## <a name="required-sql-server-permissions"></a>Permissões de SQL Server necessárias  
A conta usada para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requer permissões diferentes dependendo das ações que a conta executa:  
  
-   Para converter objetos Oracle em [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxe, para atualizar metadados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou para salvar a sintaxe convertida em scripts, a conta deve ter permissão para fazer logon na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para carregar objetos de banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a conta deve ser membro da função de servidor **sysadmin** . Isso é necessário para instalar assemblies CLR.  
  
-   Para migrar dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o, a conta deve ser membro da função de servidor **sysadmin** . Isso é necessário para executar os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pacotes de migração de dados do agente.  
  
-   Para executar o código gerado pelo SSMA, a conta deve ter permissões de **execução** para todas as funções definidas pelo usuário no esquema de **ssma_oracle** do banco de dados de destino. Essas funções fornecem funcionalidade equivalente às funções do sistema Oracle e são usadas por objetos convertidos.  
  
Se a conta usada para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for executar todas as tarefas de migração, a conta deverá ser membro da função de servidor **sysadmin** .  
  
## <a name="establishing-a-sql-server-connection"></a>Estabelecendo uma conexão SQL Server  
Antes de converter objetos de banco de dados Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxe, você deve estabelecer uma conexão com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que você deseja migrar o banco de dados Oracle ou bancos.  
  
Ao definir as propriedades de conexão, você também especifica o banco de dados em que os objetos e data serão migrados. Você pode personalizar esse mapeamento no nível de esquema do Oracle depois de se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Mapping Oracle schemas to SQL Server schemas &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md).  
  
> [!IMPORTANT]  
> Antes de tentar se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , verifique se a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está em execução e pode aceitar conexões.  
  
**Para se conectar ao SQL Server**  
  
1.  No menu **arquivo** , selecione **conectar-se a SQL Server**.  
  
    Se você se conectou anteriormente ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o nome do comando será **reconectado a SQL Server**.  
  
2.  Na caixa de diálogo conexão, digite ou selecione o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   Se você estiver se conectando à instância padrão no computador local, poderá inserir **localhost** ou um ponto (**.**).  
  
    -   Se você estiver se conectando à instância padrão em outro computador, insira o nome do computador.  
  
    -   Se você estiver se conectando a uma instância nomeada em outro computador, insira o nome do computador seguido por uma barra invertida e, em seguida, o nome da instância, como MyServer\MyInstance.  
  
3.  Se sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver configurada para aceitar conexões em uma porta não padrão, insira o número da porta que é usado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexões na caixa **porta do servidor** . Para a instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o número da porta padrão é 1433. Para instâncias nomeadas, o SSMA tentará obter o número da porta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serviço navegador.  
  
4.  Na caixa **banco de dados** , digite o nome do banco de dados de destino.  
  
    Essa opção não está disponível quando você se reconecta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
5.  Na caixa **autenticação** , selecione o tipo de autenticação a ser usado para a conexão. Para usar a conta atual do Windows, selecione **autenticação do Windows**. Para usar um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] logon, selecione **SQL Server autenticação**e forneça o nome de logon e a senha.  
  
6.  Para conexão segura, dois controles são adicionados, as caixas de seleção **criptografar conexão** e **TrustServerCertificate** . Somente quando a opção **criptografar conexão** está marcada, a caixa de seleção **TrustServerCertificate** está visível. Quando **criptografar conexão** está marcado (true) e **TrustServerCertificate** está desmarcado (false), ele validará o SQL Server certificado SSL. A validação do certificado do servidor é parte do handshake SSL e garante que o servidor é o servidor correto para a conexão. Para garantir isso, um certificado deve ser instalado no lado do cliente, bem como no lado do servidor.  
  
7.  Clique em **Conectar**.  
  
**Compatibilidade de versão superior**  
  
-   Você poderá se conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto de migração criado for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Você poderá se conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto de migração criado for [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008, mas não será possível se conectar a versões inferiores, ou seja, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005.  
  
-   Você poderá se conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 quando o projeto criado for SQL Server 2012.  
  
|TIPO de projeto versus versão do servidor de destino|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005<br /> (Versão: 9. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008<br /> (Versão: 10. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 <br />(Versão: 11. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014 <br />(Versão: 12. x)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 <br />(Versão: 13. x)|BD SQL do Azure|  
|-|-|-|-|-|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005|Sim|Sim|Sim|Sim|Sim||  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008||Sim|Sim|Sim|Sim||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012|||Sim|Sim|Sim||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]2014||||Sim|Sim||
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016|||||Sim||
|BD SQL do Azure||||||Sim|
  
> [!IMPORTANT]
> A conversão dos objetos de banco de dados é executada de acordo com o tipo de projeto, mas não de acordo com a versão do à [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] qual você está conectado. No caso do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] projeto 2005, a conversão é realizada de acordo com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005, embora você esteja conectado a uma versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014 ou [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016).  
  
## <a name="synchronizing-sql-server-metadata"></a>Sincronizando metadados de SQL Server  
Metadados sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bancos de dados não são atualizados automaticamente. Os metadados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados é um instantâneo dos metadados quando você se conecta pela primeira vez ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ou na última atualização dos metadados. Você pode atualizar os metadados manualmente para todos os bancos de dados ou para qualquer banco de dados ou objeto de banco de dados individual.  
  
**Para sincronizar metadados**  
  
1.  Certifique-se de que você está conectado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Gerenciador de metadados, marque a caixa de seleção ao lado do banco de dados ou esquema de banco de dados que você deseja atualizar.  
  
    Por exemplo, para atualizar os metadados de todos os bancos de dados, selecione a caixa ao lado de **bancos de dados**.  
  
3.  Clique com o botão direito do mouse em **bancos**de dados ou em um esquema ou banco de dados individual e selecione **sincronizar com Banco de dados**.  
  
## <a name="next-step"></a>Próxima etapa  
A próxima etapa na migração depende de suas necessidades de projeto:  
  
-   Para personalizar o mapeamento entre esquemas e bancos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados e esquemas Oracle, consulte [mapeando esquemas oracle para SQL Server esquemas &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-schemas-to-sql-server-schemas-oracletosql.md).  
  
-   Para personalizar as opções de configuração para os projetos, consulte [definindo opções de projeto &#40;OracleToSQL&#41;](../../ssma/oracle/setting-project-options-oracletosql.md).  
  
-   Para personalizar o mapeamento de tipos de dados de origem e de destino, consulte [mapeando os tipos de dados Oracle e SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/mapping-oracle-and-sql-server-data-types-oracletosql.md).  
  
-   Se você não precisar executar nenhuma dessas tarefas, poderá converter as definições de objeto do banco de dados Oracle em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definições de objeto. Para obter mais informações, consulte [convertendo esquemas Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md).  
  
## <a name="see-also"></a>Consulte Também  
[Migrando bancos de dados Oracle para SQL Server &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
