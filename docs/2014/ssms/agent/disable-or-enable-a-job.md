---
title: Desabilitar ou habilitar um trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- stopping jobs
- disabling jobs
- SQL Server Agent jobs, disabling
- jobs [SQL Server Agent], disabling
ms.assetid: 5041261f-0c32-4d4a-8bee-59a6c16200dd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1fa9a2700bd2f6a9ce2b074b1633182fc30c9aa7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211413"
---
# <a name="disable-or-enable-a-job"></a>Disable or Enable a Job
  Este tópico descreve como desabilitar um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Quando um trabalho é desabilitado, ele não é excluído e pode ser habilitado novamente quando necessário.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para desabilitar ou habilitar um trabalho usando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-disable-or-enable-a-job"></a>Para desabilitar ou habilitar um trabalho  
  
1.  No Pesquisador de **objetos**, conecte-se a [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]uma instância do e expanda essa instância.  
  
2.  Expanda o **SQL Server Agent**.  
  
3.  Expanda **Trabalhos**e clique com o botão direito do mouse no trabalho que deseja desabilitar ou habilitar.  
  
4.  Para desabilitar um trabalho, clique em **Desabilitar**. Para habilitar um trabalho, clique em **Habilitar**.  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> Usando o Transact-SQL  
  
#### <a name="to-disable-or-enable-a-job"></a>Para desabilitar ou habilitar um trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- changes the name, description, and enables status of the job NightlyBackups.  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_job  
        @job_name = N'NightlyBackups',  
        @new_name = N'NightlyBackups -- Disabled',  
        @description = N'Nightly backups disabled during server migration.',  
        @enabled = 1 ;  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_update_job &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql).  
  
  
