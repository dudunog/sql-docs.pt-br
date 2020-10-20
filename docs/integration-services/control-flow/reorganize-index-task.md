---
description: Tarefa Reorganizar Índice
title: Tarefa Reorganizar Índice | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.reorganizeindextask.f1
helpviewer_keywords:
- reorganizing indexes
- Reorganize Index task [Integration Services]
- indexes [Integration Services]
ms.assetid: 9ed87861-e5c3-4fcd-8760-d112f4c0af0c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 307854616b6257c00bbcf9d5b66df6d00211b7b5
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92197153"
---
# <a name="reorganize-index-task"></a>Tarefa Reorganizar Índice

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  A tarefa Reorganizar Índice reorganiza índices em tabelas e exibições de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações sobre o gerenciamento de índices, consulte [Reorganizar e recriar índices](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).  
  
 Utilizando a tarefa Reorganizar Índice, um pacote pode reorganizar índices em um único ou em vários banco de dados. Se a tarefa reorganizar só os índices em um único banco de dados, você poderá escolher as exibições e as tabelas cujos índices a tarefa reorganizará. A tarefa Reorganizar Índice também inclui uma opção de compactar dados de objetos grandes. Os dados de objeto grande são dados com o tipo de dados **image**, **text**, **ntext**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)** ou **xml** . Para obter mais informações, veja [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md).  
  
 A tarefa Reorganizar Índice encapsula a instrução Transact-SQL ALTER INDEX. Se você escolher compactar dados de objeto grandes, a instrução usará a cláusula REORGANIZE WITH (LOB_COMPACTION = ON); caso contrário, LOB_COMPACTION será definido como OFF. Para obter mais informações, consulte [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
> [!IMPORTANT]  
>  O tempo que a tarefa necessita para criar a instrução Transact-SQL que ela executa é proporcional ao número de índices reorganizados pela tarefa. Se a tarefa for configurada para reorganizar índices em todas as tabelas e exibições em um banco de dados com um grande número de índices ou em vários bancos de dados, ela poderá levar um tempo considerável para gerar a instrução Transact-SQL.  
  
## <a name="configuration-of-the-reorganize-index-task"></a>Configuração da tarefa Reorganizar Índice  
 Você pode definir propriedades por meio do [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer. Esta tarefa está na seção **Tarefas do Plano de Manutenção** da **Caixa de Ferramentas** , no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Tarefa de Reorganização de Índice &#40;Plano de Manutenção&#41;](../../relational-databases/maintenance-plans/reorganize-index-task-maintenance-plan.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter mais informações sobre como definir essas propriedades no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] , consulte [Definir as propriedades de uma tarefa ou um contêiner](./add-or-delete-a-task-or-a-container-in-a-control-flow.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas do Integration Services](../../integration-services/control-flow/integration-services-tasks.md)   
 [Fluxo de Controle](../../integration-services/control-flow/control-flow.md)  
  
