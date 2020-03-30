---
title: Reconciliar um diagrama de banco de dados com um banco de dados modificado
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- updating diagram to match database
- reconciling database diagrams
- diagrams [SQL Server], reconciling changes
- updating database to match diagram
- database diagrams [SQL Server], reconciling changes
ms.assetid: eda8dea2-eedd-43a7-85aa-92bd97783b5f
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: c9eaf5f0a26660439d9bfbc9db85c645d95553e3
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75255290"
---
# <a name="reconcile-a-database-diagram-with-a-modified-database-visual-database-tools"></a>Reconciliar um diagrama de banco de dados com um banco de dados modificado (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Você salva seu diagrama de banco de dados, quando estiver pronto para atualizar o banco de dados, de forma que ele corresponda ao seu diagrama. Porém, se outros usuários tiverem atualizado o banco de dados desde que você abriu seu diagrama, essas alterações podem afetar seu diagrama e vice-versa.  
  
Salvar seu diagrama reconciliará o banco de dados com seu diagrama, substituindo as alterações de outros usuários para que o banco de dados corresponda ao seu diagrama.  
  
### <a name="to-update-a-database-to-match-your-diagram"></a>Para atualizar um banco de dados para que ele corresponda ao seu diagrama  
  
1.  Salve seu diagrama de banco de dados  
  
    Se você não salvou seu diagrama anteriormente, digite um nome para o diagrama na caixa de diálogo **Salvar Novo Diagrama de Banco de Dados** e escolha **OK**.  
  
2.  A caixa de diálogo **Salvar** lista as tabelas que serão afetadas quando você salvar seu diagrama. Escolha **Sim** para continuar.  
  
3.  A caixa de diálogo **Alterações de Banco de Dados Detectadas** lista os objetos que foram modificados e serão alterados para corresponder a seu diagrama. Escolha **Sim** para salvar o diagrama e aceitar a lista de alterações.  
  
    > [!NOTE]  
    > Se seu diagrama contiver tabelas e colunas que foram excluídas no banco de dados, só suas definições serão recriadas no banco de dados quando você salvar seu diagrama. Este processo não restaura quaisquer dados que existiam nestes objetos antes de sua exclusão.  
  
### <a name="to-update-your-diagram-to-match-a-modified-database"></a>Para atualizar seu diagrama para que ele corresponda a um banco de dados modificado  
  
1.  Feche seu diagrama sem salvar as alterações.  
  
2.  Clique com o botão direito no diagrama no Pesquisador de Objetos  
  
3.  No menu de atalho, clique em **Atualizar**.  
  
4.  Reabra o diagrama.  
  
## <a name="see-also"></a>Consulte Também  
[Trabalhar com diagramas de banco de dados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/work-with-database-diagrams-visual-database-tools.md)  
  
