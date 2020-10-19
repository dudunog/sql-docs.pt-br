---
description: Crie uma cópia duplicada de uma tabela, sem os dados da linha.
title: Duplicar tabelas | Microsoft Docs
ms.custom: ''
ms.date: 10/05/2020
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- copying tables
- tables [SQL Server], duplicating
- duplicating tables
- duplicating table structures
- table copying [SQL Server]
ms.assetid: c6b07423-d1e5-4e5e-8681-5088921f5df3
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a8faa1aab3237152934f0ce9eb4cb9ce541d5d3d
ms.sourcegitcommit: 346a37242f889d76cd783f55aeed98023c693610
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2020
ms.locfileid: "91765808"
---
# <a name="duplicate-tables"></a>Duplicar tabelas
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa-pdw.md)]

Você pode duplicar uma tabela existente no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)] criando uma nova tabela e copiando as informações de coluna de uma tabela existente.  
  
> [!IMPORTANT]  
>  Essa operação duplica apenas a estrutura de uma tabela; ela não duplica nenhuma linha da tabela.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para duplicar uma tabela usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Exige permissão CREATE DATABASE no banco de dados de destino.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-duplicate-a-table"></a>Para duplicar uma tabela  
  
1.  Verifique se você está conectado ao banco de dados em que deseja criar a tabela e se o banco de dados está selecionado no Pesquisador de Objetos.  
  
2.  No Pesquisador de Objetos, clique com o botão direito do mouse em **Tabelas** e clique em **Nova Tabela**.  
  
3.  No Pesquisador de Objetos, clique com o botão direito do mouse na tabela que deseja copiar e clique em **Design**.  
  
4.  Selecione as colunas na tabela existente e, no menu **Editar** , clique em **Copiar**.  
  
5.  Volte para a nova tabela nova e selecione a primeira linha.  
  
6.  No menu **Editar** , clique em **Colar**.  
  
7.  No menu **Arquivo** , clique em **Salvar**_table name_.  
  
8.  Na caixa de diálogo **Escolher Nome** , digite um nome para a nova tabela e clique em **OK**.  

##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-duplicate-a-table-in-query-editor"></a>Para duplicar uma tabela no Editor de Consultas  
  
1.  Verifique se você está conectado ao banco de dados em que deseja criar a tabela e se o banco de dados está selecionado no Pesquisador de Objetos.  
  
2.  Clique com o botão direito do mouse na tabela que você deseja duplicar, aponte para **Gerar Script de Tabela como**e para **CREATE to**e selecione **Nova Janela do Editor de Consultas**.  
  
3.  Altere o nome da tabela.  
  
4.  Remova as colunas que não são necessárias na nova tabela.  
  
5.  Clique em **Executar**.  
