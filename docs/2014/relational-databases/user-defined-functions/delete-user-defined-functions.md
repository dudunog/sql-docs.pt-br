---
title: Excluir funções definidas pelo usuário | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: db1d668a-23b7-4757-a9c5-1bd848ba7f6d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f6c2580e17c204b534ec4c8ebadec3a1e992a4d6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68196457"
---
# <a name="delete-user-defined-functions"></a>Excluir funções definidas pelo usuário
  Você pode excluir (remover) funções definidas pelo usuário no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para excluir uma função definida pelo usuário, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Você não poderá excluir a função se houver funções Transact-SQL ou exibições no banco de dados que referenciem essa função e forem criadas usando SCHEMABINDING, ou se houver colunas computadas, restrições CHECK ou DEFAULT que referenciem a função.  
  
-   Você não poderá excluir a função se houver colunas computadas que referenciem essa função e tenham sido indexadas.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer permissão ALTER no esquema ao qual a função pertence ou permissão CONTROL na função.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-delete-a-user-defined-function"></a>Para excluir uma função definida pelo usuário  
  
1.  Clique no sinal de mais ao lado do banco de dados que contém a função que você deseja modificar.  
  
2.  Clique no sinal de mais ao lado da pasta **Programação** .  
  
3.  Clique no sinal de mais ao lado da pasta que contém a função que você deseja modificar:  
  
    -   Table-valued Function  
  
    -   Função de valor escalar  
  
    -   Função de agregação  
  
4.  Clique com o botão direito do mouse na função a ser excluída e selecione **Excluir**.  
  
5.  Na caixa de diálogo **Excluir Objeto** , clique em **OK**.  
  
    > [!IMPORTANT]  
    >  Clique em **Mostrar dependências** na caixa de diálogo **excluir objeto** para abrir a caixa de diálogo _function_name_**dependências** . Isso mostrará todos os objetos que dependem da função e todos os objetos dos quais a função depende.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-delete-a-user-defined-function"></a>Para excluir uma função definida pelo usuário  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    -- creates function called "Sales.ufn_SalesByStore"  
    USE AdventureWorks2012;  
    GO  
    CREATE FUNCTION Sales.ufn_SalesByStore (@storeid int)  
    RETURNS TABLE  
    AS  
    RETURN   
    (  
        SELECT P.ProductID, P.Name, SUM(SD.LineTotal) AS 'Total'  
        FROM Production.Product AS P   
        JOIN Sales.SalesOrderDetail AS SD ON SD.ProductID = P.ProductID  
        JOIN Sales.SalesOrderHeader AS SH ON SH.SalesOrderID = SD.SalesOrderID  
        JOIN Sales.Customer AS C ON SH.CustomerID = C.CustomerID  
        WHERE C.StoreID = @storeid  
        GROUP BY P.ProductID, P.Name  
    );  
    GO  
    ```  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    -- determines if function exists in database  
    IF OBJECT_ID (N'Sales.fn_SalesByStore', N'IF') IS NOT NULL  
    -- deletes function  
        DROP FUNCTION Sales.fn_SalesByStore;  
    GO  
    ```  
  
 Para obter mais informações, consulte [DROP FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-function-transact-sql).  
  
  
