---
title: Desabilitar ou reativar um alerta | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, alerts
- alerts [SQL Server], reactivating
- deleting alerts
- canceling alerts
- dropping alerts
- disabling alerts
- alerts [SQL Server], disabling
- reactivating alerts
- removing alerts
ms.assetid: 4cb37dc6-1134-405d-8590-58b44dcf63b2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 638ce62d8dd12764681c2b65a271d9ae13bb5d83
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68189336"
---
# <a name="disable-or-reactivate-an-alert"></a>Disable or Reactivate an Alert
  Este tópico descreve como desabilitar ou reativar um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] alerta do Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)]o.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para desabilitar ou reativar um alerta usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem editar as informações em um alerta. Deve ser concedida a outros usuários a função de banco de dados fixa **SQLAgentOperatorRole** no banco de dados **msdb** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-disable-or-reactivate-an-alert"></a>Para desabilitar ou reativar um alerta  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor que contém o alerta que você deseja desabilitar ou reativar.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique no sinal de adição para expandir a pasta **Alertas** .  
  
4.  Clique com o botão direito do mouse no alerta que deseja habilitar e selecione **Habilitar** . Para desabilitar um alerta, clique com o botão direito do mouse no alerta que deseja desabilitar e selecione **Desabilitar**.  
  
5.  É exibida a caixa de diálogo **Desabilitar Alerta** ou **Habilitar Alerta** , mostrando o status do processo. Quando terminar, clique em **Fechar**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-disable-or-reactivate-an-alert"></a>Para desabilitar ou reativar um alerta  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- changes the enabled setting of Test Alert to 0  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_update_alert  
        @name = N'Test Alert',  
        @enabled = 0 ;  
    GO  
    ```  
  
 Para obter mais informações, consulte [sp_update_alert &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-update-alert-transact-sql).  
  
  
