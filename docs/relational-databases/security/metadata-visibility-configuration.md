---
title: Configuração de visibilidade de metadados | Microsoft Docs
description: Saiba como configurar a visibilidade de metadados para protegíveis que um usuário tem ou ao qual recebeu permissão no SQL Server.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- subcomponents visibility [SQL Server]
- metadata [SQL Server], visibility
- permissions [SQL Server], metadata access
- viewing metadata
- objects [SQL Server], metadata
- displaying metadata
- database metadata [SQL Server]
- metadata [SQL Server], permissions
ms.assetid: 50d2e015-05ae-4014-a1cd-4de7866ad651
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f5317580647f0d8795277722e44382c2a77cdafe
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97467287"
---
# <a name="metadata-visibility-configuration"></a>Configuração de visibilidade de metadados
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  A visibilidade de metadados é limitada aos protegíveis que pertencem a um usuário ou sobre os quais recebeu alguma permissão. Por exemplo, a consulta a seguir retornará uma linha se o usuário recebeu uma permissão SELECT ou INSERT na tabela `myTable`.  
  
```  
SELECT name, object_id  
FROM sys.tables  
WHERE name = N'myTable';  
GO  
```  
  
 Entretanto, se o usuário não possuir nenhuma permissão em `myTable`, a consulta retornará um conjunto de resultados vazio.  
  
## <a name="scope-and-impact-of-metadata-visibility-configuration"></a>Escopo e impacto da configuração de visibilidade de metadados  
 A configuração de visibilidade de metadados apenas se aplica aos seguintes protegíveis.  

:::row:::
    :::column:::
        Exibições do catálogo

        Metadados com exposição de funções internas

        Exibições de compatibilidade
    :::column-end:::
    :::column:::
         Procedimentos armazenados do [!INCLUDE[ssDE](../../includes/ssde-md.md)] **sp_help**

        Exibições do esquema de informações

        Propriedades estendidas
    :::column-end:::
:::row-end:::
  
 A configuração de visibilidade de metadados não se aplica aos seguintes protegíveis.  

