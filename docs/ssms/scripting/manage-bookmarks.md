---
title: Gerenciar indicadores
description: A janela Indicadores de um editor de códigos permite que você crie links para localizações no código. Saiba como criar, excluir, ativar e desabilitar indicadores e como usá-los para navegar pelo código.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- bookmarks [SQL Server Management Studio]
ms.assetid: 67cc3fd6-3238-4c58-a3ec-2d3b0438143a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4b75287c722757e6bb6f12a7eb282b7f141a9483
ms.sourcegitcommit: d855def79af642233cbc3c5909bc7dfe04c4aa23
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2020
ms.locfileid: "87122597"
---
# <a name="manage-bookmarks"></a>Gerenciar indicadores
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  Quando estiver trabalhando em um editor de códigos, a janela **Indicadores** permite criar links com linhas específicas de código dentro de seu documento. Você pode exibir essa janela no menu **Exibir** .  
  
 Para criar e navegar pelos indicadores, clique nos botões localizados na barra de ferramentas **TextEditor** na parte superior da janela **Indicadores** . Você pode adicionar e remover indicadores, pode ativá-los ou desabilitá-los e organizá-los em pastas. Alguns comandos também estão disponíveis no menu de atalho na janela **Indicadores** . Para adicionar ou remover um indicador, posicione o ponto de inserção na linha desejada do Editor e clique em **Alternar um indicador**. Para ativar um indicador, marque sua caixa de seleção na janela **Indicadores** ; para desabilitar (sem remover) um indicador, desmarque sua caixa de seleção.  
  
## <a name="text-editor-toolbar"></a>Barra de ferramentas do Editor de Textos  
 Quando um documento de texto é aberto no Editor, os botões abaixo estão habilitados na barra de ferramentas **Editor de Texto** . Para exibir a barra de ferramentas **Editor de Texto** quando estiver no Editor de Consultas, no menu **Exibir** , aponte para **Barras de Ferramentas**e clique em **Editor de Texto**.  
  
 **Alternar um indicador na linha atual**  
 Adiciona ou remove um indicador na linha selecionada do documento no Editor ativo. Não altera a linha de código com indicador.  
  
 **Mover o ponto de intercalação para o indicador anterior**  
 Seleciona o indicador anterior que está habilitado na janela **Indicadores** . Quando o primeiro indicador é atingido, ele volta ao último. Conforme necessário, abre o arquivo onde está o indicador selecionado no Editor. Rola esse documento até a linha marcada e coloca o ponto de inserção nesse local.  
  
 **Mover o sinal de intercalação para o próximo indicador**  
 Seleciona o próximo indicador que está habilitado na janela **Indicadores** . Quando o último indicador é atingido, ele volta ao primeiro. Conforme necessário, abre o arquivo onde está o indicador selecionado no Editor. Rola esse documento até a linha marcada e coloca o ponto de inserção nesse local.  
  
 **Desmarcar todos os indicadores no documento atual**  
 Exibe uma mensagem de confirmação e, então, remove todos os indicadores do documento ativo. Não remove as linhas de código que continham indicadores.  
  
> [!CAUTION]  
>  Você não pode desfazer esse procedimento. Posteriormente, você deve usar **Alternar um indicador na linha atual** para criar indicadores novos. Para desabilitar indicadores sem removê-los, desmarque suas caixas de seleção na janela **Indicadores** .  
  
## <a name="bookmarks-window"></a>Janela Indicadores  
 Para organizar indicadores, crie pastas de indicadores na janela **Indicadores** . Arraste e solte indicadores nas pastas. Os botões a seguir estão disponíveis na parte superior da janela **Indicadores** .  
  
 **Alternar um indicador na linha atual.**  
 Adiciona ou remove um indicador na linha selecionada do documento no Editor ativo. Não altera a linha de código com indicador.  
  
 **Nova pasta**  
 Adiciona uma pasta à janela **Indicadores** .  
  
> [!TIP]  
>  Em um arquivo de código longo, pode ser útil organizar os indicadores em pastas relacionadas a tarefas. A seleção de uma pasta habilita os botões **Ir para o indicador anterior na pasta** e **Ir para o próximo indicador na pasta** .  
  
 **Mover o ponto de intercalação para o indicador anterior**  
 Seleciona o indicador anterior que está habilitado na janela **Indicadores** . Quando o primeiro indicador é atingido, ele volta ao último. Conforme necessário, abre o arquivo onde está o indicador selecionado no Editor. Rola esse documento até a linha marcada e coloca o ponto de inserção nesse local.  
  
 **Mover o sinal de intercalação para o próximo indicador**  
 Seleciona o próximo indicador que está habilitado na janela **Indicadores** . Quando o último indicador é atingido, ele volta ao primeiro. Conforme necessário, abre o arquivo onde está o indicador selecionado no Editor. Rola esse documento até a linha marcada e coloca o ponto de inserção nesse local.  
  
 **Mover o ponto de intercalação para o indicador anterior na pasta atual**  
 Seleciona o indicador anterior que está habilitado dentro da mesma pasta na janela **Indicadores** . Quando o primeiro indicador é atingido, volta para o último daquela pasta. Conforme necessário, abre o arquivo onde está o indicador selecionado no Editor. Rola esse documento até a linha marcada e coloca o ponto de inserção nesse local.  
  
 **Mover o ponto de intercalação para o próximo indicador na pasta atual**  
 Seleciona o próximo indicador que está habilitado dentro da mesma pasta na janela **Indicadores** . Quando o primeiro indicador é atingido, volta para o primeiro daquela pasta. Conforme necessário, abre o arquivo onde está o indicador selecionado no Editor. Rola esse documento até a linha marcada e coloca o ponto de inserção nesse local.  
  
 **Desabilitar/Habilitar Todos os Indicadores**  
 Desmarca ou habilita as caixas de seleção para todos os indicadores na janela **Indicadores** . Não remove indicadores ou altera as linhas de código que eles marcam.  
  
 **Delete (excluir)**  
 Remove o indicador atualmente selecionado na janela **Indicadores** e do documento em que está o indicador. Não remove a linha de código que continha o indicador.  
  
 Caixas de seleção de indicadores  
 Cada indicador possui sua própria caixa de seleção. Para ativar um indicador existente, marque sua caixa de seleção na janela **Indicadores** . Para ocultar (mas não remover) um indicador existente, desmarque sua caixa de seleção na janela **Indicadores** .  
  
## <a name="bookmarks-window-shortcut-menu"></a>Menu de atalho da janela Indicadores  
 Quando você clica com o botão direito do mouse em uma entrada na janela **Indicadores** , os comandos seguintes estão disponíveis no menu de atalho.  
  
 **Delete (excluir)**  
 Remove o indicador atualmente selecionado na janela **Indicadores** e do documento em que está o indicador. Não remove a linha de código que continha o indicador.  
  
 **Renomear**  
 Permite atribuir um novo nome para exibição para um indicador ou uma pasta.  
  
 **Desabilitar/Habilitar Indicador**  
 Limpa ou habilita a caixa de seleção para o indicador selecionado na janela **Indicadores** . Não remove o indicador ou altera a linhas de código que ele marca.  
  
 **Desabilitar/Habilitar Todos os Indicadores**  
 Desmarca ou habilita as caixas de seleção para todos os indicadores na janela **Indicadores** . Não remove indicadores ou altera as linhas de código que eles marcam.  
  
## <a name="see-also"></a>Consulte Também  
 [Atalhos de teclado do SQL Server Management Studio](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)  
