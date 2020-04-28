---
title: sp_stored_procedures (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_stored_procedures_TSQL
- sp_stored_procedures
dev_langs:
- TSQL
helpviewer_keywords:
- sp_stored_procedures
ms.assetid: fe52dd83-000a-4665-83fb-7a0024193dec
author: stevestein
ms.author: sstein
ms.openlocfilehash: 554b9317d6b474b23e9dbbc10dea03156ccc6287
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68702784"
---
# <a name="sp_stored_procedures-transact-sql"></a>sp_stored_procedures (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma lista de procedimentos armazenados do ambiente atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_stored_procedures [ [ @sp_name = ] 'name' ]   
    [ , [ @sp_owner = ] 'schema']   
    [ , [ @sp_qualifier = ] 'qualifier' ]  
    [ , [@fUsePattern = ] 'fUsePattern' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @sp_name = ] 'name'`É o nome do procedimento usado para retornar informações do catálogo. o *nome* é **nvarchar (390)**, com um padrão de NULL. Há suporte para a correspondência do padrão curinga.  
  
`[ @sp_owner = ] 'schema'`É o nome do esquema ao qual o procedimento pertence. o *esquema* é **nvarchar (384)**, com um padrão de NULL. Há suporte para a correspondência do padrão curinga. Se o *proprietário* não for especificado, as regras de visibilidade de procedimento padrão do DBMS subjacente se aplicarão.  
  
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se o esquema atual contiver um procedimento com o nome especificado, será retornado esse procedimento. Se um procedimento armazenado não qualificado for especificado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] procurará o procedimento na ordem seguinte:  
  
-   Esquema **sys** do banco de dados atual.  
  
-   O esquema padrão do chamador se executado em um lote ou em um SQL dinâmico; ou, se o nome do procedimento não qualificado aparecer no corpo da definição de outro procedimento, o esquema que contém esse outro procedimento é o próximo a ser pesquisado.  
  
-   O esquema **dbo** no banco de dados atual.  
  
`[ @qualifier = ] 'qualifier'`É o nome do qualificador de procedimento. o *qualificador* é **sysname**, com um padrão de NULL. Vários produtos DBMS dão suporte à nomeação de três partes para tabelas no formulário (_qualificador_**.** _esquema_**.** _nome_. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o *qualificador* representa o nome do banco de dados. Em alguns produtos, representa o nome do servidor do ambiente de banco de dados da tabela.  
  
`[ @fUsePattern = ] 'fUsePattern'`Determina se o sublinhado (_), percentual (%) ou colchetes []) é interpretado como caracteres curinga. *fUsePattern* é **bit**, com um padrão de 1.  
  
 **0** = a correspondência de padrões está desativada.  
  
 **1** = a correspondência de padrões está ativada.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**PROCEDURE_QUALIFIER**|**sysname**|Nome do qualificador de procedimento. Esta coluna pode ser NULL.|  
|**PROCEDURE_OWNER**|**sysname**|Nome do proprietário do procedimento. Esta coluna sempre retorna um valor.|  
|**PROCEDURE_NAME**|**nvarchar (134)**|Nome do procedimento. Esta coluna sempre retorna um valor.|  
|**NUM_INPUT_PARAMS**|**int**|Reservado para uso futuro.|  
|**NUM_OUTPUT_PARAMS**|**int**|Reservado para uso futuro.|  
|**NUM_RESULT_SETS**|**int**|Reservado para uso futuro.|  
|**COMENTÁRIOS**|**varchar (254)**|Descrição do procedimento. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não retorna um valor para essa coluna.|  
|**PROCEDURE_TYPE**|**smallint**|Tipo do procedimento. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre retorna 2.0. Este valor pode ser um dos seguintes:<br /><br /> 0 = SQL_PT_UNKNOWN<br /><br /> 1 = SQL_PT_PROCEDURE<br /><br /> 2 = SQL_PT_FUNCTION|  
  
## <a name="remarks"></a>Comentários  
 Para obter interoperabilidade máxima, o cliente de gateway deve supor apenas a correspondência de padrões SQL padrão (os caracteres curinga porcentagem % e sublinhado_).  
  
 As informações de permissão relacionadas ao acesso para execução a um determinado procedimento para o usuário atual não são necessariamente confirmadas; portanto, o acesso não é autorizado. Observe que somente o nome de três partes é utilizado. Em outras palavras, somente os procedimentos armazenados locais, e não os procedimentos armazenados remotos (que requerem nome de quatro partes), são retornados quando executados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o atributo de servidor ACCESSIBLE_SPROC for Y no conjunto de resultados para **sp_server_info**, somente os procedimentos armazenados que podem ser executados pelo usuário atual serão retornados.  
  
 **sp_stored_procedures** é equivalente a **SQLProcedures** em ODBC. Os resultados retornados são ordenados por **PROCEDURE_QUALIFIER**, **PROCEDURE_OWNER**e **procedure_name**.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão SELECT no esquema.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-returning-all-stored-procedures-in-the-current-database"></a>a. Retornando todos os procedimentos armazenados no banco de dados atual  
 O exemplo a seguir retorna todos os procedimentos armazenados no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_stored_procedures;  
```  
  
### <a name="b-returning-a-single-stored-procedure"></a>B. Retornando um único procedimento armazenado  
 O exemplo a seguir retorna um conjunto de resultados do procedimento armazenado `uspLogError`.  
  
```  
USE AdventureWorks2012;  
GO  
sp_stored_procedures N'uspLogError', N'dbo', N'AdventureWorks2012', 1;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
