---
title: Adicionar Enumeração a um fluxo de controle | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- adding enumerations
- Foreach Loop containers
- control flow [Integration Services], enumerations
- repeating workflows
- enumerations [Integration Services]
ms.assetid: f212b5fb-3cc4-422e-9b7c-89eb769a812a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: bff127798f7c36340a85fa72cebfdc9a012c0676
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84926097"
---
# <a name="add-enumeration-to-a-control-flow"></a>Adicionar enumeração a um fluxo de controle
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] inclui o contêiner do Loop Foreach, um elemento de fluxo de controle que torna simples a inclusão de um constructo de loop que enumera arquivos e objetos no fluxo de controle de um pacote. Para obter mais informações, consulte [Contêiner Loop Foreach](control-flow/foreach-loop-container.md).  
  
 O contêiner Loop Foreach não fornece nenhuma funcionalidade, ele só fornece a estrutura na qual você cria o fluxo de controle repetível, especifica o tipo do enumerados e configura o enumerador. Para fornecer funcionalidade de contêiner, você deve incluir no mínimo uma tarefa no contêiner Loop Foreach. Para obter mais informações, consulte [Tarefas do Integration Services](control-flow/integration-services-tasks.md).  
  
 O contêiner Loop Foreach pode incluir um fluxo de controle com várias tarefas e outros contêineres. Adicionar tarefas e contêineres ao contêiner Loop Foreach é semelhante a adicioná-las a um pacote, exceto que você arrasta as tarefas e contêineres para o contêiner Loop Foreach e não para o pacote. Se o contêiner Loop Foreach incluir mais de uma tarefa ou contêiner, você poderá conectá-los usando as restrições de precedência, assim como faria em um pacote. Para obter informações, consulte [Restrições de precedência](control-flow/precedence-constraints.md).  
  
### <a name="to-implement-a-foreach-loop-container-in-a-control-flow"></a>Para implementar um contêiner Loop Foreach em um fluxo de controle  
  
1.  Adicione o contêiner Loop Foreach ao pacote. Para obter mais informações, consulte [Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
2.  Adicione tarefas e contêineres ao contêiner Loop Foreach. Para obter mais informações, consulte [Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  .  
  
3.  Conecte tarefas e contêineres no contêiner Loop Foreach usando restrições de precedência. Para obter mais informações, consulte [Como conectar tarefas e contêineres utilizando uma restrição de precedência padrão](../../2014/integration-services/connect-tasks-and-containers-by-using-a-default-precedence-constraint.md).  
  
4.  Configure o contêiner Loop Foreach. Para obter mais informações, consulte [Configurar um contêiner Loop Foreach](../../2014/integration-services/configure-a-foreach-loop-container.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [Agrupar ou desagrupar componentes](group-or-ungroup-components.md)   
 [Restrições de precedência](control-flow/precedence-constraints.md)   
 [Adicionar iteração a um fluxo de controle](add-iteration-to-a-control-flow.md)   
 [Fluxo de controle](control-flow/control-flow.md)  
  
  
