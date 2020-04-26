---
title: Criar um alerta usando um nível de gravidade | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
- SQL Server Agent, alerts
- severity levels [SQL Server]
- alerts [SQL Server], severity levels
ms.assetid: a1fd71bf-5bf9-4ce2-9a1d-032576a4a6e9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8e94b24634eedf68afcb25c8c1ef957ce063cdc4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63136736"
---
# <a name="create-an-alert-using-severity-level"></a>Create an Alert Using Severity Level
  Este tópico descreve como criar um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alerta do Agent que é gerado quando um evento de um nível de severidade específico ocorre [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para criar um alerta usando um nível de severidade, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] fornece um modo gráfico e fácil para gerenciar o sistema de alertas inteiro e é recomendado para configurar uma infraestrutura de alerta.  
  
-   Eventos gerados com **xp_logevent** ocorrem no banco de dados mestre. Portanto, **xp_logevent** não dispara um alerta a menos que o **@database_name** para o alerta seja **'mestre'** ou NULL.  
  
-   Níveis de severidade de 19 a 25 enviam uma mensagem do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao log de aplicativos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows e disparam um alerta. Eventos com níveis de severidade inferiores a 19 vão disparar alertas apenas se você tiver usado **sp_altermessage**, RAISERROR WITH LOG ou **xp_logevent** para obrigá-los a serem gravados no log de aplicativos do Windows.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Por padrão, somente membros da função de servidor fixa **sysadmin** podem executar **sp_add_alert**.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-create-an-alert-using-severity-level"></a>Para criar um alerta usando um nível de severidade  
  
1.  No **Pesquisador de Objetos** , clique no sinal de adição para expandir o servidor no qual você deseja criar um alerta usando um nível de severidade.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse em **Alertas** e selecione **Novo Alerta**.  
  
4.  Na caixa de diálogo **Novo Alerta** , na caixa **Nome** , digite um nome para esse alerta.  
  
5.  Na lista **Tipo** , selecione **Alerta de evento do SQL Server**.  
  
6.  Em **Definição de alerta de evento**, na lista **Nome do banco de dados** , selecione um banco de dados para restringir o alerta a um banco de dados específico.  
  
7.  Em **Os alertas serão gerados com base em**, clique em **Severidade** e selecione a severidade específica que gerará o alerta.  
  
8.  Marque a caixa correspondente à caixa de seleção **Gerar alertas quando a mensagem contiver** para restringir o alerta a uma sequência de caracteres específica e digite uma palavra-chave ou uma cadeia de caracteres para o **Texto da mensagem**. O número máximo de caracteres é 100.  
  
9. Clique em **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-an-alert-using-severity-level"></a>Para criar um alerta usando um nível de severidade  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- adds an alert (Test Alert) that runs the Back up the AdventureWorks2012 Database job when fired   
    -- assumes that the message 55001 and the Back up the AdventureWorks2012 Database job already exist.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_add_alert  
        @name = N'Test Alert',  
        @message_id = 55001,   
       @severity = 0,   
       @notification_message = N'Error 55001 has occurred. The database will be backed up...',   
       @job_name = N'Back up the AdventureWorks2012 Database' ;  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_add_alert &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql).  
  
  
