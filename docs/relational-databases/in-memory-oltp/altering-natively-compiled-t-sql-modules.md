---
title: Alterando módulos T-SQL compilados nativamente | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 010318a0-6807-47c3-8ecc-bb7cb60513f0
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6979d05d29b151a34edfe1c220c9d9a4d3046359
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "73983006"
---
# <a name="altering-natively-compiled-t-sql-modules"></a>Altering Natively Compiled T-SQL Modules
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e posterior) e no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], você pode executar operações `ALTER` em procedimentos armazenados compilados nativamente e em outros módulos do [!INCLUDE[tsql](../../includes/tsql-md.md)] compilados nativamente, como UDFs escalares e gatilhos, usando a instrução `ALTER`.  
  
Ao executar `ALTER` em um módulo do [!INCLUDE[tsql](../../includes/tsql-md.md)] compilado nativamente, o módulo é recompilado usando uma nova definição. Enquanto a recompilação estiver em andamento, a versão antiga do módulo continuará disponível para execução. Uma vez concluída a compilação, as execuções de módulo serão descarregadas e a nova versão do módulo será instalada. Ao alterar um módulo do [!INCLUDE[tsql](../../includes/tsql-md.md)] compilado nativamente, é possível modificar as opções a seguir.  
  
-   parâmetros  
-   EXECUTE AS  
-   TRANSACTION ISOLATION LEVEL  
-   LANGUAGE  
-   DATEFIRST  
-   DATEFORMAT  
-   DELAYED_DURABILITY  
  
> [!NOTE]  
> Os módulos do [!INCLUDE[tsql](../../includes/tsql-md.md)] compilados nativamente não podem ser convertidos em módulos compilados não nativamente. Os módulos do T-SQL compilados não nativamente não podem ser convertidos em módulos compilados nativamente.  
  
Para obter mais informações sobre a funcionalidade e a sintaxe do `ALTER PROCEDURE`, consulte [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md).  
  
É possível executar [sp_recompile](../../relational-databases/system-stored-procedures/sp-recompile-transact-sql.md) em módulos do [!INCLUDE[tsql](../../includes/tsql-md.md)] compilados nativamente, o que faz com que o módulo recompile na próxima execução.  
  
## <a name="example"></a>Exemplo  
O exemplo a seguir cria uma tabela com otimização de memória (T1) e um procedimento armazenado compilado nativamente (usp_1) que seleciona todas as colunas de T1. Em seguida, usp_1 é alterado para remover a cláusula `EXECUTE AS`, alterar `LANGUAGE` e selecionar apenas uma coluna (C1) de T1.  
  
```sql  
CREATE TABLE [dbo].[T1] (  
  [c1] [int] NOT NULL,  
  [c2] [float] NOT NULL,  
  CONSTRAINT [PK_T1] PRIMARY KEY NONCLUSTERED ([c1])  
  ) WITH ( MEMORY_OPTIMIZED = ON , DURABILITY = SCHEMA_AND_DATA )  
GO  
  
CREATE PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english'  
)  
   SELECT c1, c2 FROM dbo.T1  
END  
GO  
  
ALTER PROCEDURE [dbo].[usp_1]  
WITH NATIVE_COMPILATION, SCHEMABINDING  
AS BEGIN ATOMIC WITH  
(  
 TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'Dutch'  
)  
   SELECT c1 FROM dbo.T1  
END  
GO    
```   
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados compilados nativamente](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)    
