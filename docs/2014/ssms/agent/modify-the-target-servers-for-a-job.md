---
title: Modificar os servidores de destino de um trabalho | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- modifying target servers
- SQL Server Agent jobs, target servers
- target servers [SQL Server], modifying
ms.assetid: 9dbe24f2-acec-4aa2-920c-e8e96efa18e4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a97fd3892e74b16c844867f88bc7d72fedc46d20
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62720376"
---
# <a name="modify-the-target-servers-for-a-job"></a>Modify the Target Servers for a Job
  Este tópico descreve como alterar os servidores de destino para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabalhos do Agent [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]ou o.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para modificar os servidores de destino de um trabalho usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Por padrão, os membros da função de servidor fixa sysadmin podem executar esse procedimento armazenado. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do SQL Server Agent no banco de dados msdb:  
  
1.  `SQLAgentUserRole`  
  
2.  `SQLAgentReaderRole`  
  
3.  SQLAgentOperatorRole  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-modify-the-target-servers-for-a-job"></a>Para modificar os servidores de destino de um trabalho  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e a expanda.  
  
2.  Expanda **SQL Server Agent**, expanda **Trabalhos**, clique com o botão direito do mouse em um trabalho e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Trabalho** , selecione a página **Destinos**e clique em **Servidor local de destino**ou **Vários servidores de destino**.  
  
     Se optar por **Vários servidores de destino**, designe os servidores a serem destino do trabalho, marcando a caixa à esquerda do nome do servidor. Verifique se as caixas de seleção dos servidores que não devem ser destino do trabalho estão desmarcadas.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-modify-the-target-servers-for-a-job"></a>Para modificar os servidores de destino de um trabalho  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo atribui o trabalho multisservidor Backups de Vendas Semanais ao servidor SEATTLE2.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_jobserver  
    @job_name = N'Weekly Sales Backups',   
    @server_name = N'SEATTLE2' ;   
GO  
  
```  
  
 Para obter mais informações, consulte [sp_add_jobserver &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-add-jobserver-transact-sql).  
  
## <a name="see-also"></a>Consulte Também  
 [Administração automatizada em toda a empresa](automated-administration-across-an-enterprise.md)  
  
  
