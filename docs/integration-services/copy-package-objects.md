---
description: Copiar objetos de pacote
title: Copiar objetos de pacote | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- control flow [Integration Services], copying objects
- copying package objects [Integration Services]
- data flow [Integration Services], copying objects
- connection managers [Integration Services], copying
ms.assetid: 99b85e5c-d6bd-4e7c-afe4-51f6ce151c2f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9d19b63fe653700839f4ea3443fc0676890fdcc9
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96127397"
---
# <a name="copy-package-objects"></a>Copiar objetos de pacote

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  Este tópico descreve como copiar os itens de fluxo de controle, itens de fluxo de dados e gerenciadores de conexões dentro de um pacote ou entre pacotes.  
  
### <a name="to-copy-control-and-data-flow-items"></a>Copiar itens de fluxo de controle e fluxo de dados  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém os pacotes com os quais deseja trabalhar.  
  
2.  No Gerenciador de Soluções, clique duas vezes nos pacotes que deseja copiar.  
  
3.  No Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , clique na guia do pacote que contém os itens a serem copiados e clique na guia **Fluxo de Controle**, **Fluxo de Dados** ou **Manipulador de Eventos** .  
  
4.  Selecione os itens de fluxo de controle ou de dados que deseja copiar. Para selecionar vários itens de uma vez, pressione a tecla Shift e clique no item ou selecione os itens como um grupo, arrastando o ponteiro pelos itens que deseja selecionar.  
  
    > [!IMPORTANT]  
    >  As restrições de precedência e caminhos que conectam itens não são selecionadas automaticamente quando você seleciona dois itens que elas conectam. Para copiar um fluxo de trabalho ordenado – um segmento do fluxo de controle ou do fluxo de dados – certifique-se de que tenha copiado também as restrições de precedência e os caminhos.  
  
5.  Clique com o botão direito do mouse em um item selecionado e clique em **Copiar**.  
  
6.  Se quiser copiar os itens para um pacote diferente, clique no pacote para o qual deseja copiar e, em seguida, clique na guia apropriada para o tipo de item.  
  
    > [!IMPORTANT]  
    >  Você não pode copiar um fluxo de dados em um pacote a menos que o pacote contenha pelo menos uma tarefa Fluxo de Dados.  
  
7.  Clique com o botão direito do mouse e clique em **Colar**.  
  
### <a name="to-copy-connection-managers"></a>Copiar gerenciadores de conexões  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote com o qual deseja trabalhar.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote.  
  
3.  No Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , clique na guia **Fluxo de Controle**, **Fluxo de Dados** ou **Manipulador de Eventos** .  
  
4.  Na área **Gerenciadores de Conexões** , clique com o botão direito do mouse no gerenciador de conexões e clique em **Copiar**. Você pode copiar apenas um gerenciador de conexões por vez.  
  
5.  Se quiser copiar os itens para um pacote diferente, clique no pacote para o qual deseja copiar e, em seguida, clique na guia **Fluxo de Controle**, **Fluxo de Dados** ou **Manipulador de Eventos** .  
  
6.  Clique com o botão direito do mouse na área **Gerenciadores de Conexões** e clique em **Colar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Fluxo de Controle](../integration-services/control-flow/control-flow.md)   
 [Fluxo de Dados](../integration-services/data-flow/data-flow.md)   
 [Conexões do SSIS &#40;Integration Services&#41;](../integration-services/connection-manager/integration-services-ssis-connections.md)   
 [Copiar itens do projeto](./integration-services-ssis-projects-and-solutions.md)  
  
