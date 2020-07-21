---
title: MSSQLSERVER_4104 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 4104 (Database Engine error)
ms.assetid: 52dc32d8-97ad-4ef0-834d-2e68f215d007
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 5125fd84b8eed24c957bc3ec2123d545bddc23c8
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86551491"
---
# <a name="mssqlserver_4104"></a>MSSQLSERVER_4104
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|4104|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|ALG_MULTI_ID_BAD|  
|Texto da mensagem|Não foi possível associar o identificador de várias partes "%.*ls".|  
  
## <a name="explanation"></a>Explicação  
 O nome de uma entidade no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é referenciado como seu *identificador*. Use identificadores sempre que referenciar entidades, por exemplo, especificando nomes de coluna e tabela em uma consulta. Um identificador de várias partes contém um ou mais qualificadores como um prefixo do identificador. Por exemplo, um identificador de tabela pode ter como prefixo qualificadores como o nome do banco de dados e o nome do esquema no qual a tabela está contida, ou um identificador de coluna pode ter como prefixo qualificadores como um nome ou alias de tabela.  
  
 O erro 4104 indica que o identificador de várias partes especificado não pôde ser mapeado para uma entidade existente. Esse erro pode ser retornado nas seguintes condições:  
  
-   O qualificador fornecido como prefixo para um nome de coluna não corresponde a nenhum nome de tabela ou alias usado na consulta.  
  
     Por exemplo, a instrução a seguir usa um alias de tabela (`Dept`) como prefixo de coluna, mas esse alias não é referenciado na cláusula FROM.  
  
    ```  
    SELECT Dept.Name FROM HumanResources.Department;  
    ```  
  
     Nas instruções a seguir, um identificador de coluna de várias partes `TableB.KeyCol` é especificado na cláusula WHERE como parte de uma condição JOIN entre duas tabelas, no entanto, `TableB` não é referenciado explicitamente na consulta.  
  
    ```  
    DELETE FROM TableA WHERE TableA.KeyCol = TableB.KeyCol;  
    ```  
  
    ```  
    SELECT 'X' FROM TableA WHERE TableB.KeyCol = TableA.KeyCol;  
    ```  
  
-   Um nome de alias para a tabela é fornecido na cláusula FROM, mas o qualificador fornecido para uma coluna é o nome da tabela. Por exemplo, a instrução a seguir usa o nome de tabela `Department` como prefixo de coluna; entretanto, a tabela tem um alias (`Dept`) referenciado na cláusula FROM.  
  
    ```  
    SELECT Department.Name FROM HumanResources.Department AS Dept;  
    ```  
  
     Quando um alias é usado, o nome de tabela não pode ser usado em nenhum outro lugar na instrução.  
  
-   O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não pode determinar se o identificador de várias partes se refere a uma coluna com um prefixo de tabela ou a uma propriedade de um tipo de dados CLR definido pelo usuário (UDT) com prefixo de uma coluna. Isso ocorre porque as propriedades de colunas UDT são referenciadas com o uso do separador de ponto (.) entre o nome da coluna e o nome da propriedade, da mesma maneira que um nome de coluna recebe um nome de tabela como prefixo. O exemplo a seguir cria duas tabelas, `a` e `b`. A tabela `b` contém a coluna `a`, que usa um `dbo.myudt2` CLR UDT como seu tipo de dados. A SELECT instrução contém um identificador de várias partes `a.c2`.  
  
    ```  
    CREATE TABLE a (c2 int);   
    GO  
    ```  
  
    ```  
    CREATE TABLE b (a dbo.myudt2);   
    GO  
    ```  
  
    ```  
    SELECT a.c2 FROM a, b;   
    ```  
  
     Pressupondo que UDT `myudt2` não tenha uma propriedade denominada `c2`, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não poderá determinar se o identificador se `a.c2`refere a uma coluna `c2` na tabela `a` ou à coluna `a`, propriedade `c2` na tabela `b`.  
  
## <a name="user-action"></a>Ação do usuário  
  
-   Compare os prefixos de coluna com os nomes de tabela ou de alias especificados na cláusula FROM da consulta. Se um alias for definido para um nome de tabela na cláusula FROM, você só poderá usar esse alias como um qualificador para colunas associadas à tabela.  
  
     As instruções acima que referenciam a tabela `HumanResources.Department` podem ser corrigidas da seguinte forma:  
  
    ```  
    SELECT Dept.Name FROM HumanResources.Department AS Dept;  
    GO  
    ```  
  
    ```  
    SELECT Department.Name FROM HumanResources.Department;  
    GO  
    ```  
  
-   Verifique se todas as tabelas são especificadas na consulta e se são condições JOIN entre tabelas são especificadas corretamente. A instrução DELETE acima pode ser corrigida da seguinte forma:  
  
    ```  
    DELETE FROM dbo.TableA  
    WHERE TableA.KeyCol = (SELECT TableB.KeyCol   
                            FROM TableB   
                            WHERE TableA.KeyCol = TableB.KeyCol);  
    GO  
    ```  
  
     A instrução SELECT acima para `TableA` pode ser corrigida da seguinte forma:  
  
    ```  
    SELECT 'X' FROM TableA, TableB WHERE TableB.KeyCol = TableA.KeyCol;  
    ```  
  
     ou  
  
    ```  
    SELECT 'X' FROM TableA INNER JOIN TableB ON TableB.KeyCol = TableA.KeyCol;  
    ```  
  
-   Use nomes exclusivos, claramente definidos como identificadores. Isso facilitará a leitura e a manutenção do código e também minimizará o risco de referências ambíguas para várias entidades.  
  
## <a name="see-also"></a>Consulte Também  
 [MSSQLSERVER_107](mssqlserver-107-database-engine-error.md)   
 [Identificadores de banco de dados](../databases/database-identifiers.md)  
  
  
