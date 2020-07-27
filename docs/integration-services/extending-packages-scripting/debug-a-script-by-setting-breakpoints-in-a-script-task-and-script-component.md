---
title: Depurar um script configurando pontos de interrupção em uma tarefa Script e um componente de Script | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- breakpoints [Integration Services]
- scripts [Integration Services], breakpoints
ms.assetid: 6c03464f-3f7d-4882-b7f8-8e396f8e2944
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0c9380a9e8699b2c0f38436228b0a2fdf820096e
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913382"
---
# <a name="debug-a-script-by-setting-breakpoints-in-a-script-task-and-script-component"></a>Depurar um script definindo pontos de interrupção em uma tarefa Script e um componente Script

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Este procedimento descreve como definir pontos de interrupção nos scripts que são usados na tarefa Script e componente Script.  
  
 Após você definir pontos de interrupção no script, a caixa de diálogo **Definir Pontos de Interrupção - \<object name>** lista os pontos de interrupção, bem como os pontos de interrupção inseridos.  
  
> [!IMPORTANT]  
>  Em determinadas circunstâncias, os pontos de interrupção na tarefa Script e no componente Script são ignorados. Para obter mais informações, consulte a seção **Depurando a tarefa Script** em [Codificando e depurando a tarefa Script](../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md) e a seção **Depurando o componente Script** em [Codificando e depurando o componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="to-set-a-breakpoint-in-script"></a>Para definir um ponto de interrupção em script  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  Clique duas vezes no pacote que contém o script em que você quer definir pontos de interrupção.  
  
3.  Para abrir a tarefa Script, clique nela duas vezes após abrir a guia **Fluxo de Controle**.  
  
4.  Para abrir o componente Script, clique na guia **Fluxo de Dados** e então clique duas vezes no componente Script.  
  
5.  Clique em **Script** e então clique em **Editar Script**.  
  
6.  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] VSTA ([!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications), localize a linha de script em que deseja definir um ponto de interrupção, clique com o botão direito do mouse na linha, aponte para **Ponto de Interrupção** e, em seguida, clique em **Inserir Ponto de Interrupção**.  
  
     O ícone de ponto de interrupção é exibido na linha de código.  
  
7.  No menu **Arquivo** , clique em **Sair**.  
  
8.  Clique em **OK**.  
  
9. Para salvar o pacote, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
  
