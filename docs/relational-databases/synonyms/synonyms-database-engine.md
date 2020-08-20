---
description: Sinônimos (Mecanismo de Banco de Dados)
title: Sinônimos (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- synonyms [SQL Server], about synonyms
ms.assetid: 6210e1d5-075f-47e4-ac8d-f84bcf26fbc0
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e74d6062af769de9364e46faea78f81e7353f630
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490320"
---
# <a name="synonyms-database-engine"></a>Sinônimos (Mecanismo de Banco de Dados)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Um sinônimo é um objeto de banco de dados que atende aos seguintes propósitos:  
  
-   Fornece um nome alternativo para outro objeto do banco de dados referido como o objeto base que pode existir em um servidor local ou remoto.  
  
-   Fornece uma camada de abstração que protege um aplicativo cliente de alterações feitas no nome ou local do objeto base.  
  
Por exemplo, considere a tabela **Employee** do [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]localizada em um servidor denominado **Server1**. Para fazer referência a esta tabela em outro servidor, **Server2**, um aplicativo precisa usar o nome de quatro partes **Server1.AdventureWorks.Person.Employee**. Além disso, se o local da tabela for alterado, por exemplo, para outro servidor, o aplicativo cliente precisará ser modificado para refletir essa alteração.  
  
Para resolver os dois problemas, é possível criar um sinônimo, **EmpTable**, no **Server2** para a tabela **Employee** no **Server1**. Agora, o aplicativo cliente precisa usar apenas o nome de uma única parte, **EmpTable**, para fazer referência à tabela **Employee** . Além disso, se o local da tabela **Employee** for alterado, você precisará modificar o sinônimo, **EmpTable**, para apontar para o novo local da tabela **Employee** . Como não existe nenhuma instrução ALTER SYNONYM, você precisa primeiro remover o sinônimo, **EmpTable**, e criá-lo novamente com o mesmo nome, mas apontá-lo para o novo local **Employee**.  
  
Um sinônimo pertence a um esquema e, como outros objetos de um esquema, seu nome precisa ser exclusivo. É possível criar sinônimos para os seguintes objetos de banco de dados:  

:::row:::
    :::column:::
        Procedimento armazenado de assembly (CLR)

        Função escalar de assembly (CLR)

        Procedimento de filtro de replicação

        Função SQL escalar

        Função SQL com valor de tabela embutida

        Visualizar
    :::column-end:::
    :::column:::
        Função com valor de tabela de assembly (CLR)

        Funções de agregação de assembly (CLR)

        Funções de agregação de assembly (CLR)

        Função SQL com valor de tabela

        Procedimento armazenado SQL

        Tabela* (definida pelo usuário)
    :::column-end:::
:::row-end:::

*Inclui tabelas temporárias locais e globais  
  
> [!NOTE]  
> Não há suporte para nomes de quatro partes para objetos base de função.  
  
Um sinônimo não pode ser o objeto base de outro sinônimo e um sinônimo não pode fazer referência a uma função de agregação definida pelo usuário.  
  
A associação entre um sinônimo e seu objeto base é feita apenas pelo nome. Toda verificação de existência, tipo e permissões no objeto base é adiada até o tempo de execução. Portanto o objeto base pode ser modificado, descartado ou descartado e substituído por outro objeto que tenha o mesmo nome que o objeto base original. Por exemplo, considere um sinônimo, **MyContacts**, que faz referência à tabela **Person.Contact** no [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)]. Se a tabela **Contact** for removida e substituída por uma exibição nomeada **Person.Contact**, **MyContacts** agora fará referência à exibição **Person.Contact** .  
  
Referências a sinônimos não são associadas a esquemas. Portanto, um sinônimo pode ser descartado a qualquer momento. No entanto, ao descartar um sinônimo, você corre o risco de deixar referências pendentes ao sinônimo descartado. Essas referências serão localizadas apenas em tempo de execução.  
  
## <a name="synonyms-and-schemas"></a>Sinônimos e esquemas  
Se você tiver um esquema padrão do qual você não é o proprietário e desejar criar um sinônimo, deverá qualificar o nome do sinônimo com o nome de um esquema que seja de sua propriedade. Por exemplo, se você possuir um esquema **x**, mas **y** for seu esquema padrão e você usar a instrução CREATE SYNONYM, deverá prefixar o nome do sinônimo com o esquema **x**, em vez de nomear o sinônimo usando um nome de uma única parte. Para obter mais informações sobre como criar sinônimos, veja [CREATE SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/create-synonym-transact-sql.md).  
  
## <a name="granting-permissions-on-a-synonym"></a>Concedendo permissões em um sinônimo  
Apenas os proprietários de sinônimos, membros de **db_owner**, ou membros de **db_ddladmin** podem conceder permissão em um sinônimo.  
  
