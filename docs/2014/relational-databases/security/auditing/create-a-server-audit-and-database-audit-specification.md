---
title: Criar uma especificação de auditoria de servidor e de auditoria de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.sqlaudit.dbaudit.general.f1
helpviewer_keywords:
- audits [SQL Server], creating database specification
- database audit [SQL Server]
ms.assetid: 26ee85de-6e97-4318-b526-900924d96e62
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 0cad01eae45d534f0f74911ce8f57827858cc920
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063228"
---
# <a name="create-a-server-audit-and-database-audit-specification"></a>Criar uma especificação de auditoria de banco de dados e de servidor
  Este tópico descreve como criar uma especificação de auditoria de servidor e de banco de dados no [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
 *Auditar* uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ou um banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] envolve eventos de rastreamento e de log que ocorrem no sistema. O objeto *SQL Server Audit* coleta uma instância única de ações no nível do servidor e/ou do banco de dados e grupos de ações a serem monitoradas. A auditoria está no nível de instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Você pode ter várias auditorias por instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . O objeto *Especificação de Auditoria de Banco de Dados* pertence a uma auditoria. É possível criar uma especificação da auditoria de banco de dados por banco de dados do SQL Server por auditoria. Para obter mais informações, veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](sql-server-audit-database-engine.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar uma especificação de auditoria de servidor e de banco de dados usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
 As especificações de auditoria de banco de dados são objetos não protegidos que residem em um determinado banco de dados. Quando uma especificação de auditoria de banco de dados é criada, ela fica em um estado desabilitado.  
  
 Quando você estiver criando ou modificando uma especificação de auditoria de banco de dados em um banco de dados de usuário, não inclua ações de auditoria em objetos do escopo de servidor, como as exibições do sistema. Se forem incluídos objetos de escopo do servidor, a auditoria será criada. No entanto, os objetos de escopo do servidor não serão incluídos e nenhum erro será retornado. Para auditar objetos de escopo do servidor, use uma especificação de auditoria de banco de dados no banco de dados mestre.  
  
 As especificações de auditoria de banco de dados residem no banco de dados onde são criadas, com exceção do banco de dados de sistema `tempdb`.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
  
-   Os usuários com a permissão ALTER ANY DATABASE AUDIT podem criar especificações de auditoria de banco de dados e associá-las a qualquer auditoria.  
  
-   Depois que uma especificação de auditoria de banco de dados é criada, ela pode ser exibida por entidades que tenham a permissão CONTROL SERVER, ALTER ANY DATABASE AUDIT ou com a conta sysadmin.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-a-server-audit"></a>Para criar uma auditoria de servidor  
  
1.  No Pesquisador de Objetos, expanda a pasta **Segurança** .  
  
2.  Clique com o botão direito do mouse na pasta **auditorias** e selecione **nova auditoria...**. Para obter mais informações, consulte [criar uma auditoria de servidor e uma especificação de auditoria de servidor](create-a-server-audit-and-server-audit-specification.md).  
  
3.  Quando terminar de selecionar as opções, clique em **OK**.  
  
#### <a name="to-create-a-database-level-audit-specification"></a>Para criar uma especificação de auditoria no nível de banco de dados  
  
1.  No Pesquisador de Objetos, expanda o banco de dados onde você deseja criar uma especificação de auditoria.  
  
2.  Expanda a pasta **Segurança** .  
  
3.  Clique com o botão direito do mouse na pasta **especificações de auditoria** e selecione **nova especificação de auditoria de banco de dados...**.  
  
     As opções a seguir estão disponíveis na caixa de diálogo **Criar Especificação de Auditoria de Banco de Dados** .  
  
     **Nome**  
     O nome da especificação de auditoria de banco de dados. Esse nome é gerado automaticamente quando você cria uma nova especificação de auditoria de servidor, mas é editável.  
  
     **Auditoria**  
     O nome de uma auditoria de banco de dados existente. Digite o nome da auditoria ou selecione-o na lista.  
  
     **Tipo de Ação de Auditoria**  
     Especifica os grupos de ação de auditoria no nível de banco de dados e as ações de auditoria a capturar. Para obter a lista de grupos de ação de auditoria no nível de banco de dados, ações de auditoria e uma descrição dos eventos que eles contêm, veja [Ações e grupos de ações de auditoria do SQL Server](sql-server-audit-action-groups-and-actions.md).  
  
     **Esquema de Objeto**  
     Exibe o esquema para **Object Name**especificado.  
  
     **Object Name**  
     Nome do objeto a ser auditado. Isso só está disponível para ações de auditoria e não se aplica a grupos de auditoria.  
  
     **Reticências (...)**  
     Abre a caixa de diálogo **Selecionar Objetos** para procurar e selecionar um objeto disponível, com base no **Tipo de Ação de Auditoria**especificado.  
  
     **Nome Principal**  
     A conta para filtrar a auditoria para o objeto que está sendo auditado.  
  
     **Reticências (...)**  
     Abre a caixa de diálogo **Selecionar Objetos** para procurar e selecionar um objeto disponível, com base no **Nome do Objeto**especificado.  
  
4.  Quando terminar de selecionar as opções, clique em **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-server-audit"></a>Para criar uma auditoria de servidor  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE master ;  
    GO  
    -- Create the server audit.   
    CREATE SERVER AUDIT Payrole_Security_Audit  
        TO FILE ( FILEPATH =   
    'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\DATA' ) ;   
    GO  
    -- Enable the server audit.   
    ALTER SERVER AUDIT Payrole_Security_Audit   
    WITH (STATE = ON) ;  
    ```  
  
#### <a name="to-create-a-database-level-audit-specification"></a>Para criar uma especificação de auditoria no nível de banco de dados  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo a seguir cria uma especificação de auditoria de banco de dados denominada `Audit_Pay_Tables` que audita instruções SELECT e INSERT pelo usuário `dbo` , para a tabela `HumanResources.EmployeePayHistory` baseada na auditoria de servidor definida acima.  
  
    ```  
    USE AdventureWorks2012 ;   
    GO  
    -- Create the database audit specification.   
    CREATE DATABASE AUDIT SPECIFICATION Audit_Pay_Tables  
    FOR SERVER AUDIT Payrole_Security_Audit  
    ADD (SELECT , INSERT  
         ON HumanResources.EmployeePayHistory BY dbo )   
    WITH (STATE = ON) ;   
    GO  
  
    ```  
  
 Para obter mais informações, veja [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-transact-sql) e [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-audit-specification-transact-sql).  
  
  
