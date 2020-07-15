---
title: Criar um trabalho do SQL Server Agent para arquivar mensagens e eventos do Database Mail
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- archiving mail messages and attachments [SQL Server]
- removing mail messages and attachements
- Database Mail [SQL Server], archiving
- saving mail messages and attachments
ms.assetid: 8f8f0fba-f750-4533-9b76-a9cdbcdc3b14
author: stevestein
ms.author: sstein
ms.custom: seo-dt-2019
ms.openlocfilehash: 1cc39f3a2a849bd60cda71c5988eeb0cadcd9a88
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85737597"
---
# <a name="create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs"></a>Criar um trabalho do SQL Server Agent para arquivar mensagens do Database Mail e logs de eventos
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  Cópias de mensagens do Database Mail e seus anexos são retidos em tabelas **msdb** junto com o log de eventos do Database Mail. Periodicamente, convém reduzir o tamanho das tabelas e arquivar mensagens e eventos que não sejam mais necessários. Os procedimentos a seguir criam um trabalho do SQL Server Agent para automatizar o processo.  
  
-   **Antes de começar:**  , [Pré-requisitos](#Prerequisites), [Recomendações](#Recommendations), [Permissões](#Permissions)  
  
-   **Para mensagens e logs do Archive Database Mail usando:**  [SQL Server Agent](#Process_Overview)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
 As novas tabelas para armazenar os dados de arquivo morto devem estar localizadas em um banco de dados de arquivo morto especial. Alternativamente as linhas podem ser exportadas para um arquivo de texto.  
   
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
 No seu ambiente de produção, convém adicionar outras verificações de erros e enviar uma mensagem de email aos operadores, caso o trabalho falhe.  
  
  
###  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 É necessário ser membro da função de servidor fixa **sysadmin** para poder executar os procedimentos armazenados descritos neste tópico.  
  
  
###  <a name="overview-of-the-process"></a><a name="Process_Overview"></a> Visão geral do processo  
  
-   O primeiro procedimento cria um trabalho denominado Archive Database Mail com as etapas a seguir.  
  
    1.  Copie todas as mensagens das tabelas do Database Mail em uma nova tabela nomeada com o mês anterior, no formato **DBMailArchive_** _<year_month>_ .  
  
    2.  Copie os anexos das mensagens copiadas na primeira etapa, das tabelas do Database Mail em uma nova tabela nomeada com o mês anterior, no formato **DBMailArchive_Attachments_** _<year_month>_ .  
  
    3.  Copie os eventos do log de eventos do Database Mail referentes às mensagens copiadas na primeira etapa, das tabelas do Database Mail em uma nova tabela nomeada com o mês anterior, no formato **DBMailArchive_Log_** _<year_month>_ .  
  
    4.  Exclua os registros dos itens de correio transferidos das tabelas do Database Mail.  
  
    5.  Exclua os eventos referentes aos itens de correio transferidos do log de eventos do Database Mail.  
  
-   Agende o trabalho a ser executado periodicamente.  
  
  
## <a name="to-create-a-sql-server-agent-job"></a>Para criar um trabalho do SQL Server Agent  
  
1.  No Pesquisador de Objetos, expanda o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, clique com o botão direito do mouse em **Trabalhos**e clique em **Novo Trabalho**.  
  
2.  Na caixa de diálogo **Novo Trabalho** , na caixa **Nome** , digite **Archive Database Mail**.  
  
3.  Na caixa **Proprietário** , confirme que o proprietário é um membro da função de servidor fixa **sysadmin** .  
  
4.  Na caixa **Categoria** , clique em **Manutenção de Banco de Dados**.  
  
5.  Na caixa **Descrição** , digite **Archive Database Mail messages**e clique em **Etapas**.  

 [Visão geral](#Process_Overview)  
  
## <a name="to-create-a-step-to-archive-the-database-mail-messages"></a>Para criar uma etapa para arquivar as mensagens do Database Mail  
  
1.  Na página **Etapas** , clique em **Nova**.  
  
2.  Na caixa **Nome da etapa** , digite **Copy Database Mail Items**.  
  
3.  Na caixa **Tipo** , selecione **Transact-SQL script (T-SQL)** .  
  
4.  Na caixa **Banco de dados** , selecione **msdb**.  
  
5.  Na caixa **Comando** , digite a seguinte instrução para criar uma tabela nomeada com o mês anterior, contendo linhas anteriores à data de início do mês atual:  
  
    ```sql  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_' + @LastMonth + '] FROM sysmail_allitems WHERE send_request_date < ''' + @CopyDate +'''';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  Clique em **OK** para salvar a etapa.  
  
 [Visão geral](#Process_Overview)  
  
## <a name="to-create-a-step-to-archive-the-database-mail-attachments"></a>Para criar uma etapa para arquivar os anexos do Database Mail  
  
1.  Na página **Etapas** , clique em **Nova**.  
  
2.  Na caixa **Nome da etapa** , digite **Copy Database Mail Attachments**.  
  
3.  Na caixa **Tipo** , selecione **Transact-SQL script (T-SQL)** .  
  
4.  Na caixa **Banco de dados** , selecione **msdb**.  
  
5.  Na caixa **Comando** , digite a seguinte instrução para criar uma tabela de anexos nomeada com o mês anterior, contendo os anexos que correspondem às mensagens transferidas na etapa anterior:  
  
    ```sql  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_Attachments_' + @LastMonth + '] FROM sysmail_attachments   
     WHERE mailitem_id in (SELECT DISTINCT mailitem_id FROM [DBMailArchive_' + @LastMonth + '] )';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  Clique em **OK** para salvar a etapa.  
  
 [Visão geral](#Process_Overview)  
  
## <a name="to-create-a-step-to-archive-the-database-mail-log"></a>Para criar uma etapa para arquivar o log do Database Mail  
  
1.  Na página **Etapas** , clique em **Nova**.  
  
2.  Na caixa **Nome da etapa** , digite **Copy Database Mail Log**.  
  
3.  Na caixa **Tipo** , selecione **Transact-SQL script (T-SQL)** .  
  
4.  Na caixa **Banco de dados** , selecione **msdb**.  
  
5.  Na caixa **Comando** , digite a seguinte instrução para criar uma tabela de log nomeada com o mês anterior, contendo as entradas do log que correspondem às mensagens transferidas na etapa anterior:  
  
    ```sql  
    DECLARE @LastMonth nvarchar(12);  
    DECLARE @CopyDate nvarchar(20) ;  
    DECLARE @CreateTable nvarchar(250) ;  
    SET @LastMonth = (SELECT CAST(DATEPART(yyyy,GETDATE()) AS CHAR(4)) + '_' + CAST(DATEPART(mm,GETDATE())-1 AS varchar(2))) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime))  
    SET @CreateTable = 'SELECT * INTO msdb.dbo.[DBMailArchive_Log_' + @LastMonth + '] FROM sysmail_Event_Log   
     WHERE mailitem_id in (SELECT DISTINCT mailitem_id FROM [DBMailArchive_' + @LastMonth + '] )';  
    EXEC sp_executesql @CreateTable ;  
    ```  
  
6.  Clique em **OK** para salvar a etapa.  
  
 [Visão geral](#Process_Overview)  
  
## <a name="to-create-a-step-to-remove-the-archived-rows-from-database-mail"></a>Para criar uma etapa para remover as linhas arquivadas do Database Mail  
  
1.  Na página **Etapas** , clique em **Nova**.  
  
2.  Na caixa **Nome da etapa** , digite **Remove rows from Database Mail**.  
  
3.  Na caixa **Tipo** , selecione **Transact-SQL script (T-SQL)** .  
  
4.  Na caixa **Banco de dados** , selecione **msdb**.  
  
5.  Na caixa **Comando** , digite a seguinte instrução para remover as linhas anteriores ao mês atual das tabelas do Database Mail:  
  
    ```sql  
    DECLARE @CopyDate nvarchar(20) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime)) ;  
    EXECUTE msdb.dbo.sysmail_delete_mailitems_sp @sent_before = @CopyDate ;  
    ```  
  
6.  Clique em **OK** para salvar a etapa.  
  
 [Visão geral](#Process_Overview)  
  
## <a name="to-create-a-step-to-remove-the-archived-items-from-database-mail-event-log"></a>Para criar uma etapa para remover os itens arquivados do log de eventos do Database Mail  
  
1.  Na página **Etapas** , clique em **Nova**.  
  
2.  Na caixa **Nome da etapa** , digite **Remove rows from Database Mail event log**.  
  
3.  Na caixa **Tipo** , selecione **Transact-SQL script (T-SQL)** .  
  
4.  Na caixa **Comando** , digite a seguinte instrução para remover as linhas anteriores ao mês atual do log de eventos do Database Mail:  
  
    ```sql  
    DECLARE @CopyDate nvarchar(20) ;  
    SET @CopyDate = (SELECT CAST(CONVERT(char(8), CURRENT_TIMESTAMP- DATEPART(dd,GETDATE()-1), 112) AS datetime)) ;  
    EXECUTE msdb.dbo.sysmail_delete_log_sp @logged_before = @CopyDate ;  
    ```  
  
5.  Clique em **OK** para salvar a etapa.  
  
 [Visão geral](#Process_Overview)  
  
## <a name="to-schedule-the-job-to-run-periodically"></a>Para agendar o trabalho a ser executado periodicamente  
  
1.  Na caixa de diálogo **Novo Trabalho** , clique em **Agendas**.  
  
2.  Na página **Agendas** , clique em **Nova**.  
  
3.  Na caixa **Nome** , digite **Archive Database Mail**.  
  
4.  Na caixa **Tipo de agenda** , selecione **Recorrente**.  
  
5.  Na área **Frequência** , selecione as opções para executar o trabalho periodicamente; por exemplo, uma vez por mês.  
  
6.  Na área **Frequência diária**, selecione **Ocorre uma vez às \<time>** .  
  
7.  Verifique se as outras opções estão configuradas a seu gosto e clique em **OK** para salvar a agenda.  
  
8.  Clique em **OK** para salvar o trabalho.  
  
 [Visão geral](#Process_Overview)  
  
  
