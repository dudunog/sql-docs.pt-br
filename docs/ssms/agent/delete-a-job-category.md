---
description: Excluir uma categoria de trabalho
title: Excluir uma categoria de trabalho
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- deleting job category
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- removing job category
ms.assetid: 47a7640b-20b3-4639-ab37-b6fc73575e6c
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: c78142b6608ccce1d633faa08ca499383d8416de
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97424709"
---
# <a name="delete-a-job-category"></a>Excluir uma categoria de trabalho
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> Atualmente, na [Instância Gerenciada de SQL do Azure](/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obter detalhes.

Este tópico descreve como excluir uma categoria de trabalho do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o [!INCLUDE[tsql](../../includes/tsql-md.md)] ou o SQL Server Management Objects.  
  
As categorias de trabalho ajudam a organizar os trabalhos de modo a facilitar sua filtragem e agrupamento. Por exemplo, você pode organizar todos os seus trabalhos de backup de banco de dados na categoria Manutenção de Banco de Dados.  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>Limitações e Restrições  
Quando se exclui uma categoria de trabalho definida pelo usuário, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent solicita que os trabalhos a ela atribuídos sejam reatribuídos a outra categoria. Você só pode excluir categorias de trabalho definidas pelo usuário.  
  
### <a name="security"></a><a name="Security"></a>Segurança  
Para obter informações detalhadas, consulte [Implementar a segurança do SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMS"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-delete-a-job-category"></a>Para excluir uma categoria de trabalho  
  
1.  No **Pesquisador de Objetos**, clique no sinal de adição para expandir o servidor no qual você deseja excluir uma categoria de trabalho.  
  
2.  Clique no sinal de adição para expandir o **SQL Server Agent**.  
  
3.  Clique com o botão direito do mouse na pasta **Trabalhos** e selecione **Gerenciar Categorias de Trabalho**.  
  
4.  Na caixa de diálogo **Gerenciar Categorias de Trabalho**_server\_name_, selecione a categoria de trabalho a ser excluída.  
  
5.  Clique em **Excluir**.  
  
6.  Na caixa de diálogo **Categorias de Trabalho** , clique em **Sim**.  
  
7.  Feche a caixa de diálogo **Gerenciar Categorias de Trabalho**_server\_name_.  
  
## <a name="using-transact-sql"></a><a name="TSQL"></a>Usando Transact-SQL  
  
#### <a name="to-delete-a-job-category"></a>Para excluir uma categoria de trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde_md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- deletes the job category named AdminJobs.  
    USE msdb ;  
    GO   
    EXEC dbo.sp_delete_category  
        @name = N'AdminJobs',  
        @class = N'JOB' ;  
    GO  
    ```  
  
Para obter mais informações, consulte [sp_delete_category (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-delete-category-transact-sql.md).  
  
## <a name="using-sql-server-management-objects"></a><a name="SMO"></a>Usando o SQL Server Management Objects  
**Para excluir uma categoria de trabalho**  
  
Chame a classe **JobCategory** com uma linguagem de programação à sua escolha, como Visual Basic, Visual C# ou PowerShell.  
