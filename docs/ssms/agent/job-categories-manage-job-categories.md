---
description: Categorias de trabalho – Gerenciar categorias de trabalho
title: Categorias de trabalho – Gerenciar categorias de trabalho
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.categories.f1
helpviewer_keywords:
- Job Categories dialog box
ms.assetid: 38276438-40b1-43ce-9aae-6805be6d9332
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 880286e2ffa649316aa3c92c37f4bca461d62d4b
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037910"
---
# <a name="job-categories---manage-job-categories"></a>Categorias de trabalho – Gerenciar categorias de trabalho
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada de SQL do Azure](/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira detalhes nas [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Use a caixa de diálogo **Categorias de Trabalho** para adicionar ou excluir categorias de trabalho. Categorias de trabalho internas não podem ser excluídas.  
  
## <a name="options"></a>Opções  
**Nome**  
O nome da categoria de trabalho.  
  
**Número de trabalhos na categoria**  
O número de trabalhos definido para essa categoria.  
  
**Exibir Trabalhos**  
Abre a caixa de diálogo **Propriedades** para a categoria selecionada, para listar todos os trabalhos atualmente definidos para aquela categoria.  
  
**Adicionar**  
Abre a caixa de diálogo **Nova Categoria de Trabalho** , para adicionar uma nova categoria de trabalho  
  
**Delete (excluir)**  
Remove a categoria de trabalho selecionada. Habilitada somente para categorias de trabalho definidas pelo usuário.  
  
**Atualizar**  
Consulta o servidor para obter as informações atuais.  
  
#### <a name="to-access-the-job-categories-dialog-box"></a>Para acessar a caixa de diálogo Categorias de trabalho  
  
1.  No **Pesquisador de Objetos**, expanda **SQL Server Agent**, clique com o botão direito do mouse em **Trabalhos**e, então, clique em **Gerenciar Categorias de Trabalho**.  
