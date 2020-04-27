---
title: Desabilitar restrições de verificação com instruções INSERT e UPDATE | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- CHECK constraints, disabling
- constraints [SQL Server], disabling
- disabling constraints
- constraints [SQL Server], check
ms.assetid: c7287ad1-50d2-4e80-bc0c-b5570f7e5f69
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bd49c3264857a92a9ca029a25894a5afdbeab381
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62760986"
---
# <a name="disable-check-constraints-with-insert-and-update-statements"></a>Desabilitar restrições de verificação com instruções INSERT e UPDATE
  Você pode desabilitar uma restrição de verificação para transações INSERT e UPDATE no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Depois de desabilitar as restrições de verificação, as inserções ou atualizações futuras na coluna não serão validadas em relação às condições de restrição. Use esta opção se você souber que novos dados violarão a restrição existente ou se a restrição se aplicar somente aos dados que já estão no banco de dados.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para desabilitar uma restrição de verificação para instruções INSERT e UPDATE usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-disable-a-check-constraint-for-insert-and-update-statements"></a>Para desabilitar uma restrição de verificação para instruções INSERT e UPDATE  
  
1.  No **Pesquisador de Objetos**, expanda a tabela com a restrição e expanda a pasta **Restrições** .  
  
2.  Clique com o botão direito do mouse na restrição e selecione **Modificar**.  
  
3.  Na grade, em **Designer de Tabela**, clique em **Impor para INSERTs e UPDATEs** e selecione **Não** no menu suspenso.  
  
4.  Clique em **fechar**  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-disable-a-check-constraint-for-insert-and-update-statements"></a>Para desabilitar uma restrição de verificação para instruções INSERT e UPDATE  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole os exemplos a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE Purchasing.PurchaseOrderHeader  
    NOCHECK CONSTRAINT CK_PurchaseOrderHeader_Freight;   
    GO  
    ```  
  
 Para obter mais informações, veja [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
###  <a name="TsqlExample"></a>  
