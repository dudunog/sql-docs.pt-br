---
title: Replay Requirements
titleSuffix: SQL Server Profiler
description: Saiba quais classes de evento e colunas de dados capturar em um rastreamento para que você possa reproduzir dados de rastreamento com o SQL Server Profiler ou o Distributed Replay Utility.
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 0e01dfc7-84b9-47f6-8bf7-b0656df4fa7d
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: d5fa4964a2ffb0d62777c25aa0d0c6ef205ee94b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789931"
---
# <a name="replay-requirements"></a>Replay Requirements

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Para reproduzir dados de rastreamento com o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ou o Distributed Replay Utility, um conjunto específico de colunas e classes de evento deve ser capturado no rastreamento. Essas configurações serão habilitadas por padrão se o modelo de rastreamento **TSQL_Replay** for usado para configurar um rastreamento que será usado posteriormente para reprodução. Este tópico descreve estas configurações e outros requisitos de reprodução.  
  
> [!NOTE]  
>  É recomendável usar o Distributed Replay Utility para reproduzir um aplicativo OLTP intensivo (com muitas conexões simultâneas ativas ou alta taxa de transferência). O Distributed Replay Utility pode reproduzir dados de rastreamento de vários computadores, com uma simulação melhor de uma carga de trabalho de missão crítica. Para obter mais informações, consulte [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md).  
  
## <a name="event-classes-required-for-replay"></a>Classes de evento necessárias para reprodução  
 Para serem reproduzidos pelo [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], o conjunto de classes de evento a seguir, além de outras classes de evento que você deseja monitorar, deve ser capturado no rastreamento:  
  
-   **CursorClose (** necessário apenas para a reprodução de cursores do lado do servidor)  
  
-   **CursorExecute** (necessário apenas para a repetição de cursores do lado do servidor)  
  
-   **CursorOpen** (necessário apenas para a repetição de cursores do lado do servidor)  
  
-   **CursorPrepare** (necessário apenas para a repetição de cursores do lado do servidor)  
  
-   **CursorUnprepare** (necessário apenas para a repetição de cursores do lado do servidor)  
  
-   **Audit Login**  
  
-   **Audit Logout**  
  
-   **ExistingConnection**  
  
-   **RPC Output Parameter**  
  
-   **RPC:Completed**  
  
-   **RPC:Starting**  
  
-   **Exec Prepared SQL** (necessário apenas para a repetição de instruções SQL preparadas do lado do servidor)  
  
-   **Prepare SQL** (necessário apenas para a reprodução de instruções SQL preparadas do lado do servidor)  
  
-   **SQL:BatchCompleted**  
  
-   **SQL:BatchStarting**  
  
## <a name="data-columns-required-for-replay"></a>Colunas de dados necessárias para reprodução  
 Além das outras colunas de dados que você deseja capturar, as seguintes colunas de dados devem ser capturadas em um rastreamento para que ele possa ser reproduzido:  
  
-   **Event Class**  
  
-   **EventSequence**  
  
-   **TextData**  
  
-   **Nome do Aplicativo**  
  
-   **LoginName**  
  
-   **DatabaseName**  
  
-   **ID do banco de dados**  
  
-   **ClientProcessID**  
  
-   **HostName**  
  
-   **ServerName**  
  
-   **Binary Data**  
  
-   **SPID**  
  
-   **Start Time**  
  
-   **EndTime**  
  
-   **IsSystem**  
  
-   **NTDomainName**  
  
-   **NTUserName**  
  
-   **Erro**  
  
> [!NOTE]  
>  Use o modelo de rastreamento **TSQL_Replay** para rastreamentos que capturam dados para reprodução.  
  
## <a name="other-replay-requirements"></a>Outros requisitos da reprodução  
 No Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a reprodução verifica a presença dos eventos e colunas necessários. Esta alteração ajuda a melhorar a precisão de repetição e retira a incerteza da repetição para solução de problemas, quando há dados necessários faltando. A repetição retorna um erro e para de repetir um arquivo quando dados necessários estão faltando em um rastreamento.  
  
 Para repetir um rastreamento contra um servidor (o destino) no qual o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esteja executando, diferente do que foi rastreado originalmente (a origem), certifique-se de ter sido feito o seguinte:  
  
-   Todos os logons e usuários contidos no rastreamento já devem ter sido criados no destino e no mesmo banco de dados da origem.  
  
-   Todos os logons e usuários no destino devem ter as mesmas permissões que tinham na origem.  
  
-   Todas as senhas de logon devem ser idênticas àquelas do usuário que executa a repetição.  
  
-   As IDs do banco de dados no destino devem, idealmente, ser idênticas àquela na origem. No entanto, se essas permissões não forem iguais, a correspondência poderá ser executada com base no **DatabaseName** se estiver presente no rastreamento.  
  
-   O banco de dados padrão de cada logon contido no rastreamento deve estar configurado (no destino) para o respectivo banco de dados de destino do logon. Por exemplo, o rastreamento a ser repetido contém atividade do logon **Fred**no banco de dados **Fred_Db** na origem. Portanto, no destino, o banco de dados padrão do logon **Fred**deve estar configurado para o banco de dados que corresponde a **Fred_Db** (mesmo que o nome do banco de dados seja diferente). Para configurar o banco de dados padrão do logon, use o procedimento armazenado de sistema **sp_defaultdb** .  
  
 A repetição de eventos associados com logons faltantes ou incorretos resulta em erros de repetição, mas a operação de repetição continua.  
  
 Para obter informações sobre quais permissões são necessárias para reproduzir um rastreamento, veja [Permissões necessárias para executar o SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Reproduzir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-table-sql-server-profiler.md)   
 [Reproduzir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/replay-a-trace-file-sql-server-profiler.md)   
 [Referência de classe de evento do SQL Server](../../relational-databases/event-classes/sql-server-event-class-reference.md)   
 [sp_defaultdb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)   
 [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md)  
  
  
