---
title: Modificar um procedimento armazenado | Microsoft Docs
description: Saiba como modificar um procedimento armazenado no SQL Server 2019 (15.x) usando o SQL Server Management Studio ou o Transact-SQL.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: conceptual
helpviewer_keywords:
- modifying stored procedures
- editing stored procedures
- stored procedures [SQL Server], modifying
ms.assetid: 13396239-6100-48ce-aa34-461358d99c92
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0137aec684b5c0e4b1ee1dfcaee07e9d7c32d3df
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475267"
---
# <a name="modify-a-stored-procedure"></a>Modificar um procedimento armazenado
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
    
##  <a name="this-topic-describes-how-to-modify-a-stored-procedure-in-sscurrent-by-using-ssmanstudiofull-or-tsql"></a><a name="Top"></a> Este tópico descreve como modificar um procedimento armazenado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Antes de começar:**  [Limitações e Restrições](#Restrictions), [Segurança](#Security)  
  
-   **Para alterar um procedimento usando:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] não podem ser modificados para serem procedimentos armazenados CLR e vice-versa.  
  
 Se a definição de procedimento anterior foi criada com WITH ENCRYPTION ou WITH RECOMPILE, essas opções estarão habilitadas somente se tiverem sido incluídas na instrução ALTER PROCEDURE.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER PROCEDURE no procedimento.  
  
##  <a name="how-to-modify-a-stored-procedure"></a><a name="Procedures"></a> Como modificar um procedimento armazenado  
 Você pode usar uma das seguintes opções:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para modificar um procedimento no Management Studio**  
  
1.  No Pesquisador de Objetos, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**, expanda o banco de dados ao qual pertence o procedimento e expanda **Programação**.  
  
3.  Expanda **Procedimentos Armazenados**, clique com o botão direito do mouse no procedimento a modificar e clique em **Modificar**.  
  
4.  Modifique o texto do procedimento armazenado.  
  
5.  Para testar a sintaxe, no menu **Consulta** , clique em **Analisar**.  
  
6.  Para salvar as modificações na definição do procedimento, no menu **Consulta** , clique em **Executar**.  
  
7.  Para salvar a definição do procedimento atualizada, como um script [!INCLUDE[tsql](../../includes/tsql-md.md)] , no menu **Arquivo** , clique em **Salvar como**. Aceite o nome de arquivo ou substitua-o por um nome novo e, então, clique em **Salvar**.  

> [!IMPORTANT]  
>  Valide todas as entradas de usuário. Não concatene a entrada de usuário antes de validá-la. Nunca execute um comando construído por uma entrada de usuário inválida.  
  
###  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para modificar um procedimento no Editor de Consultas**  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados** e o banco de dados ao qual o procedimento pertence. Ou, na barra de ferramentas, selecione o banco de dados na lista de bancos de dados disponíveis. Neste exemplo, selecione o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
3.  No menu **Arquivo** , clique em **Nova Consulta**.  
  
4.  Copie e cole o exemplo a seguir no editor de consultas. O exemplo cria o procedimento `uspVendorAllInfo` , que retorna os nomes de todos os fornecedores no banco de dados [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] , os produtos que eles fornecem, suas classificações de crédito e sua disponibilidade.  
  
    ```  
  
    IF OBJECT_ID ( 'Purchasing.uspVendorAllInfo', 'P' ) IS NOT NULL   
        DROP PROCEDURE Purchasing.uspVendorAllInfo;  
    GO  
    CREATE PROCEDURE Purchasing.uspVendorAllInfo  
    WITH EXECUTE AS CALLER  
    AS  
        SET NOCOUNT ON;  
        SELECT v.Name AS Vendor, p.Name AS 'Product name',   
          v.CreditRating AS 'Rating',   
          v.ActiveFlag AS Availability  
        FROM Purchasing.Vendor v   
        INNER JOIN Purchasing.ProductVendor pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product p  
          ON pv.ProductID = p.ProductID   
        ORDER BY v.Name ASC;  
    GO  
  
    ```  
  
5.  No menu **Arquivo** , clique em **Nova Consulta**.  
  
6.  Copie e cole o exemplo a seguir no editor de consultas. O exemplo modifica o procedimento `uspVendorAllInfo` . A cláusula EXECUTE AS CALLER é removida e o corpo do procedimento é modificado para retornar apenas os fornecedores que fornecem o produto especificado. As funções `LEFT` e `CASE` personalizam a aparência do conjunto de resultados.  
  
    ```  
    ALTER PROCEDURE Purchasing.uspVendorAllInfo  
        @Product varchar(25)   
    AS  
        SET NOCOUNT ON;  
        SELECT LEFT(v.Name, 25) AS Vendor, LEFT(p.Name, 25) AS 'Product name',   
        'Rating' = CASE v.CreditRating   
            WHEN 1 THEN 'Superior'  
            WHEN 2 THEN 'Excellent'  
            WHEN 3 THEN 'Above average'  
            WHEN 4 THEN 'Average'  
            WHEN 5 THEN 'Below average'  
            ELSE 'No rating'  
            END  
        , Availability = CASE v.ActiveFlag  
            WHEN 1 THEN 'Yes'  
            ELSE 'No'  
            END  
        FROM Purchasing.Vendor AS v   
        INNER JOIN Purchasing.ProductVendor AS pv  
          ON v.BusinessEntityID = pv.BusinessEntityID   
        INNER JOIN Production.Product AS p   
          ON pv.ProductID = p.ProductID   
        WHERE p.Name LIKE @Product  
        ORDER BY v.Name ASC;  
    GO  
  
    ```  
  
7.  Para salvar as modificações na definição do procedimento, no menu **Consulta** , clique em **Executar**.  
  
8.  Para salvar a definição do procedimento atualizada, como um script [!INCLUDE[tsql](../../includes/tsql-md.md)] , no menu **Arquivo** , clique em **Salvar como**. Aceite o nome de arquivo ou substitua-o por um nome novo e, então, clique em **Salvar**.  
  
9. Para executar o procedimento armazenado modificado, execute o exemplo a seguir.  
  
    ```  
    EXEC Purchasing.uspVendorAllInfo N'LL Crankarm';  
    GO  
  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)  
  
  
