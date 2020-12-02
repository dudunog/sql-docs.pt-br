---
description: Adicionar ou excluir um componente em um fluxo de dados
title: Adicionar ou excluir um componente em um fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- adding components
- components [Integration Services], data flow
ms.assetid: d99124f9-0994-4f40-a48e-fdca6a4383e7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 38ca8342ac6cbdab99c3314b49cac4c28408fee3
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127370"
---
# <a name="add-or-delete-a-component-in-a-data-flow"></a>Adicionar ou excluir um componente em um fluxo de dados

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Os componentes de fluxo de dados são fontes, destinos e transformações em um fluxo de dados. Para adicionar componentes a um fluxo de dados, o fluxo de controle do pacote deve incluir uma tarefa Fluxo de Dados.  
  
 Os procedimentos a seguir descrevem como adicionar ou excluir um componente no fluxo de dados de um pacote.  
  
### <a name="to-add-a-component-to-a-data-flow"></a>Para adicionar um componente a um fluxo de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** e clique duas vezes na tarefa Fluxo de Dados que contém o fluxo de dados ao qual você deseja adicionar um componente.  
  
4.  Na Caixa de Ferramentas, expanda **Origens de Fluxos de Dados**, **Transformações de Fluxos de Dados** ou **Destinos de Fluxos de Dados** e arraste um item do fluxo de dados até a superfície de design da guia **Fluxo de Dados** .  
  
5.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
### <a name="to-delete-a-component-from-a-data-flow"></a>Para excluir um componente de um fluxo de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** e clique duas vezes na tarefa Fluxo de Dados que contém o fluxo de dados do qual você deseja excluir um componente.  
  
4.  Clique com o botão direito do mouse no componente do fluxo de dados e clique em **Excluir**.  
  
5.  Confirme a operação de exclusão.  
  
6.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [Conectar componentes em um fluxo de dados](../../integration-services/data-flow/connect-components-in-a-data-flow.md)   
 [Depurar o fluxo de dados](../../integration-services/troubleshooting/debugging-data-flow.md)   
 [Fluxo de Dados](../../integration-services/data-flow/data-flow.md)  
  
  
