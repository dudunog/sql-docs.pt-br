---
title: Adicionar uma fonte usando o assistente de origem | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5e850b7c-4b89-42ad-b0a6-d63ac7cc9568
author: janinezhang
ms.author: janinez
ms.openlocfilehash: ce970f4e944fbc4d940d1021a48600be9cd47967
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84926297"
---
# <a name="add-a-source-using-source-assistant"></a>Adicionar uma origem com o Assistente de Origem
  Este tópico fornece etapas para adicionar uma nova origem por meio do Assistente de Origem e também lista as opções que estão disponíveis na caixa de diálogo **Adicionar Nova Origem** que você verá ao arrastar-soltar o Assistente de Origem para o Designer SSIS.  
  
### <a name="to-use-source-assistant-to-add-a-source"></a>Para usar o Assistente de Origem para adicionar uma origem  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ao qual você deseja adicionar um componente de origem.  
  
2.  Arraste o componente **Assistente de origem** da caixa de ferramentas do SSIS para a guia fluxo de **dados** . Você deve ver a caixa de diálogo **Adicionar nova origem** . A próxima seção fornece detalhes sobre as opções disponíveis na caixa de diálogo.  
  
3.  Selecione o tipo do destino na lista **Tipos**.  
  
4.  Selecione um Gerenciador de conexões existente na lista **gerenciadores de conexões** ou selecione **\<New>** para criar um novo Gerenciador de conexões.  
  
5.  Se você selecionar um gerenciador de conexões existente, clique em **OK** para fechar a caixa de diálogo **Adicionar Novo Destino**. Você deve ver o destino e os gerenciadores de conexões adicionados ao fluxo de dados.  
  
6.  Se você clicar **\<New>** para criar um novo Gerenciador de conexões, deverá ver uma caixa de diálogo **Gerenciador de conexões** , que permite especificar parâmetros para a conexão. Depois de concluir a criação do novo gerenciador de conexões, você verá o destino e o gerenciador de conexões no Designer SSIS.  
  
  
