---
title: Modificar restrições exclusivas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- modifying constraints
- UNIQUE constraints [SQL Server], modifying
- constraints [SQL Server], modifying
- constraints [SQL Server], unique
ms.assetid: fddbdc9e-958b-4614-8e88-6ca205d64a4e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8bb3daf170e25abc9b346aeaedb4b835cae2dfdd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68809922"
---
# <a name="modify-unique-constraints"></a>Modificar restrições exclusivas
  Você pode modificar uma restrição exclusiva no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para modificar uma restrição exclusiva usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Exige a permissão ALTER na tabela.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-modify-a-unique-constraint"></a>Para modificar uma restrição exclusiva  
  
1.  No **Pesquisador de Objetos**, clique com o botão direito do mouse na tabela que contém restrição exclusiva e selecione **Design**.  
  
2.  No menu **Designer de Tabela**, clique em **Índices/Chaves...** .  
  
3.  Na caixa de diálogo **Índices/Chaves** , selecione **Índice ou Chave Exclusiva/Primária Selecionada**e selecione a restrição que deseja editar.  
  
4.  Complete uma ação da seguinte tabela:  
  
    |Para|Siga estas etapas|  
    |--------|------------------------|  
    |Alterar as colunas às quais a restrição está associada|1) Na grade, em **(Geral)** , clique em **Colunas** e nas reticências **(…)** à direita da propriedade.<br /><br /> 2) Na caixa de diálogo **Colunas de Índice** , especifique a nova coluna, a ordem de classificação ou ambas para o índice.|  
    |Renomear a restrição|Na grade, em **Identidade**, digite um novo nome na caixa **Nome** . Verifique se seu novo nome não duplica um nome na lista **Índice ou Chave Exclusiva/Primária Selecionada** .|  
    |Definir a opção clustered|Na grade, em **Designer de Tabela**, selecione **Criar como Clusterizado** e, na lista suspensa, escolha Sim para criar um índice clusterizado e Não para criar um não clusterizado. Só pode existir um índice clusterizado por tabela. Se já houver um índice clusterizado nessa tabela, você deverá desmarcar essa configuração no índice original.|  
    |Definir um fator de preenchimento|Na grade, em **Designer de Tabela**, expanda a categoria **Especificação de Preenchimento** e digite um inteiro de 0 a 100 na caixa **Fator de Preenchimento** .|  
  
5.  No menu **Arquivo**, clique em **Salvar**_nome da tabela_.  
  
##  <a name="to-modify-a-unique-constraint"></a><a name="TsqlProcedure"></a> **Para modificar uma restrição exclusiva**  
  
 Para modificar a restrição UNIQUE usando o Transact-SQL, exclua primeiramente a restrição UNIQUE existente e, em seguida, recrie-a com a nova definição. Para obter mais informações, consulte [Delete Unique Constraints](delete-unique-constraints.md) e [Create Unique Constraints](create-unique-constraints.md).  
  
###  <a name="TsqlExample"></a>  
