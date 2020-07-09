---
title: DBCC CLONEDATABASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CLONEDATABASE
- CLONE DATABASE
- DBCC_CLONEDATABASE_TSQL
- DBCC CLONEDATABASE
- DBCC CLONE DATABASE
- CLONEDATABASE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database cloning [SQL Server]
- cloning databases
- clone databases
- cloning database
- clone database
- copying databases
- copy databases
- copying database
- copy database
- NO_STATISTICS option
- NO_QUERYSTORE option
- VERIFY_CLONEDB option
- BACKUP_CLONEDB option
- database copying [SQL Server]
- database cloning [SQL Server]
- DBCC CLONEDATABASE statement
ms.assetid: ''
author: bluefooted
ms.author: pamela
manager: amitban
ms.openlocfilehash: 2f1214064c11537f4752f9ec824123c3d601a1c4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730736"
---
# <a name="dbcc-clonedatabase-transact-sql"></a>DBCC CLONEDATABASE (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Gera um clone somente de esquema de um banco de dados usando DBCC CLONEDATABASE para investigar problemas de desempenho relacionados ao otimizador de consulta.

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
DBCC CLONEDATABASE   
(  
    source_database_name
    ,  target_database_name
)
    [ WITH { [ NO_STATISTICS ] [ , NO_QUERYSTORE ] [ , VERIFY_CLONEDB | SERVICEBROKER ] [ , BACKUP_CLONEDB ] } ]     
