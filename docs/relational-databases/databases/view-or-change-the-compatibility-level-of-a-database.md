---
title: Exibir ou alterar o nível de compatibilidade de um banco de dados | Microsoft Docs
description: Saiba como exibir ou alterar o nível de compatibilidade de um banco de dados no SQL Server usando o SQL Server Management Studio ou Transact-SQL.
ms.custom: ''
ms.date: 11/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- compatibility levels [SQL Server], viewing
- compatibility [SQL Server], databases
- compatibility levels [SQL Server], changing
ms.assetid: 579867ec-57cb-4cb8-af35-9688c1e9e15d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d43fb7c4138c0070b3b3ca36c16e480f9d798683
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85727548"
---
# <a name="view-or-change-the-compatibility-level-of-a-database"></a>Exibir ou alterar o nível de compatibilidade de um banco de dados
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Este tópico descreve como exibir ou alterar o nível de compatibilidade de um banco de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Antes de alterar o nível de compatibilidade de um banco de dados, você deve entender o impacto da alteração em seus aplicativos. Para obter mais informações, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir ou alterar o nível de compatibilidade de um banco de dados usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no banco de dados.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-compatibility-level-of-a-database"></a>Para exibir ou alterar o nível de compatibilidade de um banco de dados  
  
1.  Depois de conectar-se à instância adequada do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no Pesquisador de Objetos, clique no nome do servidor.  
  
2.  Expanda **Bancos de Dados**e, dependendo do banco de dados, selecione um banco de dados de usuário ou expanda **Bancos de Dados do Sistema** e selecione um banco de dados do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados e clique em **Propriedades**.  
  
     A caixa de diálogo **Database Properties** abre.  
  
4.  No painel **Selecionar uma página** , clique em **Opções**.  
  
     O nível de compatibilidade atual é exibido na caixa de listagem **Nível de compatibilidade** .  
  
5.  Para alterar o nível de compatibilidade, selecione uma opção diferente da lista. As opções disponíveis para as diferentes versões do [!INCLUDE[ssde_md](../../includes/ssde_md.md)] estão listadas na página [Nível de compatibilidade de ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md#supported-dbcompats).  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-view-the-compatibility-level-of-a-database"></a>Para exibir as informações sobre o nível de compatibilidade de um banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo retorna o nível de compatibilidade do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT compatibility_level  
FROM sys.databases WHERE name = 'AdventureWorks2012';  
GO  
```  
  
#### <a name="to-change-the-compatibility-level-of-a-database"></a>Para alterar o nível de compatibilidade de um banco de dados  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo altera o nível de compatibilidade do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] para `120`, que é o nível de compatibilidade do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
```sql  
ALTER DATABASE AdventureWorks2012  
SET COMPATIBILITY_LEVEL = 120;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também
 [ALTER DATABASE &#40;Transact-SQL&#41; Nível de Compatibilidade](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)
