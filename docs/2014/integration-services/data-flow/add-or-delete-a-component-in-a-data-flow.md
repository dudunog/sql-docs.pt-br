---
title: Adicionar ou excluir um componente em um fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- adding components
- components [Integration Services], data flow
ms.assetid: d99124f9-0994-4f40-a48e-fdca6a4383e7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d68c57031b830fd891b4e2f0bcd8df87aa06732f
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85432443"
---
# <a name="add-or-delete-a-component-in-a-data-flow"></a>Adicionar ou excluir um componente em um fluxo de dados
  Os componentes de fluxo de dados são fontes, destinos e transformações em um fluxo de dados. Para adicionar componentes a um fluxo de dados, o fluxo de controle do pacote deve incluir uma tarefa Fluxo de Dados.  
  
 Os procedimentos a seguir descrevem como adicionar ou excluir um componente no fluxo de dados de um pacote.  
  
### <a name="to-add-a-component-to-a-data-flow"></a>Para adicionar um componente a um fluxo de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** e clique duas vezes na tarefa Fluxo de Dados que contém o fluxo de dados ao qual você deseja adicionar um componente.  
  
4.  Na Caixa de Ferramentas, expanda **Origens de Fluxos de Dados**, **Transformações de Fluxos de Dados**ou **Destinos de Fluxos de Dados**e arraste um item do fluxo de dados até a superfície de design da guia **Fluxo de Dados** .  
  
5.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
### <a name="to-delete-a-component-from-a-data-flow"></a>Para excluir um componente de um fluxo de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** e clique duas vezes na tarefa Fluxo de Dados que contém o fluxo de dados do qual você deseja excluir um componente.  
  
4.  Clique com o botão direito do mouse no componente do fluxo de dados e clique em **Excluir**.  
  
5.  Confirme a operação de exclusão.  
  
6.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [Conectar componentes em um fluxo de dados](data-flow.md)   
 [Configurar uma saída de erro em um componente de fluxo de dados](../configure-an-error-output-in-a-data-flow-component.md)   
 [Fluxo de Dados](data-flow.md)  
  
  
