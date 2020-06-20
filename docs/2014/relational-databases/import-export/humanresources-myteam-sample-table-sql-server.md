---
title: Tabela de exemplo HumanResources.myTeam (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- myTeam sample table [SQL Server]
- bulk importing [SQL Server], examples
- bulk exporting [SQL Server], examples
ms.assetid: 27da45a0-c1f4-4bf4-ab24-6196e80d3834
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 47b8990bfb211b12e97d02d2df77fd94d684ac8a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050467"
---
# <a name="humanresourcesmyteam-sample-table-sql-server"></a>Tabela de exemplo HumanResources.myTeam (SQL Server)
  Muitos dos exemplos de código em [Importando e exportando dados em massa](bulk-import-and-export-of-data-sql-server.md) exigem uma tabela de teste com finalidade especial denominada **myTeam**. Antes de poder executar os exemplos, você deve criar a tabela **myTeam** no esquema **HumanResources** do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
> [!NOTE]  
>  [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] é um dos bancos de dados de exemplo no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 A tabela **myTeam** contém as seguintes colunas.  
  
|Coluna|Tipo de dados|Nulidade|Descrição|  
|------------|---------------|-----------------|-----------------|  
|**EmployeeID**|`smallint`|Não nulo|Chave primária para as linhas. A ID de funcionário de um membro da minha equipe.|  
|**Nome**|`nvarchar(50)`|Não nulo|Nome de um membro de myTeam.|  
|**Título**|`nvarchar(50)`|Nullable|O cargo que o funcionário exerce na minha equipe.|  
|**Informações**|`nvarchar(50)`|Não nulo|Data e hora da última atualização da linha. (Padrão)|  
  
 **Para criar HumanResources.myTeam**  
  
-   Use as seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    ```  
    --Create HumanResources.MyTeam:   
    USE AdventureWorks;  
    GO  
    CREATE TABLE HumanResources.myTeam   
    (EmployeeID smallint NOT NULL,  
    Name nvarchar(50) NOT NULL,  
    Title nvarchar(50) NULL,  
    Background nvarchar(50) NOT NULL DEFAULT ''  
    );  
    GO  
    ```  
  
 **Para popular HumanResources.myTeam**  
  
-   Execute as seguintes instruções `INSERT` para popular a tabela com duas linhas:  
  
    ```  
    USE AdventureWorks;  
    GO  
    INSERT INTO HumanResources.myTeam(EmployeeID,Name,Title,Background)  
       VALUES(77,'Mia Doppleganger','Administrative Assistant','Microsoft Office');  
    GO  
    INSERT INTO HumanResources.myTeam(EmployeeID,Name,Title,Background)  
       VALUES(49,'Hirum Mollicat','I.T. Specialist','Report Writing and Data Mining');  
    GO  
    ```  
  
    > [!NOTE]  
    >  Essas instruções ignoram a quarta coluna, `Background`. Isso tem um valor padrão. Ignorar essa coluna faz com que essa instrução `INSERT` deixe a coluna em branco.  
  
## <a name="see-also"></a>Consulte Também  
 [Importação e exportação em massa de dados &#40;SQL Server&#41;](bulk-import-and-export-of-data-sql-server.md)  
  
  
