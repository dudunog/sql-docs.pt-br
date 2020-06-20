---
title: Renomear índices | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- renaming indexes
- index names [SQL Server]
- indexes [SQL Server], renaming
ms.assetid: d3d612a1-ea1b-4d99-85d2-0a2ad54f4b0e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 184d6e20f7857c5ea3535e77e21a0630ffc7b678
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049847"
---
# <a name="rename-indexes"></a>Renomear índices
  Este tópico descreve como renomear um índice no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Renomear um índice substitui o nome do índice atual pelo novo nome que você fornece. O nome especificado deve ser exclusivo dentro da tabela ou exibição. Por exemplo, duas tabelas podem ter um índice nomeado **XPK_1**, mas a mesma tabela não pode ter dois índices nomeados **XPK_1**. Você não pode criar um índice com o mesmo nome que um índice desabilitado existente. Renomear um índice não faz com que o índice seja reconstruído.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para renomear um índice, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
 Quando você cria uma restrição PRIMARY KEY ou UNIQUE em uma tabela, um índice com o mesmo nome da restrição é automaticamente criado para a tabela. Como os nomes de índice devem ser exclusivos dentro de uma tabela, você não pode criar ou renomear um índice com o mesmo nome de uma restrição PRIMARY KEY ou UNIQUE existente na tabela.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no índice.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-rename-an-index-by-using-the-table-designer"></a>Para renomear um índice usando o Designer de Tabela  
  
1.  No Pesquisador de Objetos, clique no sinal de adição para expandir o banco de dados que contém a tabela na qual você deseja renomear um índice.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique com o botão direito do mouse na tabela na qual você deseja renomear um índice e selecione **Design**.  
  
4.  No menu **Designer de Tabela** , clique em **Índices/Chaves**.  
  
5.  Selecione o índice a ser renomeado na caixa de texto **Índice ou Chave Exclusiva/Primária Selecionada** .  
  
6.  Na grade, clique em **Nome** e digite um nome novo na caixa de texto.  
  
7.  Clique em **fechar**  
  
8.  No menu **Arquivo** , clique em **Salvar**_table_name_.  
  
#### <a name="to-rename-an-index-by-using-object-explorer"></a>Para renomear um índice usando o Pesquisador de Objetos  
  
1.  No Pesquisador de Objetos, clique no sinal de adição para expandir o banco de dados que contém a tabela na qual você deseja renomear um índice.  
  
2.  Clique no sinal de adição para expandir a pasta **Tabelas** .  
  
3.  Clique no sinal de adição para expandir a tabela na qual você deseja renomear um índice.  
  
4.  Clique no sinal de adição para expandir a pasta **Índices** .  
  
5.  Clique com o botão direito do mouse no índice a ser renomeado e selecione **Renomear**.  
  
6.  Digite o novo nome do índice e pressione Enter.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-rename-an-index"></a>Para renomear um índice  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    --Renames the IX_ProductVendor_VendorID index on the Purchasing.ProductVendor table to IX_VendorID.   
  
    EXEC sp_rename N'Purchasing.ProductVendor.IX_ProductVendor_VendorID', N'IX_VendorID', N'INDEX';   
    GO  
    ```  
  
 Para obter mais informações, veja [sp_rename &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql).  
  
  
