---
title: Classe de evento Exchange Spill | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Exchange Spill event class
ms.assetid: fb876cec-f88d-4975-b3fd-0fb85dc0a7ff
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 234c70cb0724bd313f7e98b92f8d043ff1e2bf5f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85642324"
---
# <a name="exchange-spill-event-class"></a>classe de evento Exchange Spill
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  A classe de evento **Exchange Spill** indica que os buffers de comunicação em um plano de consulta paralelo foram temporariamente gravados no banco de dados **tempdb** . Isso ocorre raramente e somente quando um plano de consulta tiver exames de vários intervalos.  
  
 Normalmente, a consulta do [!INCLUDE[tsql](../../includes/tsql-md.md)] que gera tais exames de intervalo tem muitos operadores BETWEEN, cada um dos quais seleciona um intervalo de linhas de uma tabela ou um índice. Uma alternativa é obter vários intervalos usando expressões como (T.a > 10 AND T.a < 20) ou (T.a > 100 AND T.a < 120). Além disso, os planos de consulta devem exigir que esses intervalos sejam examinados em ordem, porque existe uma cláusula ORDER BY em T.a ou um iterador do plano requer que ele consuma as tuplas na ordem classificada.  
  
 Quando um plano de consulta para tal consulta tem vários operadores **Parallelism** , os buffers de comunicação de memória usados pelos operadores **Parallelism** ficam completos e pode surgir uma situação em que o progresso da execução da consulta é interrompido. Nessa situação, um dos operadores **Parallelism** grava seu buffer de saída em **tempdb** (uma operação chamada *exchange spill*) de modo que possa consumir linhas de alguns de seus buffers de entrada. Finalmente, as linhas derramadas são devolvidas ao consumidor quando este estiver pronto para consumi-las.  
  
 Muito raramente, vários exchange spills podem ocorrer no mesmo plano de execução, fazendo com que a execução da consulta seja lenta. Se você notar mais de cinco derramamentos na execução do mesmo plano de consulta, contate seu profissional de suporte.  
  
 Algumas vezes, os exchange spills são transitórios e podem desaparecer como alterações de distribuição de dados.  
  
 Há várias maneiras de evitar eventos de exchange spills:  
  
-   Omita a cláusula ORDER BY se você não precisar que o conjunto de resultados seja ordenado.  
  
-   Se ORDER BY for necessário, elimine a coluna que participa de vários exames de intervalo (T.a no exemplo acima) da cláusula ORDER BY.  
  
-   Usando uma dica de índice, force o otimizador a usar um caminho de acesso diferente na tabela em questão.  
  
-   Reescreva a consulta para produzir um plano de execução de consulta diferente.  
  
-   Force a execução serial da consulta adicionando a opção MAXDOP = 1 no final da operação da consulta ou índice. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) e [Configurar operações de índice paralelo](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
> [!IMPORTANT]  
>  Para determinar o local em que o evento **Exchange Spill** está ocorrendo quando o otimizador de consultas gera um plano de execução, também é necessário coletar uma classe de evento Showplan no rastreamento. É possível escolher qualquer uma das classes de evento Showplan, exceto as classes de evento **Showplan Text** e **Showplan Text (Unencoded)** , que não retornam a ID do nó. As ID do nó nos Showplans identificam cada operação que o otimizador de consultas executa ao gerar um plano de execução de consulta. Essas operações são chamadas operadores e cada operador no Showplan possui uma ID de nó. A coluna **ObjectID** dos eventos **Exchange Spill** corresponde à ID do nó nas classes de eventos Showplan. Assim, é possível determinar o operador ou a operação que gerou o erro.  
  
## <a name="exchange-spill-event-class-data-columns"></a>Colunas de dados da classe de evento Exchange Spill  
  
|Nome da coluna de dados|Tipo de dados|Descrição|ID da coluna|Filtrável|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|Nome do aplicativo cliente que criou a conexão com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa coluna é populada com os valores passados pelo aplicativo e não com o nome exibido do programa.|10|Sim|  
|**ClientProcessID**|**int**|ID atribuída pelo computador host ao processo em que o aplicativo cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer a ID de processo do cliente.|9|Sim|  
|**DatabaseID**|**int**|ID do banco de dados especificado pela instrução USE de *database* ou o banco de dados padrão se nenhuma instrução USE de *database* tiver sido emitida para uma determinada instância. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibirá o nome do banco de dados se a coluna de dados **ServerName** for capturada no rastreamento e o servidor estiver disponível. Determine o valor para um banco de dados usando a função DB_ID.|3|Sim|  
|**DatabaseName**|**nvarchar**|Nome do banco de dados no qual a instrução do usuário está sendo executada.|35|Sim|  
|**EventClass**|**int**|Tipo de evento = 127.|27|Não|  
|**EventSequence**|**int**|Sequência de um determinado evento na solicitação.|51|Não|  
|**EventSubClass**|**int**|Tipo de subclasse de evento.<br /><br /> 1= Início do derramamento<br /><br /> 2= Término do derramamento|21|Sim|  
|**GroupID**|**int**|ID do grupo de carga de trabalho no qual o evento de Rastreamento do SQL dispara.|66|Sim|  
|**HostName**|**nvarchar**|Nome do computador no qual o cliente está sendo executado. Essa coluna de dados será populada se o cliente fornecer o nome do host. Para determinar o nome do host, use a função HOST_NAME.|8|Sim|  
|**IsSystem**|**int**|Indica se o evento ocorreu em um processo do sistema ou do usuário. 1 = sistema, 0 = usuário.|60|Sim|  
|**LoginName**|**nvarchar**|Nome do logon do usuário (o logon de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou as credenciais de logon do Windows no formato *\<DOMAIN>\\<username\>* ).|11|Sim|  
|**LoginSid**|**imagem**|Número SID (identificação de segurança) do usuário que fez logon. Você pode encontrar essas informações na tabela **syslogins** do banco de dados **master** . Cada SID é exclusivo para cada logon no servidor.|41|Sim|  
|**NTDomainName**|**nvarchar**|O domínio do Windows ao qual o usuário pertence.|7|Sim|  
|**NTUserName**|**nvarchar**|Nome do usuário do Windows.|6|Sim|  
|**ObjectID**|**int**|ID de objeto atribuída pelo sistema. Corresponde à ID do nó nos Showplans.|22|Sim|  
|**RequestID**|**int**|ID da solicitação que contém a instrução.|49|Sim|  
|**ServerName**|**nvarchar**|Nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo rastreada.|26|Não|  
|**SessionLoginName**|**nvarchar**|Nome de logon do usuário que originou a sessão. Por exemplo, para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o Logon1 e executar uma instrução como Logon2, o **SessionLoginName** mostrará o Logon1 e o **LoginName** mostrará o Logon2. Essa coluna exibe logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do Windows.|64|Sim|  
|**SPID**|**int**|Identificação da sessão em que ocorreu o evento.|12|Sim|  
|**StartTime**|**datetime**|Hora de início do evento, se disponível.|14|Sim|  
|**TransactionID**|**bigint**|ID da transação atribuída pelo sistema.|4|Sim|  
|**XactSequence**|**bigint**|Token que descreve a transação atual.|50|Sim|  
  
## <a name="see-also"></a>Consulte Também  
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Opções Set Index](../../relational-databases/indexes/set-index-options.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
  
