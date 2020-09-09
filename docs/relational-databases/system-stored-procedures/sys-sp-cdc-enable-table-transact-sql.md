---
description: sys.sp_cdc_enable_table (Transact-SQL)
title: sys. sp_cdc_enable_table (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_enable_table_TSQL
- sp_cdc_enable_table_TSQL
- sys.sp_cdc_enable_table
- sp_cdc_enable_table
dev_langs:
- TSQL
helpviewer_keywords:
- change data capture [SQL Server], enabling tables
- sys.sp_cdc_enable_table
- sp_cdc_enable_table
ms.assetid: 26150c09-2dca-46ad-bb01-3cb3165bcc5d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5832381bab59aff32c039d4f26b648c62802d5d1
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89541088"
---
# <a name="syssp_cdc_enable_table-transact-sql"></a>sys.sp_cdc_enable_table (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Habilita o Change Data Capture para a tabela de origem especificada no banco de dados atual. Quando uma tabela está habilitada para Change Data Capture, um registro de cada operação DML (Linguagem de Manipulação de Dados) aplicado à tabela é gravado no log de transações. O processo do Change Data Capture recupera essas informações a partir do log e grava-as nas tabelas de alteração que são acessadas usando um conjunto de funções.  
  
 A captura de dados de alteração não está disponível em todas as edições do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.sp_cdc_enable_table   
  [ @source_schema = ] 'source_schema',   
  [ @source_name = ] 'source_name' ,  [,[ @capture_instance = ] 'capture_instance' ]  
  [,[ @supports_net_changes = ] supports_net_changes ]  
  , [ @role_name = ] 'role_name'  
  [,[ @index_name = ] 'index_name' ]  
  [,[ @captured_column_list = ] 'captured_column_list' ]  
  [,[ @filegroup_name = ] 'filegroup_name' ]  
  [,[ @allow_partition_switch = ] 'allow_partition_switch' ]  
  [;]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @source_schema = ] 'source_schema'` É o nome do esquema ao qual a tabela de origem pertence. *source_schema* é **sysname**, sem padrão, e não pode ser nulo.  
  
`[ @source_name = ] 'source_name'` É o nome da tabela de origem na qual habilitar a captura de dados de alterações. *source_name* é **sysname**, sem padrão, e não pode ser nulo.  
  
 *source_name* deve existir no banco de dados atual. As tabelas no esquema **CDC** não podem ser habilitadas para a captura de dados de alterações.  
  
`[ @role_name = ] 'role_name'` É o nome da função de banco de dados usada para o acesso à porta de entrada. *role_name* é **sysname** e deve ser especificado. Se explicitamente definido como NULL, nenhuma função associada será usada para limitar o acesso aos dados de alteração.  
  
 Se a função existir atualmente, ela será usada. Se a função não existir, será feita uma tentativa de criar uma função de banco de dados com o nome especificado. Os espaços em branco do nome da função à direita da cadeia de caracteres são eliminados antes de tentar criar a função. Se o chamador não for autorizado a criar uma função dentro do banco de dados, a operação de procedimento armazenado irá falhar.  
  
`[ @capture_instance = ] 'capture_instance'` É o nome da instância de captura usada para nomear objetos de captura de dados de alteração específicos da instância. *capture_instance* é **sysname** e não pode ser nulo.  
  
 Se não for especificado, o nome será derivado do nome do esquema de origem mais o nome da tabela de origem no formato *schemaname_sourcename*. *capture_instance* não pode exceder 100 caracteres e deve ser exclusivo no banco de dados. Seja especificado ou derivado, *capture_instance* é cortado de qualquer espaço em branco à direita da cadeia de caracteres.  
  
 Uma tabela de origem pode ter um máximo de duas instâncias de captura. Para obter mais informações, consulte [Sys. sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md).  
  
`[ @supports_net_changes = ] supports_net_changes` Indica se o suporte para consulta de alterações líquidas deve ser habilitado para esta instância de captura. *supports_net_changes* é **bit** com um padrão de 1 se a tabela tiver uma chave primária ou se a tabela tiver um índice exclusivo que foi identificado usando o @index_name parâmetro. Caso contrário, o parâmetro será padronizado como 0.  
  
 Se for 0, somente as funções de suporte à consulta de todas as alterações serão geradas.  
  
 Se for 1, as funções necessárias à consulta de alterações líquidas também serão geradas.  
  
 Se *supports_net_changes* for definido como 1, *index_name* deverá ser especificado ou a tabela de origem deverá ter uma chave primária definida.  
  
`[ @index_name = ] 'index_name_'` O nome de um índice exclusivo a ser usado para identificar exclusivamente as linhas na tabela de origem. *index_name* é **sysname** e pode ser nulo. Se especificado, *index_name* deve ser um índice exclusivo válido na tabela de origem. Se *index_name* for especificado, as colunas de índice identificadas têm precedência sobre quaisquer colunas de chave primária definidas como o identificador de linha exclusivo para a tabela.  
  
`[ @captured_column_list = ] 'captured_column_list'` Identifica as colunas da tabela de origem que devem ser incluídas na tabela de alteração. *captured_column_list* é **nvarchar (max)** e pode ser NULL. Se for NULL, todas as colunas serão incluídas na tabela de alteração.  
  
 Nomes de Coluna devem ser colunas válidas na tabela de origem. As colunas definidas em um índice de chave primária ou colunas definidas em um índice referenciado por *index_name* devem ser incluídas.  
  
 *captured_column_list* é uma lista separada por vírgulas de nomes de coluna. Nomes de colunas individuais na lista podem ser citados opcionalmente usando aspas duplas ("") ou colchetes ([]). Se um nome de coluna contiver uma vírgula inserida, o nome de coluna deve ser citado.  
  
 o *captured_column_list* não pode conter os seguintes nomes de coluna reservados: **_ de US $ start_lsn**, **_ _ $ end_lsn**, **_ $ seqval**, **_ $ operation $** e **_ $ update_mask**.  
  
`[ @filegroup_name = ] 'filegroup_name'` É o grupo de arquivos a ser usado para a tabela de alteração criada para a instância de captura. *filegroup_name* é **sysname** e pode ser nulo. Se especificado, *filegroup_name* deve ser definido para o banco de dados atual. Se for NULL, o grupo de arquivos padrão será usado.  
  
 Recomendamos a criação de um grupo de arquivos separado para tabelas de alteração do Change Data Capture.  
  
`[ @allow_partition_switch = ] 'allow_partition_switch'` Indica se o comando SWITCH PARTITION de ALTER TABLE pode ser executado em uma tabela habilitada para a captura de dados de alterações. *allow_partition_switch* é **bit**, com um padrão de 1.  
  
 Para tabelas não particionadas, a configuração de alternância é sempre 1 e a configuração real é ignorada. Se a alternância estiver explicitamente definida como 0 para uma tabela não particionada, o aviso 22857 será emitido para indicar que a configuração de alternância foi ignorada. Se a alternância estiver explicitamente definida como 0 para uma tabela particionada, o aviso 22356 será emitido para indicar que as operações de alternância da partição na tabela de origem não serão permitidas. Finalmente, se a configuração de alternância estiver explicitamente definida como 1 ou permitida para ser padronizada como 1 e a tabela habilitada estiver particionada, o aviso 22855 será emitido para indicar que as alternâncias de partição não serão bloqueadas. Se ocorrer qualquer alternância de partição, o Change Data Capture não controlará as alterações resultantes da alternância. Isso provocará inconsistências de dados quando os dados de alteração forem consumidos.  
  
> [!IMPORTANT]  
>  SWITCH PARTITION é uma operação de metadados, mas provoca alterações nos dados. As alterações de dados associadas a essa operação não são capturadas nas tabelas de alteração do Change Data Capture. Considere uma tabela com três partições em que são feitas alterações. O processo de captura rastreará operações de inserção, atualização e exclusão de usuário que são executadas na tabela. Entretanto, se uma partição for alternada para outra tabela (por exemplo, para executar uma exclusão em massa), as linhas movidas como parte dessa operação não serão capturadas como linhas excluídas na tabela de alteração. Da mesma forma, se uma nova partição com linhas previamente populadas for adicionada à tabela, essas linhas não constarão na tabela de alteração. Isso pode causar inconsistência de dados quando as alterações forem consumidas por um aplicativo e aplicadas a um destino.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Antes de habilitar uma tabela para Change Data Capture, o banco de dados deve estar habilitado. Para determinar se o banco de dados está habilitado para o Change Data Capture, consulte a coluna **is_cdc_enabled** na exibição do catálogo [Sys. databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) . Para habilitar o banco de dados, use o procedimento armazenado [Sys. sp_cdc_enable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md) .  
  
 Quando o Change Data Capture está habilitado para uma tabela, uma tabela de alteração e uma ou duas funções de consulta são geradas. A tabela de alteração serve como um repositório para as alterações da tabela de origem extraídas do log de transações pelo processo de captura. As funções de consulta são usadas para extrair dados da tabela de alteração. Os nomes dessas funções são derivados do parâmetro *capture_instance* das seguintes maneiras:  
  
-   Todas as alterações funcionam: **CDC. fn_cdc_get_all_changes_<capture_instance>**  
  
-   Função de alterações líquidas: **CDC. fn_cdc_get_net_changes_<capture_instance>**  
  
 o **Sys. sp_cdc_enable_table** também criará os trabalhos de captura e limpeza para o banco de dados se a tabela de origem for a primeira tabela no banco de dado a ser habilitada para o Change Data Capture e não existirem publicações transacionais para o Database. Ele define a coluna **is_tracked_by_cdc** na exibição de catálogo [Sys. Tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) como 1.  
  
> [!NOTE]  
>  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não precisa estar em execução quando o Change Data Capture estiver habilitado para uma tabela. No entanto o processo de captura não processará o log de transações e não gravará as entradas na tabela de alteração, a não ser que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent esteja em execução.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa **db_owner** .  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-enabling-change-data-capture-by-specifying-only-required-parameters"></a>a. Habilitando o Change Data Capture especificando somente os parâmetros necessários  
 O exemplo a seguir habilita o Change Data Capture na tabela `HumanResources.Employee`. Somente os parâmetros necessários são especificados.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_enable_table  
    @source_schema = N'HumanResources'  
  , @source_name = N'Employee'  
  , @role_name = N'cdc_Admin';  
GO  
```  
  
### <a name="b-enabling-change-data-capture-by-specifying-additional-optional-parameters"></a>B. Habilitando o Change Data Capture especificando parâmetros opcionais adicionais  
 O exemplo a seguir habilita o Change Data Capture na tabela `HumanResources.Department`. Todos os parâmetros, exceto o `@allow_partition_switch` são especificados.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_enable_table  
    @source_schema = N'HumanResources'  
  , @source_name = N'Department'  
  , @role_name = N'cdc_admin'  
  , @capture_instance = N'HR_Department'   
  , @supports_net_changes = 1  
  , @index_name = N'AK_Department_Name'   
  , @captured_column_list = N'DepartmentID, Name, GroupName'   
  , @filegroup_name = N'PRIMARY';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys. sp_cdc_disable_table &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-table-transact-sql.md)   
 [sys. sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [CDC. fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [CDC. fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [sys. sp_cdc_help_jobs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)  
  
  
