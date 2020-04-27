---
title: Conexão de diagnóstico para administradores de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- server management [SQL Server], connections
- administrator connections [SQL Server]
- ports [SQL Server], DAC
- DAC
- network connections [SQL Server], dedicated administrator
- diagnostic connections [SQL Server]
- connections [SQL Server], dedicated administrator
- ports [SQL Server]
- dedicated administrator connections [SQL Server]
ms.assetid: 993e0820-17f2-4c43-880c-d38290bf7abc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5e8022dd9a7bd4f301ca55f60614e1b13369b804
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62810417"
---
# <a name="diagnostic-connection-for-database-administrators"></a>Conexão de diagnóstico para administradores de banco de dados
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece uma conexão diagnóstica especial para administradores quando conexões padrão com o servidor não são possíveis. Esta conexão diagnóstica permite que um administrador acesse o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para executar consultas diagnósticas e resolver problemas mesmo quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não está respondendo às solicitações de conexão padrão.  
  
 Esta conexão de administrador dedicada (DAC) oferece suporte à criptografia e outros recursos de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O DAC só permite alterar o contexto de usuário para outro usuário admin.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esforça-se o máximo para o êxito de uma conexão DAC, mas pode falhar em situações extremas.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].|  
  
## <a name="connecting-with-dac"></a>Conectando com DAC  
 Por padrão, a conexão só é permitida de um cliente executando no servidor. As conexões de rede apenas são permitidas se forem configuradas com o procedimento armazenado sp_configure com a [opção de conexões admin remotas](remote-admin-connections-server-configuration-option.md).  
  
 Apenas membros da função sysadmin do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem se conectar usando o DAC.  
  
 O DAC está disponível e tem suporte através do utilitário de prompt de comando **sqlcmd** que usa uma opção de administrador especial ( **-A**). Para obter mais informações sobre como usar **sqlcmd**, veja [Usar sqlcmd com variáveis de script](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md). Você também pode conectar a prefixação `admin:`ao nome da instância no formato **sqlcmd-Sadmin:** _<instance_name>._ Você também pode iniciar um DAC de um [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] editor de consultas conectando `admin:` \<-se ao *instance_name*>.  
  
## <a name="restrictions"></a>Restrições  
 Como o DAC existe somente para diagnosticar problemas do servidor em circunstâncias raras, há algumas restrições na conexão:  
  
-   Para garantir que existam recursos disponíveis para a conexão, apenas um DAC é permitido por instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se uma conexão DAC já estiver ativa, qualquer nova solicitação de conexão via DAC será negada com o erro 17810.  
  
-   Para conservar recursos, o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] não escuta na porta do DAC, a menos que tenha sido iniciado com um sinalizador de rastreamento 7806.  
  
-   Inicialmente, o DAC tenta se conectar ao banco de dados padrão associado ao logon. Após uma conexão bem-sucedida, você pode se conectar ao banco de dados mestre. Se o banco de dados padrão estiver offline ou não estiver disponível, a conexão retornará o erro 4060. Entretanto, ela terá êxito se você substituir o banco de dados padrão para se conectar ao banco de dados mestre em vez de usar o seguinte comando:  
  
     **sqlcmd -A -d master**  
  
     Recomendamos que você se conecte ao banco de dados mestre com o DAC porque esse mestre estará com certeza disponível se a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] for iniciada.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] impede a execução de consultas paralelas ou comandos com o DAC. Por exemplo, erro 3637 será gerado se você executar uma das seguintes instruções com o DAC:  
  
    -   RESTORE  
  
    -   BACKUP  
  
-   Apenas recursos limitados têm garantia de disponibilidade com o DAC. Não use o DAC para executar consultas com muitos recursos (por exemplo, uma junção complexa em tabela grande) ou consultas que podem ser bloqueadas. Isso ajuda a evitar que o DAC combine qualquer problema de servidor existente. Para evitar possíveis cenários de bloqueio, se você tiver que executar consultas que possam ser bloqueadas, execute-as nos níveis de isolamento baseados em instantâneos, se possível. Caso contrário, defina o nível de isolamento da transação como READ UNCOMMITTED e o valor LOCK_TIMEOUT como um valor curto, como 2000 milissegundos, ou ambos. Isso impedirá que a sessão DAC seja bloqueada. Porém, dependendo do estado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , a sessão DAC pode ser travada imediatamente. É possível que você consiga encerrar a sessão DAC usando CNTRL-C, mas não é garantido. Nesse caso, sua única opção pode ser reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Para garantir a conectividade e resolver problemas com o DAC, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reserva recursos limitados para processar comandos executados no DAC. Esses recursos geralmente só são suficientes para diagnósticos simples e resolução de problemas de funções, como as listadas abaixo.  
  
 Embora seja teoricamente possível executar qualquer instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que não tenha que ser executada paralelamente no DAC, recomendamos que você restrinja o uso dos seguintes comandos de diagnóstico e resolução de problemas:  
  
-   Consulta de exibições de gerenciamento dinâmico para diagnósticos básicos como sys.dm_tran_locks, para o status de bloqueio, sys.dm_os_memory_cache_counters, para verificar o funcionamento dos caches, e sys.dm_exec_requests e sys.dm_exec_sessions, para sessões e solicitações ativas. Evite exibições de gerenciamento dinâmico que sejam intensivas do recurso (por exemplo, sys.dm_tran_version_store examina o repositório de versão completo e pode causar E/S extensiva) ou que usem junções complexas. Para obter informações sobre implicações de desempenho, consulte a documentação sobre [exibições de gerenciamento dinâmico](../../relational-databases/views/views.md)específicas.  
  
