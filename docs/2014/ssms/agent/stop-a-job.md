---
title: Parar um trabalho   Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
ms.assetid: 4249328a-24d8-4284-9d1d-7d04ed90e3d7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 78986e85dd8ee808f5fb621182d903a94bbc5eb7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067519"
---
# <a name="stop-a-job"></a>Stop a Job
  Este tópico descreve como interromper um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabalho do Agent. Um trabalho é uma série especificada de ações que o SQL Server Agent executa.  
  
-   **Antes de começar:** ,  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para interromper um trabalho usando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Se um trabalho estiver executando no momento uma etapa do tipo **CmdExec** ou **PowerShell**, o processo em execução (por exemplo, MyProgram.exe) será forçado a terminar prematuramente. Isso pode causar comportamento imprevisível, como manter abertos os arquivos em uso pelo processo.  
  
-   Em caso de trabalho multisservidor, uma instrução STOP para o trabalho é postada em todos os servidores de destino do trabalho.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-stop-a-job"></a>Para interromper um trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e a expanda.  
  
2.  Expanda **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho que deseja interromper e clique em **Parar Trabalho**.  
  
3.  Se desejar interromper vários trabalhos, clique com o botão direito do mouse em **Monitor de Atividade do Trabalho**e, depois, clique em **Exibir Atividade do Trabalho**. No Monitor de Atividade do Trabalho, selecione os trabalhos que você deseja interromper, clique com o botão direito do mouse em sua seleção e, depois, clique em **Parar Trabalhos**.  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> Usando o Transact-SQL  
  
### <a name="to-stop-a-job"></a>Para interromper um trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```sql
    -- stops a job named Weekly Sales Data Backup  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_stop_job  
        N'Weekly Sales Data Backup' ;  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_stop_job &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-stop-job-transact-sql).  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Usando SQL Server Management Objects  

### <a name="to-stop-a-job"></a>Para interromper um trabalho
  
 Chame o método `Stop` da classe `Job` usando uma linguagem de programação da sua escolha, como o Visual Basic, o Visual C# ou o PowerShell. Para obter mais informações, veja [SMO (SQL Server Management Objects)](https://msdn.microsoft.com/library/ms162169.aspx).  