```  
  
## <a name="arguments"></a>Argumentos  
*source_database_name*  
É o nome do banco de dados a ser copiado. 
  
*target_database_name*  
É o nome do banco de dados para o qual o banco de dados de origem será copiado. Este banco de dados será criado por DBCC CLONEDATABASE e não deve existir. 
  
NO_STATISTICS  
Especifica se as estatísticas de tabela/índice precisam ser excluídas do clone. Se essa opção não for especificada, as estatísticas de tabela/índice serão incluídas automaticamente. Essa opção está disponível desde o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 CU3 e o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1.

NO_QUERYSTORE<br>
Especifica se os dados do repositório de consultas precisam ser excluídos do clone. Se essa opção não for especificada, os dados do repositório de consultas serão copiados para o clone se o repositório de consultas estiver habilitado no banco de dados de origem. Essa opção está disponível desde o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1.

VERIFY_CLONEDB  
Verifica a consistência do novo banco de dados.  Essa opção é necessária se o banco de dados clonado é destinado ao uso de produção.  Habilitar VERIFY_CLONEDB também desabilita a coleta do repositório de estatísticas e de consultas; portanto, é equivalente a executar VERIFY_CLONEDB, NO_STATISTICS, NO_QUERYSTORE.  Essa opção está disponível desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP3, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU8.

> [!NOTE]  
> O comando a seguir pode ser usado para confirmar se o banco de dados clonado está pronto para produção: <br/>`SELECT DATABASEPROPERTYEX('clone_database_name', 'IsVerifiedClone')`


SERVICEBROKER<br>
Especifica se os catálogos de sistema relacionados ao Service Broker devem ser incluídos no clone.  A opção SERVICEBROKER não pode ser usada junto com VERIFY_CLONEDB.  Essa opção está disponível desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP3, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU8.

BACKUP_CLONEDB  
Cria e verifica se um backup do banco de dados do clone.  Se usado em combinação com VERIFY_CLONEDB, o banco de dados do clone é verificado antes da realização do backup.  Essa opção está disponível desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP3, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU8.
  
## <a name="remarks"></a>Comentários
As validações a seguir são executadas pelo DBCC CLONEDATABASE. O comando falhará se alguma das validações falhar.
- O banco de dados de origem deve ser um banco de dados de usuário. Não é permitida a clonagem de bancos de dados do sistema (mestre, modelo, msdb, tempdb, banco de dados de distribuição etc.).
- O banco de dados de origem deve estar online e legível.
- Um banco de dados que usa o mesmo nome do banco de dados do clone não deve existir.
- O comando não está em uma transação de usuário.

Se todas as validações forem bem-sucedidas, a clonagem do banco de dados de origem será executada pelas seguintes operações:
- Cria um novo banco de dados de destino que usa o mesmo layout de arquivo que o da fonte, mas com tamanhos de arquivos padrão do modelo de banco de dados.
- Cria um instantâneo interno do banco de dados de origem.
- Copia os metadados do sistema da origem para o banco de dados de destino.
- Copia todo o esquema para todos os objetos da origem para o banco de dados de destino.
- Copia estatísticas para todos os índices da origem para o banco de dados de destino.

> [!NOTE]  
> O novo banco de dados gerado de DBCC CLONEDATABASE é usado principalmente para fins de diagnósticos e solução de problemas.  Para que o banco de dados clonado seja compatível para uso como um banco de dados de produção, a opção de VERIFY_CLONEDB deve ser usada.

Todos os arquivos do banco de dados de destino herdarão as configurações de tamanho e crescimento do modelo de banco de dados. Os nomes de arquivo para o banco de dados de destino seguirão a convenção de número source_file_name _underscore_random. Se o nome de arquivo gerado já existir na pasta de destino, DBCC CLONEDATABASE falhará.

DBCC CLONEDATABASE não dará suporte à criação de um clone se houver algum objeto de usuário (tabelas, índices, esquemas, funções e assim por diante) que foi criado no modelo de banco de dados. Se os objetos de usuário estiverem presentes no modelo de banco de dados, o clone do banco de dados falhará com a seguinte mensagem de erro:

```
Msg 2601, Level 14, State 1, Line 1
Cannot insert duplicate key row in object <system table> with unique index 'index name'. The duplicate key value is <key value>   
```

> [!IMPORTANT]
> Se você tiver índices columnstore, veja [Considerações ao ajustar as consultas com índices Columnstore em bancos de dados do clone](https://techcommunity.microsoft.com/t5/SQL-Server/Considerations-when-tuning-your-queries-with-columnstore-indexes/ba-p/385294) para atualizar as estatísticas de índice columnstore antes de executar o comando **DBCC CLONEDATABASE**.  Começando com o SQL Server 2019, as etapas manuais descritas no artigo acima não serão mais necessárias, porque o comando **DBCC CLONEDATABASE** coleta essas informações automaticamente.

<a name="ctp23"></a>

## <a name="stats-blob-for-columnstore-indexes"></a>Blob de estatísticas para índices columnstore

[!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)], o `DBCC CLONEDATABASE` captura automaticamente os blobs de estatísticas para índices columnstore, de modo que nenhuma etapa manual é necessária.`DBCC CLONEDATABASE` cria uma cópia somente de esquema de um banco de dados que inclui todos os elementos necessários para solucionar problemas de desempenho de consulta sem copiar os dados. Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o comando não copiava as estatísticas necessárias para solucionar problemas com precisão em consultas de índice de columnstore, e etapas manuais eram necessárias para capturar essas informações.

Para obter informações relacionadas à segurança de dados em bancos de dados clonados, veja [Noções básicas sobre segurança de dados em bancos de dados clonados](https://techcommunity.microsoft.com/t5/SQL-Server/Understanding-data-security-in-cloned-databases-created-using/ba-p/385287).

## <a name="internal-database-snapshot"></a>Instantâneo de banco de dados interno
DBCC CLONEDATABASE usa um instantâneo de banco de dados interno do banco de dados de origem para a consistência transacional necessária para executar a cópia. O uso desse instantâneo evita bloqueio e problemas de simultaneidade quando esses comandos são executados. Se um instantâneo não puder ser criado, DBCC CLONEDATABASE falhará. 

Bloqueios de nível de banco de dados são mantidos durante as seguintes etapas do processo de cópia:
- Validar o banco de dados de origem
- Obter o bloqueio S para o banco de dados de origem
- Cria um instantâneo do banco de dados de origem
- Criar um banco de dados do clone (um banco de dados vazio herdado do modelo de banco de dados)
- Obter o bloqueio X para o banco de dados do clone
- Copiar os metadados para o banco de dados do clone
- Liberar todos os bloqueios de banco de dados

Assim que o comando tiver concluído a execução, o instantâneo interno será descartado. As opções TRUSTWORTHY e DB_CHAINING estão desativadas em um banco de dados clonado. 

## <a name="supported-objects"></a>Objetos com suporte
Somente os seguintes objetos podem ser clonados no banco de dados de destino. Objetos criptografados são clonados, mas não podem ser usados no banco de dados de clones. Todos os objetos que não estão listados na seção a seguir não são compatíveis no clone: 
- APPLICATION ROLE
- AVAILABILITY GROUP
- COLUMNSTORE INDEX
- CDB
- CDC
- CLR (desde o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 CU3, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 e versões posteriores)
- DATABASE PROPERTIES
- DEFAULT
- FILES AND FILEGROUPS
- Texto completo (desde o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU2)
- FUNCTION
- INDEX
- LOGIN
- PARTITION FUNCTION
- PARTITION SCHEME
- PROCEDURE   
> [!NOTE]   
> Há suporte para os procedimentos [!INCLUDE[tsql](../../includes/tsql-md.md)] em todas as versões desde o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2. Há suporte para procedimentos CLR desde o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 CU3. Há suporte para procedimentos compilados nativamente desde o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1.  

- QUERY STORE (desde o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1)   
> [!NOTE]   
> Os dados do repositório de consultas são copiados somente se ele está habilitado no banco de dados de origem. Para copiar as estatísticas de runtime mais recentes como parte do repositório de consultas, execute sp_query_store_flush_db para liberar as estatísticas de runtime para o repositório de consultas antes de executar DBCC CLONEDATABASE.  

- ROLE
- RULE
- SCHEMA
- SEQUENCE
- SPATIAL INDEX
- STATISTICS
- SYNONYM
- TABLE
- MEMORY OPTIMIZED TABLES (somente no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 e em versões posteriores).
- FILESTREAM AND FILETABLE OBJECTS (desde o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 CU3, [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 e versões posteriores). 
- TRIGGER
- TYPE
- UPGRADED DB
- USER
- VIEW
- XML INDEX
- XML SCHEMA COLLECTION  

## <a name="permissions"></a>Permissões  
Exige associação à função de servidor fixa **sysadmin** .

## <a name="error-log-messages"></a>Mensagens de log de erros
As mensagens a seguir são um exemplo de como as mensagens são registradas no log de erros durante o processo de clonagem:

```
2018-03-26 15:33:56.05 spid53 Database cloning for 'sourcedb' has started with target as 'sourcedb_clone'.