-   Consulta de exibições do catálogo.  
  
-   Comandos DBCC básicos como DBCC FREEPROCCACHE, DBCC FREESYSTEMCACHE, DBCC DROPCLEANBUFFERS`,` e DBCC SQLPERF. Não execute comandos com uso intensivo de recursos, como **DBCC** CHECKDB, DBCC DBREINDEX ou DBCC SHRINKDATABASE.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] Comando KILL *\<spid>* . Dependendo do estado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o comando KILL nem sempre pode ter êxito; assim, a única opção pode ser reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A seguir, algumas diretrizes gerais:  
  
    -   Verifique se o SPID foi realmente interrompido consultando `SELECT * FROM sys.dm_exec_sessions WHERE session_id = <spid>`. Se nenhuma linha for retornada, significa que a sessão foi interrompida.  
  
    -   Se a sessão ainda estiver ativa, verifique se há tarefas atribuídas para ela executando a consulta `SELECT * FROM sys.dm_os_tasks WHERE session_id = <spid>`. Se a tarefa estiver ativa, é provável que sua sessão esteja sendo interrompida no momento. Observe que isso pode levar um tempo considerável e não ter êxito nenhum.  
  
    -   Se não houver nenhuma tarefa no sys.dm_os_tasks associado a esta sessão, mas a sessão continuar em sys.dm_exec_sessions após a execução do comando KILL, significa que você não tem um trabalhador disponível. Selecione uma das tarefas atualmente em execução (uma tarefa listada na exibição de sys.dm_os_tasks com `sessions_id <> NULL`) e interrompa a sessão associada a ela para liberar o trabalhador. Observe que talvez não seja suficiente interromper apenas uma sessão: talvez seja necessário interromper várias.  
  
## <a name="dac-port"></a>Porta DAC  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verifica o DAC em uma porta TCP 1434, se estiver disponível, ou em uma porta TCP dinamicamente atribuída na inicialização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . O log de erros contém o número da porta que o DAC está escutando. Por padrão, a escuta do DAC aceita conexão apenas na porta local. Para obter um exemplo de código que ativa conexões de administração remota, veja [Opção remote admin connections de configuração de servidor](remote-admin-connections-server-configuration-option.md).  
  
 Depois que uma conexão de administração remota for configurada, a escuta do DAC será habilitada sem a necessidade de reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e um cliente poderá se conectar ao DAC remotamente. Você pode habilitar a escuta do DAC para aceitar conexões remotamente, mesmo que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não responda durante a primeira conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o DAC localmente e, em seguida, executar o procedimento armazenado sp_configure para aceitar conexão de conexões remotas.  
  
 Em configurações de cluster, o DAC estará offline, por padrão. Os usuários podem executar a opção conexão de administração remota do sp_configure para permitir que a escuta do DAC acesse uma conexão remota. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estiver respondendo e a escuta do DAC não estiver habilitada, talvez seja necessário reiniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para se conectar ao DAC. Dessa forma, recomendamos que você habilite a opção de configuração conexões de administração remotas em sistemas clusterizados.  
  
 A porta DAC é atribuída dinamicamente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durante a inicialização. Ao conectar-se à instância padrão, o DAC evita usar uma solicitação do Protocolo de Resolução (SSRP) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao serviço SQL Server Browser. Primeiro ele se conecta usando a porta TCP 1434. Se isso falhar, ele faz uma chamada ao SSRP para obter a porta. Se o navegador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estiver escutando as solicitações de SSRP, a solicitação de conexão retornará um erro. Consulte o log de erros para localizar o número da porta que o DAC está escutando. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for configurado para aceitar conexões de administração remotas, o DAC deverá ser iniciado com um número de porta explícito:  
  
 **sqlcmd-STCP:** _ \<servidor>,\<porta>_  
  
 O log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lista o número da porta para o DAC, que, por padrão, é 1434. Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver configurado para aceitar apenas conexões DAC locais, conecte usando o adaptador de loopback com o seguinte comando:  
  
 **sqlcmd-s 127.0.0.1**,`1434`  
  
## <a name="example"></a>Exemplo  
 Neste exemplo, um administrador nota que o servidor `URAN123` não está respondendo e deseja diagnosticar o problema. Para isso, o usuário ativa o utilitário de prompt de comando `sqlcmd` e se conecta ao servidor `URAN123` usando `-A` para indicar o DAC.  
  
 `sqlcmd -S URAN123 -U sa -P <xxx> -A`  
  
 Agora o administrador pode executar consultas para diagnosticar o problema e possivelmente encerrar as sessões sem-resposta.  
  
## <a name="related-tasks"></a>Related Tasks  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Usar sqlcmd com variáveis de script](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)  
  
 [Utilitário sqlcmd](../../tools/sqlcmd-utility.md)  
  
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)  
  
 [sp_who &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql)  
  
 [sp_lock &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-lock-transact-sql)  
  
 [KILL &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/kill-transact-sql)  
  
 [DBCC CHECKALLOC &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkalloc-transact-sql)  
  
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)  
  
 [DBCC OPENTRAN &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-opentran-transact-sql)  
  
 [DBCC INPUTBUFFER &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-inputbuffer-transact-sql)  
  
 [Opções de configuração do servidor &#40;SQL Server&#41;](server-configuration-options-sql-server.md)  
  
 [Funções e exibições de gerenciamento dinâmico relacionadas à transação &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql)  
  
 [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql)  
  
  
