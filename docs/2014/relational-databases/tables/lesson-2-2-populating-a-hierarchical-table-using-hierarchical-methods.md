---
title: Populando uma tabela hierárquica usando métodos hierárquicos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- HierarchyID
helpviewer_keywords:
- HierarchyID
ms.assetid: 2c95fa60-5b8e-4a05-ac09-cffe2b05900a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0ec81ae3a078846ad9288fe75eab9fe30d547a4e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66110057"
---
# <a name="populating-a-hierarchical-table-using-hierarchical-methods"></a>Preenchendo uma tabela hierárquica utilizando métodos hierárquicos
  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] tem oito funcionários que trabalham no departamento de Marketing. A hierarquia dos funcionários é assim:  
  
 **Davi**, **EmployeeID** 6, é o Gerente de Marketing. Três especialistas em Marketing são subordinados a **Davi**:  
  
-   **Sara**, **EmployeeID** 46  
  
-   **Bruno**, **EmployeeID** 271  
  
-   **Julieta**, **EmployeeID** 119  
  
 A Assistente de Marketing **Valentina** , (**EmployeeID** 269), é subordinada a **Sara**, e a Assistente de Marketing **Marina** , (**EmployeeID** 272), é subordinada a **Bruno**.  
  
### <a name="to-insert-the-root-of-the-hierarchy-tree"></a>Para inserir a raiz da árvore de hierarquia  
  
1.  O exemplo a seguir insere **Davi** , o Gerente de Marketing, na tabela da raiz da hierarquia. A coluna **OrdLevel** é uma coluna calculada. Portanto, não faz parte da instrução INSERT. Este primeiro registro usa o método [GetRoot()](/sql/t-sql/data-types/getroot-database-engine) para popular o primeiro registro como a raiz da hierarquia.  
  
    ```  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES (hierarchyid::GetRoot(), 6, 'David', 'Marketing Manager') ;  
    GO  
    ```  
  
2.  Execute o seguinte código para examinar a linha inicial na tabela:  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
     [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    ```  
  
 Como na lição anterior, usamos o método `ToString()` para converter o tipo de dados `hierarchyid` em um formato mais facilmente entendido.  
  
### <a name="to-insert-a-subordinate-employee"></a>Para inserir um funcionário subordinado  
  
1.  **Sara** é subordinada a **Davi**. Para inserir o nó **de Sariya** , você deve criar um valor de **OrgNode** apropriado do `hierarchyid`tipo de dados. O código a seguir cria uma variável do tipo de dados `hierarchyid` e a popula com o valor OrgNode de raiz da tabela. Em seguida, usa essa variável com o método [GetDescendant()](/sql/t-sql/data-types/getdescendant-database-engine) para inserir a linha que é um nó subordinado. `GetDescendant` usa dois argumentos. Analise as seguintes opções para os valores de argumento:  
  
    -   Se o pai for o NULL, o `GetDescendant` retornará NULL.  
  
    -   Se o pai não for NULL, e child1 e child2 forem NULL, o `GetDescendant` retornará um filho de pai.  
  
    -   Se o pai e child1 forem NULL e child2 for NULL, o `GetDescendant` retornará um filho de pai maior que child1.  
  
    -   Se o pai e child2 não forem NULL e child1 for NULL, o `GetDescendant` retornará um filho de pai menor que child2.  
  
    -   Se o pai, child 1 e child 2 não forem NULL, o `GetDescendant` retornará um filho de pai maior que child1 e menor que child2.  
  
     O código a seguir usa os argumentos `(NULL, NULL)` do pai da raiz, pois ainda não há linhas na tabela exceto a raiz. Execute o seguinte código para inserir **Sara**:  
  
    ```  
    DECLARE @Manager hierarchyid   
    SELECT @Manager = hierarchyid::GetRoot()  
    FROM HumanResources.EmployeeOrg ;  
  
    INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
    VALUES  
    (@Manager.GetDescendant(NULL, NULL), 46, 'Sariya', 'Marketing Specialist') ;  
  
    ```  
  
2.  Repita a consulta do primeiro procedimento para consultar a tabela e verificar como as entradas são exibidas:  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    ```  
  
     [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    /1/          0x58    1        46         Sariya  Marketing Specialist  
    ```  
  
### <a name="to-create-a-procedure-for-entering-new-nodes"></a>Para criar um procedimento para inserir novos nós  
  
1.  Para simplificar a inserção de dados, crie o procedimento armazenado a seguir para adicionar funcionários à tabela **EmployeeOrg** . O procedimento aceita valores de entrada sobre o empregado sendo adicionado. Isso inclui o **EmployeeID** do gerente do novo funcionário, o número **EmployeeID** do novo funcionário, além de seu nome e cargo. O procedimento usa `GetDescendant()` e o método [GetAncestor()](/sql/t-sql/data-types/getancestor-database-engine) . Execute o seguinte código para criar o procedimento:  
  
    ```  
    CREATE PROC AddEmp(@mgrid int, @empid int, @e_name varchar(20), @title varchar(20))   
    AS   
    BEGIN  
       DECLARE @mOrgNode hierarchyid, @lc hierarchyid  
       SELECT @mOrgNode = OrgNode   
       FROM HumanResources.EmployeeOrg   
       WHERE EmployeeID = @mgrid  
       SET TRANSACTION ISOLATION LEVEL SERIALIZABLE  
       BEGIN TRANSACTION  
          SELECT @lc = max(OrgNode)   
          FROM HumanResources.EmployeeOrg   
          WHERE OrgNode.GetAncestor(1) =@mOrgNode ;  
  
          INSERT HumanResources.EmployeeOrg (OrgNode, EmployeeID, EmpName, Title)  
          VALUES(@mOrgNode.GetDescendant(@lc, NULL), @empid, @e_name, @title)  
       COMMIT  
    END ;  
    GO  
    ```  
  
2.  O exemplo a seguir adiciona os quatro funcionários restantes que são subordinados direta ou indiretamente a **Davi**.  
  
    ```  
    EXEC AddEmp 6, 271, 'John', 'Marketing Specialist' ;  
    EXEC AddEmp 6, 119, 'Jill', 'Marketing Specialist' ;  
    EXEC AddEmp 46, 269, 'Wanida', 'Marketing Assistant' ;  
    EXEC AddEmp 271, 272, 'Mary', 'Marketing Assistant' ;  
    ```  
  
3.  Novamente, execute a seguinte consulta para examinar as linhas na tabela **EmployeeOrg** :  
  
    ```  
    SELECT OrgNode.ToString() AS Text_OrgNode,   
    OrgNode, OrgLevel, EmployeeID, EmpName, Title   
    FROM HumanResources.EmployeeOrg ;  
    GO  
    ```  
  
     [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
    ```  
    Text_OrgNode OrgNode OrgLevel EmployeeID EmpName Title  
    ------------ ------- -------- ---------- ------- -----------------  
    /            Ox      0        6          David   Marketing Manager  
    /1/          0x58    1        46         Sariya  Marketing Specialist  
    /1/1/        0x5AC0  2        269        Wanida  Marketing Assistant  
    /2/          0x68    1        271        John    Marketing Specialist  
    /2/1/        0x6AC0  2        272        Mary    Marketing Assistant  
    /3/          0x78    1        119        Jill    Marketing Specialist  
    ```  
  
 Agora a tabela está totalmente populada com a organização de marketing.  
  
## <a name="next-task-in-lesson"></a>Próxima tarefa da lição  
 [Consultando uma tabela hierárquica por meio de métodos de hierarquia](lesson-2-3-querying-a-hierarchical-table-using-hierarchy-methods.md)  
  
  