Você pode `GRANT`, `DENY` e `REVOKE` todas ou qualquer uma das seguintes permissões em um sinônimo:  

:::row:::
    :::column:::
      CONTROL

      Execute

      SELECT

      UPDATE
    :::column-end:::
    :::column:::
      Delete (excluir)

      INSERT

      TAKE OWNERSHIP

      VIEW DEFINITION
    :::column-end:::
:::row-end:::

## <a name="using-synonyms"></a>Usando sinônimos  
 É possível usar sinônimos em lugar do objeto base referenciado em várias instruções SQL e contextos de expressão. As seguintes colunas contêm uma lista dessas instruções e contextos de expressão:  

:::row:::
    :::column:::
        SELECT

        UPDATE

        Execute
    :::column-end:::
    :::column:::
        INSERT

        Delete (excluir)

        Subseleções
    :::column-end:::
:::row-end:::
 
 Quando você está trabalhando com sinônimos nos contextos declarados anteriormente, o objeto base é afetado. Por exemplo, se um sinônimo fizer referência a um objeto base que está em uma tabela e você inserir uma linha no sinônimo, na verdade você estará inserindo uma linha na tabela referida.  
  
> [!NOTE]  
> Não é possível fazer referência a um sinônimo localizado em um servidor vinculado.  
  
 É possível usar um sinônimo como o parâmetro da função OBJECT_ID. No entanto, a função retorna a ID do objeto do sinônimo, não o objeto base.  
  
 Não é possível fazer referência a um sinônimo em uma instrução DDL. Por exemplo, as instruções a seguir que fazem referência a um sinônimo denominado `dbo.MyProduct`geram erros:  
  
```sql  
ALTER TABLE dbo.MyProduct  
   ADD NewFlag int null;  
EXEC ('ALTER TABLE dbo.MyProduct  
   ADD NewFlag int null');  
```  
  
As instruções de permissão a seguir são associadas apenas ao sinônimo e não ao objeto base:  

:::row:::
    :::column:::
        GRANT

        REVOKE
    :::column-end:::
    :::column:::
        NEGAR
    :::column-end:::
:::row-end:::

Sinônimos não são associados a esquemas e, portanto, não podem ser referidos pelos seguintes contextos de expressão associados a esquemas:  

:::row:::
    :::column:::
        Restrições CHECK

        Expressões padrão

        Exibições associadas a esquema
    :::column-end:::
    :::column:::
        Colunas computadas

        Expressões de regra

        Funções associadas a esquema
    :::column-end:::
:::row-end:::
  
Para obter mais informações sobre funções associadas a esquema, veja [Criar funções definidas pelo usuário &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md).  
  
## <a name="getting-information-about-synonyms"></a>Obtendo informações sobre sinônimos  
A exibição do catálogo `sys.synonyms` contém uma entrada para cada sinônimo em determinado banco de dados. Essa exibição do catálogo expõe metadados de sinônimos, como o nome do sinônimo e o nome do objeto base. Para obter mais informações, confira [sinônimos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-synonyms-transact-sql.md).  
  
Usando propriedades estendidas é possível adicionar texto descritivo ou instrucional, máscaras de entrada e regras de formatação como propriedades de um sinônimo. Como a propriedade é armazenada em um banco de dados, todos os aplicativos que leem a propriedade podem avaliar o objeto da mesma maneira. Para obter mais informações, veja [sp_addextendedproperty &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproperty-transact-sql.md).  
  
Para localizar o tipo base do objeto base de um sinônimo, use a função OBJECTPROPERTYEX. Para obter mais informações, veja [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md).  
  
### <a name="examples"></a>Exemplos  
O exemplo a seguir retorna o tipo básico do objeto base de um sinônimo que é um objeto local.  
  
```sql  
USE tempdb;  
GO  
CREATE SYNONYM MyEmployee   
FOR AdventureWorks2012.HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('MyEmployee'), 'BaseType') AS BaseType;  
```  
  
O exemplo a seguir retorna o tipo básico do objeto base de um sinônimo que é um objeto remoto localizado em um servidor denominado `Server1`.  
  
```sql  
EXECUTE sp_addlinkedserver Server1;  
GO  
CREATE SYNONYM MyRemoteEmployee  
FOR Server1.AdventureWorks2012.HumanResources.Employee;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('MyRemoteEmployee'), 'BaseType') AS BaseType;  
GO  
```  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Criar Sinônimos](../../relational-databases/synonyms/create-synonyms.md)    
 [CREATE SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/create-synonym-transact-sql.md)    
 [DROP SYNONYM &#40;Transact-SQL&#41;](../../t-sql/statements/drop-synonym-transact-sql.md)    
  
