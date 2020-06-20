---
title: Modificar um Trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- modifying jobs
- SQL Server Agent jobs, modifying
ms.assetid: dd5e5f20-20c4-4ab9-a19a-db87577dcd43
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0d25830ad119a1f5f344a4dcf318c35bee5f86ca
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062191"
---
# <a name="modify-a-job"></a>Modify a Job
  Este tópico descreve como alterar as propriedades de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabalhos do Agent no usando [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , [!INCLUDE[tsql](../../includes/tsql-md.md)] ou SQL Server Management Objects.  
  
 **Neste tópico**  
  
-   **Antes de começar:** ,  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para modificar um trabalho, usando:**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
 Um trabalho mestre do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent não pode ser destino em ambos os servidores, local e remoto.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
 A menos que seja membro da função de servidor fixa **sysadmin** , você poderá modificar somente trabalhos de sua propriedade. Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](implement-sql-server-agent-security.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMS"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-modify-a-job"></a>Para modificar um trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e a expanda.  
  
2.  Expanda o **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse no trabalho que deseja modificar e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Trabalho** , atualize as propriedades, etapas, agenda, alertas e notificações do trabalho, usando as páginas correspondentes.  
  
##  <a name="using-transact-sql"></a><a name="TSQL"></a> Usando o Transact-SQL  
  
#### <a name="to-modify-a-job"></a>Para modificar um trabalho  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do Mecanismo de Banco de Dados e expanda-a.  
  
2.  Na barra de ferramentas, clique em **Nova Consulta**.  
  
3.  Na janela de consulta, use os procedimentos armazenados do sistema a seguir para modificar um trabalho.  
  
    -   Execute [sp_update_job &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql) para alterar os atributos de um trabalho.  
  
    -   Execute [sp_update_schedule &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-schedule-transact-sql) para alterar os detalhes de agendamento de uma definição de trabalho.  
  
    -   Execute [sp_add_jobstep &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql) para adicionar novas etapas de trabalho.  
  
    -   Execute [sp_update_jobstep &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql) para alterar as etapas de trabalho pré-existentes.  
  
    -   Execute [sp_delete_jobstep &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-delete-jobstep-transact-sql) para remover uma etapa de trabalho de um trabalho.  
  
    -   Procedimentos armazenados adicionais para modificar qualquer trabalho mestre do SQL Server Agent:  
  
        -   Execute [sp_delete_jobserver &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-delete-jobserver-transact-sql) para excluir um servidor atualmente associado a um trabalho.  
  
        -   Execute [sp_add_jobserver &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql) associe um servidor ao trabalho atual.  
  
##  <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Usando SQL Server Management Objects  
 **Para modificar um trabalho**  
  
 Use a classe `Job` usando uma linguagem de programação da sua escolha, como o Visual Basic, o Visual C# ou o PowerShell. Para obter mais informações, veja [SMO (SQL Server Management Objects)](https://msdn.microsoft.com/library/ms162169.aspx).  
  
  
