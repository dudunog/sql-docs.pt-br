---
title: 'Etapa 8: Anotar e formatar o pacote da Lição 1 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: e3751e53-77c7-47d0-8fe8-73ed1a53413a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3a67d7593ca63a2271fc94fc7203e9bb55d6efcc
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71680968"
---
# <a name="lesson-1-8-annotate-and-format-the-lesson-1-package"></a>Lição 1-8: Anotar e formatar o pacote da Lição 1 

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Agora que você concluiu a configuração do pacote da Lição 1, é uma boa hora para organizar o layout do pacote. Se as formas em layouts de fluxo de controle e de dados forem de tamanhos diferentes ou não estiverem dispostas uniformemente, poderá ser mais difícil entender o pacote.  
  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools fornece ferramentas para formatar facilmente o layout do pacote. Os recursos de formatação incluem a capacidade de criar formas do mesmo tamanho, alinhar formas e alterar o espaçamento horizontal e vertical entre os espaçamentos.  
  
Outro modo para melhorar a compreensão de funcionalidade de pacote é adicionar anotações que descrevem a funcionalidade do pacote.  
  
Nesta tarefa, você usa os recursos de formatação nas ferramentas de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para melhorar o layout do fluxo de dados e também adicionar uma anotação.  
  
## <a name="format-the-layout-of-the-data-flow"></a>Formatar o layout do fluxo de dados  
  
1.  Se o pacote da Lição 1 ainda não estiver aberto, clique duas vezes em **Lição 1.dtsx** no **Gerenciador de Soluções**.  
  
2.  Selecione a guia **Fluxo de Dados**.  
  
3.  Para selecionar todos os componentes de fluxo de dados ao mesmo tempo, use **Editar** > **Selecionar Tudo**.
  
4.  No menu **Formato**, selecione **Igualar Tamanho** e, em seguida, selecione **Ambos**.  
  
5.  Com os objetos de fluxo de dados selecionados, no menu **Formato**, selecione **Alinhar** e, em seguida, **Centros**.  

6.  Com os objetos de fluxo de dados selecionados, no menu **Formato**, aponte para **Espaçamento Vertical** e, em seguida, selecione **Igualar**.  
  
## <a name="add-an-annotation-to-the-data-flow"></a>Adicionar uma anotação ao fluxo de dados  
  
1.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da superfície de design do fluxo de dados e selecione **Adicionar Anotação**.  
  
2.  Insira ou cole o texto a seguir na caixa de anotação.  
  
        The data flow extracts data from a file, looks up values in the CurrencyKey column in the DimCurrency table and the DateKey column in the DimDate table, and writes the data to the NewFactCurrencyRate table.
  
    Para encapsular o texto na caixa de anotação, posicione o cursor no local em que deseja começar uma nova linha e pressione **Enter**.  
  
    Se você não adicionar texto à caixa de anotação, essa caixa desaparecerá quando você clicar fora dela.  Devido a esse comportamento, caso você deseje colar o texto na caixa de anotação, copie o texto para a área de transferência antes de selecionar Adicionar Anotação. 
  
## <a name="go-to-next-task"></a>Ir para a próxima tarefa
[Etapa 9: Testar o pacote da Lição 1](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
  
  