:::row:::
    :::column:::
        Tabelas do sistema de envio de logs

        Tabelas do sistema de plano de manutenção do banco de dados

        Tabelas do sistema de replicação
    :::column-end:::
    :::column:::
         [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tabelas do sistema do Agent

        Tabelas do sistema de backup

        Replicação e procedimento armazenados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent **sp_help**
    :::column-end:::
:::row-end:::

 Acessibilidade de metadados limitada significa o seguinte:  
  
-   Aplicativos que assumem que o acesso de metadados **público** será interrompido.  
  
-   Consultas nas exibições de sistema podem retornar apenas um subconjunto de linhas, ou às vezes um conjunto de resultados vazio.  
  
-   Funções internas, que emitem metadados como em OBJECTPROPERTYEX podem retornar NULO.  
  
-   Os procedimentos armazenados do [!INCLUDE[ssDE](../../includes/ssde-md.md)] **sp_help** podem retornar apenas um subconjunto de linhas ou NULL.  
  
 Os módulos SQL, como os procedimentos armazenados e os gatilhos, são executados no contexto de segurança do chamador e, em consequência, têm acessibilidade limitada aos metadados. Por exemplo, no código a seguir, quando o procedimento armazenado tentar acessar os metadados para a tabela `myTable` na qual o visitante não tem nenhum direito, há retorno de um conjunto de resultados vazio. Em versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é retornada uma linha.  
  
```  
CREATE PROCEDURE assumes_caller_can_access_metadata  
BEGIN  
SELECT name, object_id   
FROM sys.objects   
WHERE name = N'myTable';  
END;  
GO  
```  
  
 Você pode conceder aos visitantes uma permissão VIEW DEFINITION, que permita aos visitantes exibir os metadados no escopo apropriado: nível de objeto, nível de banco de dados ou nível de servidor. Assim, no exemplo prévio, se o visitante tiver uma permissão VIEW DEFINITION em `myTable`, o procedimento armazenado retornará uma linha. Para obter mais informações, veja [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md) e [Permissões de banco de dados GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md).  
  
 Você também pode modificar o procedimento armazenado de forma a executar com as credenciais do proprietário. Quando o proprietário do procedimento e o da tabela forem o mesmo proprietário, o encadeamento de propriedade é aplicável e o contexto de segurança do proprietário do procedimento ativa o acesso aos metadados para `myTable`. Nesse cenário, o seguinte código retorna uma linha de metadados ao chamador.  
  
> [!NOTE]  
>  O exemplo a seguir utiliza a exibição do catálogo [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) , em vez da exibição de compatibilidade [sys.sysobjects](../../relational-databases/system-compatibility-views/sys-sysobjects-transact-sql.md) .  
  
```  
CREATE PROCEDURE does_not_assume_caller_can_access_metadata  
WITH EXECUTE AS OWNER  
AS  
BEGIN  
SELECT name, object_id  
FROM sys.objects   
WHERE name = N'myTable'   
END;  
GO  
```  
  
> [!NOTE]  
>  Você pode usar EXECUTE AS para alternar temporariamente para o contexto de segurança do chamador. Para obter mais informações, veja [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md).  
  
## <a name="benefits-and-limits-of-metadata-visibility-configuration"></a>Benefícios e limites da configuração de visibilidade de metadados  
 A configuração de visibilidade de metadados pode ter uma função importante em seu plano de segurança global. Entretanto, há casos nos quais um usuário habilidoso e determinado pode forçar a divulgação de alguns metadados. Recomendamos que você implante permissões para metadados como um dos muitos detalhes de defesa.  
  
 É teoricamente possível forçar a emissão de metadados em mensagens de erro manipulando a ordem de avaliação do predicado nas consultas. A possibilidade de tais *ataques por tentativa e erro* não é específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Está implícita nas transformações associativas e comutativas permitidas pela álgebra relacional. Você pode reduzir esse risco limitando as informações retornadas nas mensagens de erro. Para restringir ainda mais a visibilidade de metadados desse modo, você pode iniciar o servidor com o sinalizador de rastreamento 3625. Este sinalizador de rastreamento limita a quantidade de informações mostradas nas mensagens de erro. Por sua vez, isso ajuda a impedir divulgações forçadas. Em compensação as mensagens de erro serão concisas e será difícil usar para propósitos de depuração. Para obter mais informações, consulte [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../database-engine/configure-windows/database-engine-service-startup-options.md) e [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).  
  
 Os metadados a seguir não estão sujeitos a divulgação forçada:  
  
-   O valor armazenado na coluna **provider_string** de **sys.servers**. Um usuário que não tem permissão ALTER ANY LINKED SERVER verá um valor NULL nessa coluna.  
  
-   Definição de fonte de um objeto definido pelo usuário como um procedimento armazenado ou gatilho. O código de origem só é visível quando um destes for verdadeiro:  
  
    -   O usuário tem permissão VIEW DEFINITION no objeto.  
  
    -   Não foi negada permissão ao usuário em VIEW DEFINITION no objeto e possui permissões em CONTROL, ALTER ou em TAKE OWNERSHIP no objeto. Todos os outros usuários verão NULL.  
  
-   As colunas de definição encontradas nas exibições do catálogo a seguir:  

    - **sys.all_sql_modules**  
    - **sys.server_sql_modules**  
    - **sys.default_constraints**
    - **sys.numbered_procedures**
    - **sys.sql_modules**
    - **sys.check_constraints**
    - **sys.computed_columns**

-   A coluna **ctext** na exibição de compatibilidade **syscomments** .  
  
-   A saída do procedimento **sp_helptext** .  
  
-   As seguintes colunas nas exibições do esquema de informações:

    - INFORMATION_SCHEMA.CHECK_CONSTRAINTS.CHECK_CLAUSE
    - INFORMATION_SCHEMA.DOMAINS.DOMAIN_DEFAULT
    - INFORMATION_SCHEMA.ROUTINES.ROUTINE_DEFINITION
    - INFORMATION_SCHEMA.COLUMNS.COLUMN_DEFAULT
    - INFORMATION_SCHEMA.ROUTINE_COLUMNS.COLUMN_DEFAULT
    - INFORMATION_SCHEMA.VIEWS.VIEW_DEFINITION

-   Função OBJECT_DEFINITION()  
  
-   O valor armazenado na coluna password_hash em **sys.sql_logins**.  Um usuário que não tenha a permissão CONTROL SERVER verá um valor NULL nessa coluna.  
  
> [!NOTE]  
>  As definições de SQL de procedimentos e funções de sistema internos são publicamente visíveis na exibição do catálogo **sys.system_sql_modules** , no procedimento armazenado **sp_helptext** e na função OBJECT_DEFINITION().  
  
## <a name="general-principles-of-metadata-visibility"></a>Princípios gerais de visibilidade de metadados  
 A seguir, alguns princípios gerais para serem considerados relativos à visibilidade de metadados:  
  
-   Permissões implícitas de funções fixas  
  
-   Escopo das permissões  
  
-   Precedência em DENY  
  
-   Visibilidade de metadados de subcomponente  
  
### <a name="fixed-roles-and-implicit-permissions"></a>Funções fixas e permissões implícitas  
 Os metadados que podem ser acessados através de funções fixas dependem de suas permissões implícitas correspondentes.  
  
### <a name="scope-of-permissions"></a>Escopo das permissões  
 Permissões em um escopo implicam na capacidade de ver os metadados nesse escopo e em todos os escopos inclusos. Por exemplo, a permissão SELECT dentro de um esquema implica que o beneficiado tem permissão SELECT em todos os protegíveis contidos nesse esquema. A concessão de permissão SELECT em um esquema permite que usuário veja então os metadados do esquema e também todas as tabelas, exibições, funções, procedimentos, filas, sinônimos, tipos e coleções de esquema XML inclusos. Para obter mais informações sobre escopos, veja [Hierarquia de permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md).  
  
### <a name="precedence-of-deny"></a>Precedência em DENY  
 DENY normalmente tem precedência sobre outras permissões. Por exemplo, se um usuário de banco de dados recebeu permissão EXECUTE em um esquema, mas teve a permissão EXECUTE negada em um procedimento armazenado nesse esquema, o usuário não pode exibir os metadados para esse procedimento armazenado.  
  
 Além disso, se um usuário teve a permissão EXECUTE negada em um esquema, mas recebeu a permissão EXECUTE em um procedimento armazenado nesse esquema, o usuário não pode exibir os metadados para esse procedimento armazenado.  
  
 Outro exemplo, se um usuário teve permissão EXECUTE concedida e negada em um procedimento armazenado, o que é possível através de suas diversas associações à funções, DENY terá precedência e o usuário não poderá exibir os metadados do procedimento armazenado.  
  
### <a name="visibility-of-subcomponent-metadata"></a>Visibilidade de metadados de subcomponente  
 A visibilidade de subcomponentes, como índices, restrições de verificação e gatilhos são determinados através de permissões no pai. Esses subcomponentes não têm permissões que possam ser concedidas. Por exemplo, se um usuário recebeu alguma permissão em uma tabela, o usuário poderá exibir os metadados para as tabelas, colunas, índices, restrições de verificações, gatilhos e outros subcomponentes similares.  
  
#### <a name="metadata-that-is-accessible-to-all-database-users"></a>Metadados acessíveis a todos os usuários do banco de dados  
 Algum metadados devem ser acessíveis a todos os usuários em um banco de dados específico. Por exemplo, grupos de arquivos não têm permissões que possam ser conferidas; consequentemente, um usuário não pode receber permissão para exibir os metadados de um grupo de arquivos. Entretanto, qualquer usuário que possa criar uma tabela deve poder acessar os metadados de grupo de arquivos para usar *filegroup* ON ou as cláusulas TEXTIMAGE_ON *filegroup* da instrução CREATE TABLE.  
  
 Os metadados retornados pelas funções DB_ID() e DB_NAME() são visíveis para todos os usuários.  
  
 Esta é uma lista das exibições do catálogo visíveis na função **pública**.  

:::row:::
    :::column:::
        **sys.partition_functions**

        **sys.partition_schemes**

        **sys.filegroups**

        **sys.database_files**

        **sys.partitions**

        **sys.schemas**

        **sys.sql_dependencies**

        **sys.parameter_type_usages**
    :::column-end:::
    :::column:::
        **sys.partition_range_values**

        **sys.data_spaces**

        **sys.destination_data_spaces**

        **sys.allocation_units**

        **sys.messages**

        **sys.configurations**

        **sys.type_assembly_usages**

        **sys.column_type_usages**
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Consulte Também  
 [GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [DENY &#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [REVOKE &#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [Cláusula EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições de compatibilidade &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
