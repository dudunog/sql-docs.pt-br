---
title: Agrupar ou desagrupar componentes | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- grouping containers
- tasks [Integration Services], grouping
- containers [Integration Services], grouping
- grouping tasks
ms.assetid: 34320838-c271-4f8c-90b3-1254690890bb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 999bdd02c0cbfa2f8d2df6be93b3261c5bdc1dc5
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296374"
---
# <a name="group-or-ungroup-components"></a>Agrupa ou desagrupa componentes

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  As guias **Fluxo de Controle**, **Fluxo de dados**e **Manipuladores de Eventos** no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] dão suporte a agrupamento recolhível. Se um pacote tem muitos componentes, as guias podem ficar cheias, tornando difícil visualizar todos os componentes ao mesmo tempo e localizar o item com o qual você quer trabalhar. O recurso de agrupamento desmontável, que pode conservar espaço na superfície de trabalho, e assim tornar mais fácil o trabalho com pacotes grandes.  
  
 Você seleciona os componentes que deseja agrupar, então os agrupa e, depois, expande ou recolhe os grupos para se adequarem ao seu trabalho. Expandir um grupo lhe dá acesso às propriedades dos componentes no grupo. As restrições de precedência que conectam tarefas e contêineres são automaticamente incluídas no grupo.  
  
 As seguintes são considerações para agrupar componentes.  
  
-   Para agrupar componentes, o fluxo de controle, fluxo de dados ou manipulador de eventos deverá conter mais de um componente.  
  
-   Os grupos também podem ser aninhados, tornando possível criar grupos dentro de grupos. A superfície do design pode implementar vários grupos não aninhados, mas um componente pode pertencer somente a um grupo, exceto se os grupos estiverem aninhados.  
  
-   Quando um pacote é salvo, o [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer salva o agrupamento, mas o agrupamento não tem nenhum efeito na execução de pacote. A habilidade de agrupar componentes é um recurso de tempo de design, ela não afeta o comportamento de tempo de execução do pacote.  
  
### <a name="to-group-components"></a>Para agrupar componentes  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle**, **Fluxo de Dados**ou **Manipuladores de Eventos** .  
  
4.  Na superfície de design da guia, selecione os componentes que você deseja agrupar, clique com o botão direito do mouse no componente selecionado e clique em **Agrupar**.  
  
5.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
### <a name="to-ungroup-components"></a>Para desagrupar componentes  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle**, **Fluxo de Dados**ou **Manipuladores de Eventos** .  
  
4.  Na superfície de design da guia, selecione o grupo que contém o componente que você deseja desagrupar, clique com o botão direito do mouse no componente selecionado e clique em **Desagrupar**.  
  
5.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)   
 [Como conectar tarefas e contêineres por meio de uma restrição de precedência padrão](https://msdn.microsoft.com/library/8f31f15f-98ff-4c35-b41f-8b8cfd148d75)  
  
  
