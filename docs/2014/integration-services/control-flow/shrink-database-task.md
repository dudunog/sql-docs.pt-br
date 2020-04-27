---
title: Tarefa Reduzir Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.shrinkdatabasetask.f1
helpviewer_keywords:
- Shrink Database task
- database shrinking [Integration Services]
- shrinking databases
ms.assetid: e66286f8-97b1-4e5a-86b4-e56f1932b7d5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 617a0af103c5490faec2a5a8e5f6796cc8af0eea
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62830089"
---
# <a name="shrink-database-task"></a>Tarefa Reduzir Banco de Dados
  A tarefa Reduzir Banco de Dados reduz o tamanho de dados de bancos de dados e de arquivos de log do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Usando a tarefa Reduzir Banco de Dados, um pacote pode reduzir os arquivos de um único banco de dados ou de vários bancos de dados.  
  
 A redução de arquivos de dados recupera espaço com a movimentação de páginas de dados do final do arquivo para o espaço desocupado mais próximo à frente do arquivo. Quando espaço livre suficiente é criado no final do arquivo, as páginas de dados no final do arquivo podem ser desalocadas e retornadas para o sistema de arquivos.  
  
> [!WARNING]  
>  Os dados movidos para reduzir um arquivo podem ser espalhados para qualquer local disponível no arquivo. Isso provoca uma fragmentação do índice e pode reduzir a velocidade do desempenho de consultas que pesquisam um intervalo do índice. Para eliminar a fragmentação, considere a recompilação dos índices no arquivo após a redução.  
  
## <a name="commands"></a>Comandos  
 A tarefa Reduzir Banco de Dados encapsula um comando DBCC SHRINKDATABASE, inclusive os seguintes argumentos e opções:  
  
-   *database_name*  
  
-   *target_percent*  
  
-   NOTRUNCATE ou TRUNCATEONLY.  
  
 Se a tarefa Reduzir Banco de Dados reduzir vários bancos de dados, a tarefa executará vários comandos SHRINKDATABASE, um para cada banco de dados. Todas as instâncias do comando SHRINKDATABASE usam os mesmos valores de argumento, exceto para o argumento *database_name* . Para obter mais informações, consulte [DBCC SHRINKDATABASE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql).  
  
## <a name="configuration-of-the-shrink-database-task"></a>Configuração da tarefa Reduzir Banco de Dados  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer. Esta tarefa está na seção **Tarefas do Plano de Manutenção** da **Caixa de Ferramentas** , no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , clique no seguinte tópico:  
  
-   [Tarefa Reduzir Banco de Dados &#40;Plano de Manutenção&#41;](../../relational-databases/maintenance-plans/shrink-database-task-maintenance-plan.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../set-the-properties-of-a-task-or-container.md)  
  
  
