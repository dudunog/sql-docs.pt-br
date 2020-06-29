---
title: 'Etapa 8: Tornando o pacote da Lição 1 mais fácil de compreender | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e3751e53-77c7-47d0-8fe8-73ed1a53413a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e3a8837cbf3b102435a94706ee277aab9a42fb73
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85440673"
---
# <a name="step-8-making-the-lesson-1-package-easier-to-understand"></a>Etapa 8: Tornar o pacote da Lição 1 mais fácil de compreender
  Agora que você concluiu a configuração do pacote da Lição 1, é uma boa ideia verificar o layout do pacote. Se as formas dos layouts de controle e dos fluxos de dados são de tamanhos aleatórias ou se as formas não estão alinhadas ou agrupadas, a funcionalidade de pacote pode ser mais difícil de ser entendida.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornecem recursos que facilitam e agilizam a formatação do layout do pacote. Os recursos de formatação incluem a capacidade de criar formas do mesmo tamanho, alinhar formas e manipular o espaçamento horizontal e vertical entre os espaçamentos.  
  
 Outro modo para melhorar a compreensão de funcionalidade de pacote é adicionar anotações que descrevem a funcionalidade do pacote.  
  
 Nesta tarefa, você utilizará os recursos de formatação nas ferramentas de dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para melhorar o layout do fluxo de dados e também adicionar uma anotação ao fluxo de dados.  
  
### <a name="to-format-the-layout-of-the-data-flow"></a>Para formatar o layout do fluxo de dados  
  
1.  Se o pacote da Lição 1 ainda não estiver aberto, no Gerenciador de Soluções, clique duas vezes em Lição 1.dtsx.  
  
2.  Clique na guia **Fluxo de Dados** .  
  
3.  Posicione o cursor na parte superior e à direita da transformação Extrair Moeda de Exemplo e clique e arraste o cursor por todos os componentes do fluxo de dados.  
  
4.  No menu **Formatar** , aponte para **Igualar Tamanho**e clique em **Ambos**.  
  
5.  Com os objetos de fluxo de dados selecionados, no menu **Formatar** , aponte para **Alinhar**e clique em **À esquerda**.  
  
### <a name="to-add-an-annotation-to-the-data-flow"></a>Para adicionar uma anotação ao fluxo de dados  
  
1.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da superfície de design do fluxo de dados e clique em **Adicionar Anotação**.  
  
2.  Digite ou cole o texto a seguir na caixa de anotação.  
  
     **O fluxo de dados extrai os dados de um arquivo, pesquisa valores na coluna CurrencyKey da tabela DimCurrency e na coluna DateKey da tabela DimDate, além de gravar os dados na tabela NewFactCurrencyRate.**  
  
     Para usar a quebra de linhas no texto da caixa de anotação, posicione o cursor no local em que deseja começar uma nova linha e pressione a tecla Enter.  
  
     Se você não inserir um texto na caixa de anotação, essa caixa desaparecerá ao clicar fora dela.  
  
## <a name="next-steps"></a>Próximas etapas  
 [Etapa 9: Testar o pacote de tutorial da Lição 1](../integration-services/lesson-1-9-testing-the-lesson-1-tutorial-package.md)  
  
  
