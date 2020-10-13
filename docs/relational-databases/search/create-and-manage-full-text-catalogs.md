---
description: Criar e gerenciar catálogos de texto completo
title: Criar e gerenciar catálogos de texto completo | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text catalogs [SQL Server], creating
- full-text search [SQL Server], using SQL Server Management Studio
ms.assetid: 824b7131-44a6-4815-89e6-62b7bab060e3
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f95811113261f10701e0fcfc41c70e348891f6a9
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91868095"
---
# <a name="create-and-manage-full-text-catalogs"></a>Criar e gerenciar catálogos de texto completo
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
Um catálogo de texto completo é um contêiner lógico para um grupo de índices de texto completo. É necessário criar um catálogo de texto completo antes de criar um índice de texto completo.

Um catálogo de texto completo é um objeto virtual que não pertence a nenhum grupo de arquivos.
  
##  <a name="create-a-full-text-catalog"></a><a name="creating"></a> Criar um catálogo de texto completo  

### <a name="create-a-full-text-catalog-with-transact-sql"></a>Criar um catálogo de texto completo com Transact-SQL
Use [CREATE FULLTEXT CATALOG](../../t-sql/statements/create-fulltext-catalog-transact-sql.md). Por exemplo:

```sql 
USE AdventureWorks;  
GO  
CREATE FULLTEXT CATALOG ftCatalog AS DEFAULT;  
GO  
``` 

### <a name="create-a-full-text-catalog-with-management-studio"></a>Criar um catálogo de texto completo com o Management Studio
1.  No Pesquisador de Objetos, expanda o servidor, **Bancos de Dados**e o banco de dados em que deseja criar um catálogo de texto completo.  
  
2.  Expanda **Armazenamento**e clique com o botão direito do mouse em **Catálogos de Texto Completo**.  
  
3.  Selecione **Novo Catálogo de Texto Completo**.  
  
4.  Na caixa de diálogo **Novo Catálogo de Texto Completo** , especifique as informações do catálogo que você está recriando. Para obter mais informações, veja [Catálogo de texto completo novo &#40;Página Geral&#41;](../../t-sql/statements/create-fulltext-catalog-transact-sql.md).  
  
    > [!NOTE]  
    >  Os identificadores de catálogos de texto completo começam em 00005 e são incrementados em um para cada novo catálogo criado.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

##  <a name="get-the-properties-of-a-full-text-catalog"></a><a name="props"></a> Obter as propriedades de um catálogo de texto completo  
Use a função [!INCLUDE[tsql](../../includes/tsql-md.md)]**FULLTEXTCATALOGPROPERTY** para obter o valor de várias propriedades relacionadas a catálogos de texto completo. Para obter mais informações, consulte [FULLTEXTCATALOGPROPERTY](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md).

Por exemplo, execute a consulta a seguir para obter a contagem de índices no catálogo de texto completo `Catalog1`.

```sql 
USE <database>;  
GO  
SELECT fulltextcatalogproperty('Catalog1', 'ItemCount');  
GO  
```  
  
A tabela a seguir lista as propriedades relacionadas a catálogos de texto completo. Talvez essas informações sejam úteis para administrar e solucionar problemas de pesquisa de texto completo. 
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**AccentSensitivity**|Configuração da diferenciação de caracteres com/sem acento.|
|**ImportStatus**|Se o catálogo de texto completo está sendo importado.|  
|**IndexSize**|Tamanho do catálogo de texto completo em megabytes (MB).| 
|**ItemCount**|Número atual de itens indexados de texto completo no catálogo de texto completo.|  
|**MergeStatus**|Se uma mesclagem mestra está em andamento.| 
|**PopulateCompletionAge**|Diferença, em segundos, entre a conclusão da última população do índice de texto completo e 01/01/1990 00:00:00.| 
|**PopulateStatus**|Status da população.<br /><br /> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]|  
|**UniqueKeyCount**|Número de chaves exclusivas no catálogo de texto completo.| 

##  <a name="rebuild-a-full-text-catalog"></a><a name="rebuildone"></a> Recompilar um catálogo de texto completo  

Execute a instrução Transact-SQL [ALTER FULLTEXT CATALOG ... REBUILD](
../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)ou faça as coisas a seguir no SQL Server Management Studio (SSMS).

1.  No SSMS, no Pesquisador de Objetos, expanda o servidor, expanda **Bancos de Dados** e o banco de dados que contém o catálogo de texto completo que você deseja recompilar.  
  
2.  Expanda **Armazenamento**e, depois, **Catálogos de texto completo**.  
  
3.  Clique com o botão direito do mouse no nome do catálogo de texto completo que deseja recriar e selecione **Recriar**.  
  
4.  Para a pergunta **Deseja excluir o catálogo de texto completo e recriá-lo?**, clique em **OK**.  
  
5.  Na caixa de diálogo **Recriar Catálogo de Texto Completo** , clique em **Fechar**.  
   
##  <a name="rebuild-all-full-text-catalogs-for-a-database"></a><a name="rebuildall"></a> Recompilar todos os catálogos de texto completo para um banco de dados  

1.  No SSMS, no Pesquisador de Objetos, expanda o servidor, expanda **Bancos de Dados** e o banco de dados que contém os catálogos de texto completo que você deseja recompilar.  
  
2.  Expanda **Armazenamento**e clique com o botão direito do mouse em **Catálogos de Texto Completo**.  
  
3.  Selecione **Recriar Tudo**.  
  
4.  Para a pergunta **Deseja excluir todos os catálogos de texto completo e recriá-los?**, clique em **OK**.  
  
5.  Na caixa de diálogo **Recriar Todos os Catálogos de Texto Completo** , clique em **Fechar**.  
  
  
  
##  <a name="remove-a-full-text-catalog-from-a-database"></a><a name="removing"></a> Remover um catálogo de texto completo de um banco de dados  

Execute a instrução Transact-SQL [DROP FULLTEXT CATALOG](
../../t-sql/statements/drop-fulltext-catalog-transact-sql.md) ou faça o seguinte no SQL Server Management Studio (SSMS).

1.  No SSMS, no Pesquisador de Objetos, expanda o servidor, **Bancos de Dados** e o banco de dados que contém o catálogo de texto completo que você deseja remover.  
  
2.  Expanda **Armazenamento**e **Catálogo de texto completo**.  
  
3.  Clique com o botão direito do mouse no catálogo de texto completo que deseja remover e selecione **Excluir**.  
  
4.  Na caixa de diálogo **Excluir Objetos** , clique em **OK**.  

## <a name="next-step"></a>Próxima etapa
[Criar e gerenciar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md)