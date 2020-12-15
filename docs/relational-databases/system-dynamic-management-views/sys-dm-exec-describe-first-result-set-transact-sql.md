---
title: sys.dm_exec_describe_first_result_set (Transact-SQL)
description: sys.dm_exec_describe_first_result_set (Transact-SQL)
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_describe_first_result_set
- sys.dm_exec_describe_first_result_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_describe_first_result_set catalog view
ms.assetid: 6ea88346-0bdb-4f0e-9f1f-4d85e3487d23
author: markingmyname
ms.author: maghan
ms.custom: ''
ms.date: 06/10/2016
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 21b823aeaa319263a3e90a3ddd917e9605506c0c
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472857"
---
# <a name="sysdm_exec_describe_first_result_set-transact-sql"></a>sys.dm_exec_describe_first_result_set (Transact-SQL)

[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

Essa função de gerenciamento dinâmico usa uma [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução como um parâmetro e descreve os metadados do primeiro conjunto de resultados para a instrução.  
  
 **Sys.dm_exec_describe_first_result_set** tem a mesma definição de conjunto de resultados que [Sys.dm_exec_describe_first_result_set_for_object &#40;&#41;do Transact-SQL](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md) e é semelhante a sp_describe_first_result_set &#40;o [Transact-SQL](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)&#41;.  
  

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.dm_exec_describe_first_result_set(@tsql, @params, @include_browse_information)  
```  
  
## <a name="arguments"></a>Argumentos  
 *\@TSQL*  
 Uma ou mais instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. O *Transact-SQL_batch* pode **ser nvarchar (**_n_*_)_* ou **nvarchar (max)**.  
  
 *\@params*  
 \@params fornece uma cadeia de caracteres de declaração para parâmetros para o [!INCLUDE[tsql](../../includes/tsql-md.md)] lote, semelhante a sp_executesql. Os parâmetros podem ser **nvarchar (n)** ou **nvarchar (max)**.  
  
 É uma cadeia de caracteres que contém as definições de todos os parâmetros que foram inseridos na [!INCLUDE[tsql](../../includes/tsql-md.md)] *_batch*. A cadeia de caracteres deve ser uma constante Unicode ou uma variável Unicode. Cada definição de parâmetro consiste em um nome de parâmetro e um tipo de dados. *n* é um espaço reservado que indica definições de parâmetros adicionais. Todos os parâmetros especificados em stmt devem ser definidos em \@ params. Se a [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução ou o lote na instrução não contiver parâmetros, \@ params não será necessário. O valor padrão para este parâmetro é NULL.  
  
 *\@include_browse_information*  
 Se definido como 1, cada consulta será analisada como se tivesse uma opção FOR BROWSE na consulta. Colunas de chave adicionais e informações de tabela de origem são retornadas.  
  
## <a name="table-returned"></a>Tabela retornada  
 Esses metadados comuns são retornados como um conjunto de resultados. Uma linha para cada coluna nos metadados de resultados descreve o tipo e a nulidade da coluna no formato mostrado na tabela a seguir. Se a primeira instrução não existir para todo caminho de controle, um conjunto de resultados com zero linhas será retornado.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**is_hidden**|**bit**|Especifica que a coluna é uma coluna extra adicionada para fins de informações de navegação e que ela não é exibida realmente no conjunto de resultados.|  
|**column_ordinal**|**int**|Contém a posição ordinal da coluna no conjunto de resultados. A posição da primeira coluna será especificada como 1.|  
|**name**|**sysname**|Conterá o nome da coluna se um nome puder ser determinado. Se não, conterá NULL.|  
|**is_nullable**|**bit**|Contém os seguintes valores:<br /><br /> Valor 1 se a coluna permitir NULLs.<br /><br /> Valor 0 se a coluna não permitir NULLs.<br /><br /> Valor 1 se não for possível determinar se a coluna permite NULLs.|  
|**system_type_id**|**int**|Contém a system_type_id do tipo de dados de coluna conforme especificado em sys. Types. Para tipos de CLR, embora a coluna system_type_name retorne NULL, essa coluna retornará o valor 240.|  
|**system_type_name**|**nvarchar(256)**|Contém o nome e argumentos (como comprimento, precisão, escala), especificados para o tipo de dados da coluna.<br /><br /> Se o tipo de dados for um tipo de alias definido pelo usuário, o tipo de sistema subjacente será especificado aqui.<br /><br /> Se o tipo de dados for um tipo CLR definido pelo usuário, NULL será retornado nessa coluna.|  
|**max_length**|**smallint**|Comprimento máximo (em bytes) da coluna.<br /><br /> -1 = o tipo de dados da coluna é **varchar (max)**, **nvarchar (max)**, **varbinary (max)** ou **XML**.<br /><br /> Para colunas de **texto** , o valor de **max_length** será 16 ou o valor definido por **sp_tableoption ' texto na linha '**.|  
|**precisão**|**tinyint**|Precisão da coluna, se tiver base numérica. Caso contrário, retorna 0.|  
|**scale**|**tinyint**|Escala da coluna, se tiver base numérica. Caso contrário, retorna 0.|  
|**collation_name**|**sysname**|Nome da ordenação da coluna, se baseada em caracteres. Caso contrário, retorna NULL.|  
|**user_type_id**|**int**|Para tipos de CLR e alias, contém o user_type_id do tipo de dados da coluna como especificado em sys.types. Caso contrário, é NULL.|  
|**user_type_database**|**sysname**|Para tipos de CLR e de alias, contém o nome do banco de dados no qual o tipo é definido. Caso contrário, é NULL.|  
|**user_type_schema**|**sysname**|Para tipos de CLR e de alias, contém o nome do esquema no qual o tipo é definido. Caso contrário, é NULL.|  
|**user_type_name**|**sysname**|Para tipos de CLR e de alias, contém o nome do tipo. Caso contrário, é NULL.|  
|**assembly_qualified_type_name**|**nvarchar(4000)**|Para tipos de CLR, retorna o nome do assembly e da classe que define o tipo. Caso contrário, é NULL.|  
|**xml_collection_id**|**int**|Contém o xml_collection_id do tipo de dados da coluna como especificado em sys.columns. Essa coluna retornará NULL se o tipo retornado não estiver associado a uma coleção de esquemas XML.|  
|**xml_collection_database**|**sysname**|Contém o banco de dados no qual a coleção de esquemas XML associada a esse tipo está definida. Essa coluna retornará NULL se o tipo retornado não estiver associado a uma coleção de esquemas XML.|  
|**xml_collection_schema**|**sysname**|Contém o esquema no qual a coleção de esquemas XML associada a esse tipo está definida. Essa coluna retornará NULL se o tipo retornado não estiver associado a uma coleção de esquemas XML.|  
|**xml_collection_name**|**sysname**|Contém o nome da coleção de esquemas XML associada a esse tipo. Essa coluna retornará NULL se o tipo retornado não estiver associado a uma coleção de esquemas XML.|  
|**is_xml_document**|**bit**|Retornará 1 se o tipo de dados retornado for o XML e esse tipo for garantido de ser um documento XML completo (incluindo um nó raiz), em vez de um fragmento XML. Caso contrário, retorna 0.|  
|**is_case_sensitive**|**bit**|Retornará 1 se a coluna for um tipo de cadeia de caracteres com diferenciação de maiúsculas e minúsculas. Retornará 0 se não estiver.|  
|**is_fixed_length_clr_type**|**bit**|Retornará 1 se a coluna for de um tipo de CLR de comprimento fixo. Retornará 0 se não estiver.|  
|**source_server**|**sysname**|Nome do servidor de origem (se for originado de um servidor remoto). O nome é fornecido como aparece em sys. Servers. Retornará NULL se a coluna tiver origem no servidor local ou caso não seja possível determinar o servidor de origem. Será populado somente se informações de navegação forem solicitadas.|  
|**source_database**|**sysname**|Nome do banco de dados de origem retornado pela coluna neste resultado. Retornará NULL se o banco de dados não puder ser determinado. Será populado somente se informações de navegação forem solicitadas.|  
|**source_schema**|**sysname**|Nome do esquema de origem retornado pela coluna neste resultado. Retornará NULL se o esquema não puder ser determinado. Será populado somente se informações de navegação forem solicitadas.|  
|**source_table**|**sysname**|Nome da tabela de origem retornado pela coluna neste resultado. Retornará NULL se a tabela não puder ser determinada. Será populado somente se informações de navegação forem solicitadas.|  
|**source_column**|**sysname**|Nome da coluna de origem retornado pela coluna de resultado. Retornará NULL se a coluna não puder ser determinada. Será populado somente se informações de navegação forem solicitadas.|  
|**is_identity_column**|**bit**|Retornará 1 se a coluna for uma coluna de identidade; caso contrário, retornará 0. Retornará NULL caso não seja possível determinar se a coluna é uma coluna de identidade.|  
|**is_part_of_unique_key**|**bit**|Retornará 1 se a coluna fizer parte de um índice exclusivo (incluindo as restrições exclusivas e primárias); caso contrário, retornará 0. Retornará NULL caso não seja possível determinar se a coluna faz parte de um índice exclusivo. Será populado somente se informações de navegação forem solicitadas.|  
|**is_updateable**|**bit**|Retornará 1 se a coluna for uma coluna atualizável; caso contrário, retornará 0. Retornará NULL caso não seja possível determinar se a coluna é atualizável.|  
|**is_computed_column**|**bit**|Retornará 1 se a coluna for uma coluna computada; caso contrário, retornará 0. Retornará NULL caso não seja possível determinar se a coluna é uma coluna computada.|  
|**is_sparse_column_set**|**bit**|Retornará 1 se a coluna for uma coluna esparsa; caso contrário, retornará 0. Retornará NULL caso não seja possível determinar se a coluna faz parte de um conjunto de colunas esparsas.|  
|**ordinal_in_order_by_list**|**smallint**|A posição desta coluna na lista ORDER BY. Retornará o NULL se a coluna não for exibida na lista ORDER BY ou se a lista ORDER BY não puder ser determinada exclusivamente.|  
|**order_by_list_length**|**smallint**|O comprimento da lista ORDER BY. Retornará NULL se não houver uma lista ORDER BY ou se a lista ORDER BY não puder ser determinada exclusivamente. Observe que este valor será o mesmo para todas as linhas retornadas por sp_describe_first_result_set.|  
|**order_by_is_descending**|**NULO smallint**|Se o ordinal_in_order_by_list não for NULL, a coluna **order_by_is_descending** relatará a direção da cláusula ORDER BY para esta coluna. Caso contrário, relatará NULL.|  
|**error_number**|**int**|Contém o número do erro retornado pela função. Se nenhum erro ocorreu, a coluna conterá NULL.|  
|**error_severity**|**int**|Contém a severidade do erro retornado pela função. Se nenhum erro ocorreu, a coluna conterá NULL.|  
|**error_state**|**int**|Contém a mensagem de estado. retornada pela função. Se nenhum erro ocorreu, a coluna conterá NULL.|  
|**error_message**|**nvarchar (4096)**|Contém a mensagem retornada pela função. Se nenhum erro ocorreu, a coluna conterá NULL.|  
|**error_type**|**int**|Contém um inteiro que representa o erro que é retornado. Mapeia para error_type_desc. Consulte a lista sob comentários.|  
|**error_type_desc**|**nvarchar(60)**|Contém uma pequena cadeia de caracteres maiúsculos que representa o erro sendo retornado. Mapeia para error_type. Consulte a lista sob comentários.|  
  
## <a name="remarks"></a>Comentários  
 Esta função usa o mesmo algoritmo como **sp_describe_first_result_set**. Para obter mais informações, consulte [sp_describe_first_result_set &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md).  
  
 A tabela a seguir lista os tipos de erros e suas descrições  
  
|error_type|error_type|Descrição|  
|-----------------|-----------------|-----------------|  
|1|MISC|Todos os erros que não são descritos de outra forma.|  
|2|SYNTAX|Um erro de sintaxe ocorreu no lote.|  
|3|CONFLICTING_RESULTS|O resultado não pôde ser determinado devido a um conflito entre duas primeiras instruções possíveis.|  
|4|DYNAMIC_SQL|O resultado não pôde ser determinado devido a um SQL dinâmico que poderia retornar o primeiro resultado.|  
|5|CLR_PROCEDURE|O resultado não pôde ser determinado devido a um procedimento armazenado de CLR que poderia retornar o primeiro resultado.|  
|6|CLR_TRIGGER|O resultado não pôde ser determinado devido a um gatilho CLR que poderia retornar o primeiro resultado.|  
|7|EXTENDED_PROCEDURE|O resultado não pôde ser determinado devido a um procedimento armazenado estendido que poderia retornar o primeiro resultado.|  
|8|UNDECLARED_PARAMETER|O resultado não pôde ser determinado porque o tipo de dados de uma ou mais das colunas do conjunto de resultados pode depender de um parâmetro não declarado.|  
|9|RECURSION|O resultado não pôde ser determinado porque o lote contém uma instrução recursiva.|  
|10|TEMPORARY_TABLE|O resultado não pôde ser determinado porque o lote contém uma tabela temporária e não tem suporte de **sp_describe_first_result_set**.|  
|11|UNSUPPORTED_STATEMENT|O resultado não pôde ser determinado porque o lote contém uma instrução sem suporte de **sp_describe_first_result_set** (por exemplo, FETCH, REVERT, etc.).|  
|12|OBJECT_TYPE_NOT_SUPPORTED|O \@ object_id passado para a função não tem suporte (ou seja, não é um procedimento armazenado)|  
|13|OBJECT_DOES_NOT_EXIST|O \@ object_id passado para a função não foi encontrado no catálogo do sistema.|  
  
## <a name="permissions"></a>Permissões  
 Requer permissão para executar o \@ argumento TSQL.  
  
## <a name="examples"></a>Exemplos  
 Exemplos adicionais no tópico [sp_describe_first_result_set &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md) podem ser adaptados para usar **Sys.dm_exec_describe_first_result_set**.  
  
### <a name="a-returning-information-about-a-single-transact-sql-statement"></a>a. Retornando informações sobre uma única instrução Transact-SQL  
 O código a seguir retorna informações sobre os resultados de uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_exec_describe_first_result_set  
(N'SELECT object_id, name, type_desc FROM sys.indexes', null, 0) ;  
```  
  
### <a name="b-returning-information-about-a-procedure"></a>B. Retornando informações sobre um procedimento  
 O exemplo a seguir cria um procedimento armazenado chamado pr_TestProc que retorna dois conjuntos de resultados. Em seguida, o exemplo demonstra que **sys.dm_exec_describe_first_result_set** retorna informações sobre o primeiro conjunto de resultados no procedimento.  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE PROC Production.TestProc  
AS  
SELECT Name, ProductID, Color FROM Production.Product ;  
SELECT Name, SafetyStockLevel, SellStartDate FROM Production.Product ;  
GO  
  
SELECT * FROM sys.dm_exec_describe_first_result_set  
('Production.TestProc', NULL, 0) ;  
```  
  
### <a name="c-returning-metadata-from-a-batch-that-contains-multiple-statements"></a>C. Retornando metadados de um lote que contém várias instruções  
 O exemplo a seguir avalia um lote que contém duas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)]. O conjunto de resultados descreve o primeiro conjunto de resultados retornado.  
  
```  
USE AdventureWorks2012;  
GO  
  
SELECT * FROM sys.dm_exec_describe_first_result_set(  
N'SELECT CustomerID, TerritoryID, AccountNumber FROM Sales.Customer WHERE CustomerID = @CustomerID;  
SELECT * FROM Sales.SalesOrderHeader;',  
N'@CustomerID int', 0) AS a;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_describe_first_result_set ](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_describe_undeclared_parameters ](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sys.dm_exec_describe_first_result_set_for_object ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md)  
  
  
