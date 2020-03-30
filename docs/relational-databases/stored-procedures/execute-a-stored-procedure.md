---
title: Executar um procedimento armazenado | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: conceptual
f1_keywords:
- sql13.swb.executeprocedure.general.f1
- sql13.swb.executeprocedure.f1
helpviewer_keywords:
- stored procedures [SQL Server], parameters
- extended stored procedures [SQL Server], executing
- system stored procedures [SQL Server], executing
- stored procedures [SQL Server], executing
- user-defined stored procedures [SQL Server]
ms.assetid: a0b1337d-2059-4872-8c62-3f967d8b170f
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 55acdb31113dde48aeda980e3823f194f66d15c0
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "80243416"
---
# <a name="execute-a-stored-procedure"></a>Executar um procedimento armazenado
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Este tópico descreve como executar um procedimento armazenado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Há dois modos diferentes de executar um procedimento armazenado. A primeira e mais comum abordagem é fazer com que um aplicativo ou usuário chame o procedimento. A segunda abordagem é definir o procedimento para ser executado automaticamente quando uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for iniciada. Quando um procedimento é chamado por um aplicativo ou usuário, a palavra-chave EXECUTE ou EXEC do [!INCLUDE[tsql](../../includes/tsql-md.md)] é declarada explicitamente na chamada. Como alternativa, o procedimento poderá ser chamado e executado sem a palavra-chave se o for a primeira instrução do lote [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para executar um procedimento armazenado usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   A ordenação de banco de dados de chamada é usada durante a correspondência de nomes dos procedimentos do sistema. Portanto, em seu aplicativo, você deve sempre fazer a diferenciação exata entre maiúsculas e minúsculas nos nomes em chamadas de procedimento. Por exemplo, este código falhará se for executado no contexto de um banco de dados que tenha uma ordenação com diferenciação de maiúsculas e minúsculas:  
  
    ```sql  
    EXEC SP_heLP; -- Will fail to resolve because SP_heLP does not equal sp_help  
    ```  
  
     Para exibir os nomes exatos do procedimento do sistema, consulte as exibições de catálogo [sys.system_objects](../../relational-databases/system-catalog-views/sys-system-objects-transact-sql.md) e [sys.system_parameters](../../relational-databases/system-catalog-views/sys-system-parameters-transact-sql.md) .  
  
-   Se um procedimento definido pelo usuário tiver o mesmo nome de um procedimento de sistema, o procedimento definido pelo usuário talvez nunca seja executado.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Executando procedimentos armazenados do sistema  
  
     Procedimentos armazenados do sistema começam com o prefixo **sp_** . Como eles aparecem logicamente em todos os bancos de dados definidos pelo usuário e pelo sistema, podem ser executados de qualquer banco de dados sem ter que qualificar totalmente o nome de procedimento. No entanto, recomendamos que você qualifique por esquema todos os nomes dos procedimentos armazenados do sistema com o nome do esquema **sys** para evitar conflitos de nomes. O exemplo a seguir mostra o método recomendado para chamar um procedimento armazenado do sistema.  
  
    ```sql  
    EXEC sys.sp_who;  
    ```  
  
-   Executando procedimentos armazenados definidos pelo usuário  
  
     Ao executar um procedimento definido pelo usuário, nós recomendamos qualificar o nome de procedimento com o nome do esquema. Esta prática melhora um pouco o desempenho, pois o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não tem que pesquisar vários esquemas. Isso também impedirá a execução do procedimento errado se um banco de dados tiver procedimentos com o mesmo nome em vários esquemas.  
  
     O exemplo a seguir mostra o método recomendado para executar um procedimento armazenado definido pelo usuário. Observe que o procedimento aceita um parâmetro de entrada. Para obter informações sobre como especificar parâmetros de entrada e saída, veja [Especificar parâmetros](../../relational-databases/stored-procedures/specify-parameters.md).  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    EXEC dbo.uspGetEmployeeManagers @BusinessEntityID = 50;  
    ```  
  
     -Ou-  
  
    ```sql  
    EXEC AdventureWorks2012.dbo.uspGetEmployeeManagers 50;  
    GO  
    ```  
  
     Se um procedimento não qualificado definido pelo usuário for especificado, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] pesquisará o procedimento na seguinte ordem:  
  
    1.  Esquema **sys** do banco de dados atual.  
  
    2.  O esquema padrão do chamador se executado em um lote ou em SQL dinâmico. Ou, se o nome do procedimento não qualificado aparecer no corpo da definição de outro procedimento, o esquema que contém esse outro procedimento será pesquisado a seguir.  
  
    3.  O esquema **dbo** no banco de dados atual.  
  
-   Procedimentos armazenados executados automaticamente  
  
     Os procedimentos marcados para execução automática são executados sempre que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado e o banco de dados **mestre** é recuperado durante esse processo de inicialização. A configuração dos procedimentos para execução automática pode ser útil para executar operações de manutenção de banco de dados ou para que os procedimentos sejam executados continuamente como processos em segundo plano. Um outro uso para a execução automática é o procedimento realizar tarefas do sistema ou de manutenção no **tempdb**, tal como criar uma tabela temporária global. Isso garante que essa tabela temporária existirá sempre que o **tempdb** for recriado durante a inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Um procedimento executado automaticamente funciona com as mesmas permissões dos membros da função de servidor fixa do **sysadmin** . Qualquer mensagem de erro gerada pelo procedimento é gravada no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Não há limite para o número de procedimentos de inicialização que você pode ter, porém lembre-se de que cada um consome um thread de trabalho durante a execução. Se precisar executar vários procedimentos na inicialização, mas, se não for necessário executá-los em paralelo, torne um procedimento o procedimento de inicialização e faça com que este procedimento chame os demais. Isto usará apenas um thread de trabalho.  
  
    > [!TIP]  
    >  Não retorne nenhum conjunto de resultados de um procedimento executado automaticamente. Como o procedimento armazenado é executado pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , em vez de pelo aplicativo ou usuário, os conjuntos de resultados não têm para onde ir.  
  
-   Configurando, limpando e controlando a execução automática  
  
     Somente o administrador de sistema (**sa**) pode marcar um procedimento para ser executado automaticamente. Além disso, o procedimento armazenado deve estar no banco de dados **mestre** , pertencer ao **sa**e não deverá conter parâmetros de entrada ou de saída.  
  
     Use [sp_procoption](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md) para:  
  
    1.  Determinar um procedimento existente como um procedimento de inicialização.  
  
    2.  Interromper a execução de um procedimento na inicialização do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 Para obter mais informações, veja [EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-transact-sql.md) e [Cláusula EXECUTE AS &#40;Transact-SQL&#41;](../../t-sql/statements/execute-as-clause-transact-sql.md).  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Para obter mais informações, confira a seção “Permissões” em [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-execute-a-stored-procedure"></a>Para executar um procedimento armazenado  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], expanda essa instância e expanda **Bancos de Dados**.  
  
2.  Expanda o banco de dados desejado, expanda **Programabilidade**e expanda **Procedimentos Armazenados**.  
  
3.  Clique com o botão direito do mouse no procedimento armazenado definido pelo usuário desejado e clique em **Executar Procedimento Armazenado**.  
  
4.  Na caixa de diálogo **Executar Procedimento** , especifique um valor para cada parâmetro e se ele deve passar um valor nulo.  
  
     **Parâmetro**  
     Indica o nome do parâmetro.  
  
     **Tipo de Dados**  
     Indica o tipo de dados do parâmetro.  
  
     **Parâmetro de Saída**  
     Indica se este é um parâmetro de saída.  
  
     **Passar Valor Nulo**  
     Passe um NULL como valor do parâmetro.  
  
     **Valor**  
     Digite o valor do parâmetro ao chamar o procedimento.  
  
5.  Para executar o procedimento armazenado, clique em **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-execute-a-stored-procedure"></a>Para executar um procedimento armazenado  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como executar um procedimento armazenado que espera um parâmetro. O exemplo executa o procedimento armazenado `uspGetEmployeeManagers` com o valor  `6` especificado como o parâmetro `@EmployeeID` .  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC dbo.uspGetEmployeeManagers 6;  
GO  
```  
  
#### <a name="to-set-or-clear-a-procedure-for-executing-automatically"></a>Para definir ou limpar um procedimento para execução automática  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_procoption](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md) para definir um procedimento para execução automática.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionName = 'startup'   
    , @OptionValue = 'on';  
```  
  
#### <a name="to-stop-a-procedure-from-executing-automatically"></a>Para interromper a execução de um procedimento automaticamente  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_procoption](../../relational-databases/system-stored-procedures/sp-procoption-transact-sql.md) para interromper a execução automática de um procedimento.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_procoption @ProcName = '<procedure name>'   
    , @OptionValue = 'off';  
```  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> Exemplo (Transact-SQL)  
  
## <a name="see-also"></a>Consulte Também  
 [Especificar parâmetros](../../relational-databases/stored-procedures/specify-parameters.md)   
 [Configurar a opção de configuração de servidor scan for startup procs](../../database-engine/configure-windows/configure-the-scan-for-startup-procs-server-configuration-option.md)   
 [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [Procedimentos armazenados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)  
  
  