2018-03-26 15:33:56.46 spid53 Starting up database 'sourcedb_clone'.

2018-03-26 15:33:57.80 spid53 Setting database option TRUSTWORTHY to OFF for database 'sourcedb_clone'.

2018-03-26 15:33:57.80 spid53 Setting database option DB_CHAINING to OFF for database 'sourcedb_clone'.

2018-03-26 15:33:57.88 spid53 Starting up database 'sourcedb_clone'.

2018-03-26 15:33:57.91 spid53 Database 'sourcedb_clone' is a cloned database. A cloned database should be used for diagnostic purposes only and is not supported for use in a production environment.

2018-03-26 15:33:57.92 spid53 Database cloning for 'sourcedb' has finished. Cloned database is 'sourcedb_clone'.
```

## <a name="database-properties"></a>Propriedades de banco de dados
`DATABASEPROPERTYEX('dbname', 'IsClone')` retornará 1 se o banco de dados foi gerado usando DBCC CLONEDATABASE.

`DATABASEPROPERTYEX('dbname', 'IsVerifiedClone')` retornará 1 se o banco de dados foi verificado com êxito usando com VERIFY_CLONEDB.

## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-clone-of-a-database-that-includes-schema-statistics-and-query-store"></a>a. Criação de um clone de um banco de dados que inclui esquema, estatísticas e repositório de consultas 
O exemplo a seguir cria um clone do banco de dados AdventureWorks que inclui um esquema, estatísticas e dados do repositório de consultas ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 e versões posteriores)

```sql  
DBCC CLONEDATABASE (AdventureWorks, AdventureWorks_Clone);    
GO 
```  
  
### <a name="b-creating-a-schema-only-clone-of-a-database-without-statistics"></a>B. Criação de um clone somente de esquema de banco de dados sem estatísticas 
O exemplo a seguir cria um clone do banco de dados AdventureWorks que não inclui estatísticas ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 CU3 e versões posteriores)

```sql  
DBCC CLONEDATABASE (AdventureWorks, AdventureWorks_Clone) WITH NO_STATISTICS;    
GO 
```  

### <a name="c-creating-a-schema-only-clone-of-a-database-without-statistics-and-query-store"></a>C. Criação de um clone somente de esquema de banco de dados sem estatísticas e repositório de consultas 
O exemplo a seguir cria um clone do banco de dados AdventureWorks que não inclui estatísticas e dados do repositório de consultas ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 e versões posteriores)

```sql  
DBCC CLONEDATABASE (AdventureWorks, AdventureWorks_Clone) WITH NO_STATISTICS, NO_QUERYSTORE;    
GO 
```  

### <a name="d-creating-a-clone-of-a-database-that-is-verified-for-production-use"></a>D. Criação de um clone de um banco de dados verificado para uso em produção
O exemplo a seguir cria um clone somente de esquema do banco de dados AdventureWorks sem estatísticas e dados do repositório de consultas que são verificados para uso como um banco de dados de produção ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e versões posteriores).

```sql  
DBCC CLONEDATABASE (AdventureWorks, AdventureWorks_Clone) WITH VERIFY_CLONEDB;    
GO 
```  
  
### <a name="e-creating-a-clone-of-a-database-that-is-verified-for-production-use-that-includes-a-backup-of-the-cloned-database"></a>E. Criação de um clone de um banco de dados verificado para uso em produção que inclui um backup do banco de dados clonado
O exemplo a seguir cria um clone somente de esquema do banco de dados AdventureWorks sem estatísticas e dados do repositório de consultas que são verificados para uso como um banco de dados de produção.  Um backup verificado do banco de dados clonado também será criado ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 e versões posteriores).

```sql  
DBCC CLONEDATABASE (AdventureWorks, AdventureWorks_Clone) WITH VERIFY_CLONEDB, BACKUP_CLONEDB;    
GO 
```

## <a name="see-also"></a>Consulte Também
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)    
[Como gerar um script dos metadados do banco de dados necessários para criar um banco de dados somente estatísticas no SQL Server](https://support.microsoft.com/help/914288)   

