---
title: sys. dm_exec_query_statistics_xml (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_query_statistics_xml
- sys.dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml_TSQL
- dm_exec_query_statistics_xml
helpviewer_keywords:
- sys.dm_exec_query_statistics_xml management view
ms.assetid: fdc7659e-df41-488e-b2b5-0d79734dfecb
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 6304e6381b9bbfcc17b218122631d06293e15830
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734709"
---
# <a name="sysdm_exec_query_statistics_xml-transact-sql"></a>sys. dm_exec_query_statistics_xml (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi-asdw](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asdw.md)]

Retorna o plano de execução de consulta para solicitações em andamento. Use essa DMV para recuperar o Showplan XML com estatísticas transitórias. 

## <a name="syntax"></a>Sintaxe

```
sys.dm_exec_query_statistics_xml(session_id)  
``` 

## <a name="arguments"></a>Argumentos 
*session_id*  
 É a ID da sessão que executa o lote a ser pesquisado. *session_id* é **smallint**. *session_id* pode ser obtido dos seguintes objetos de gerenciamento dinâmico:  
  
-   [sys.dm_exec_requests](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
-   [sys.dm_exec_sessions](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
-   [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md)  

## <a name="table-returned"></a>Tabela retornada

|Nome da coluna|Tipo de Dados|Descrição|  
|-----------------|---------------|-----------------|
|session_id|**smallint**|ID da sessão. Não permite valor nulo.|
|request_id|**int**|ID da solicitação. Não permite valor nulo.|
|sql_handle|**varbinary(64)**|É um token que identifica exclusivamente o lote ou o procedimento armazenado do qual a consulta faz parte. Anulável.|
|plan_handle|**varbinary(64)**|É um token que identifica exclusivamente um plano de execução de consulta para um lote em execução no momento. Anulável.|
|query_plan|**xml**|Contém a representação Showplan do tempo de execução do plano de execução de consulta especificado com *plan_handle* que contém estatísticas parciais. O Showplan está em formato XML. Um plano é gerado para cada lote que contém, por exemplo, instruções ad hoc [!INCLUDE[tsql](../../includes/tsql-md.md)], chamadas de procedimento armazenado e chamadas de função definidas pelo usuário. Anulável.|

## <a name="remarks"></a>Comentários
Essa função do sistema está disponível a partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1. Consulte KB [3190871](https://support.microsoft.com/help/3190871)

Essa função do sistema funciona em uma infraestrutura de criação de perfil de estatísticas de execução de consulta **leves** e **Standard** . Para obter mais informações, consulte [consultar a infraestrutura de criação de perfil](../../relational-databases/performance/query-profiling-infrastructure.md).  

Sob as condições a seguir, nenhuma saída SHOWPLAN é retornada na coluna **query_plan** da tabela retornada para **Sys. dm_exec_query_statistics_xml**:  
  
-   Se o plano de consulta que corresponde ao *session_id* especificado não estiver mais sendo executado, a coluna **query_plan** da tabela retornada será nula. Por exemplo, essa condição pode ocorrer se houver um atraso de tempo entre o momento em que o identificador de plano foi capturado e quando ele foi usado com **Sys. dm_exec_query_statistics_xml**.  
    
Devido a uma limitação no número de níveis aninhados permitido no tipo de dados **XML** , **Sys. dm_exec_query_statistics_xml** não pode retornar planos de consulta que atendam ou ultrapassem 128 níveis de elementos aninhados. Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta condição evitava que o plano de consulta retornasse e gerasse um erro 6335. No [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2 e versões posteriores, a coluna **QUERY_PLAN** retorna NULL.   

## <a name="permissions"></a>Permissões  
Ativado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , requer `VIEW SERVER STATE` permissão no servidor.  
Nas [!INCLUDE[ssSDS](../../includes/sssds-md.md)] camadas Premium, o requer a `VIEW DATABASE STATE` permissão no banco de dados. Nas [!INCLUDE[ssSDS](../../includes/sssds-md.md)] camadas Standard e Basic, o requer o **administrador do servidor** ou uma conta de **administrador do Azure Active Directory** .

## <a name="examples"></a>Exemplos  
  
### <a name="a-looking-at-live-query-plan-and-execution-statistics-for-a-running-batch"></a>a. Examinando o plano de consulta ao vivo e as estatísticas de execução de um lote em execução  
 O exemplo a seguir consulta **Sys. dm_exec_requests** para localizar a consulta interessante e copiar sua `session_id` da saída.  
  
```sql  
SELECT * FROM sys.dm_exec_requests;  
GO  
```  
  
 Em seguida, para obter o plano de consulta ao vivo e as estatísticas de execução, use a `session_id` função de sistema Copie com **sys. dm_exec_query_statistics_xml**.  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_query_statistics_xml(< copied session_id >);  
GO  
```   

 Ou combinados a todas as solicitações em execução.  
  
```sql  
--Run this in a different session than the session in which your query is running.
SELECT * FROM sys.dm_exec_requests
CROSS APPLY sys.dm_exec_query_statistics_xml(session_id);  
GO  
```   
  
## <a name="see-also"></a>Consulte Também
  [Sinalizadores de rastreamento](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)  
 [Funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Exibições de gerenciamento dinâmico relacionadas ao banco de dados &#40;&#41;Transact-SQL](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

