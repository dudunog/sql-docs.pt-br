---
title: Adicionar, excluir, alterar o escopo da variável definida pelo usuário em um pacote | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- variables [Integration Services], adding
ms.assetid: cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 946a9f3ccecfcad30042d0264942836522e64c7d
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439683"
---
# <a name="add-delete-change-scope-of-user-defined-variable-in-a-package"></a>Adicionar, excluir, alterar o escopo de uma variável definida pelo usuário em um pacote
  Estes procedimentos descrevem como adicionar, excluir e alterar o escopo de uma variável definida pelo usuário em um pacote usando a janela **Variáveis** .  
  
 Para obter mais informações sobre escopo variável, consulte [Variáveis do SSIS &#40;Integration Services&#41;](integration-services-ssis-variables.md).  
  
 O [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] também fornece variáveis do sistema que disponibilizam informações sobre o sistema em tempo de execução e podem ser usadas em contêineres como pacotes e manipuladores de eventos. Você não pode excluir as variáveis de sistema.  
  
### <a name="to-add-a-variable"></a>Para adicionar uma variável  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o pacote do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] com o qual você deseja trabalhar.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  No Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] , defina o escopo da variável, seguindo uma das ações:  
  
    -   Para definir o escopo para o pacote, clique na superfície de design da guia **Fluxo de Controle** .  
  
    -   Para definir o escopo a um manipulador de eventos, selecione um executável e um manipulador de eventos na superfície de design da guia **Manipulador de Eventos** .  
  
    -   Para definir o escopo para uma tarefa ou contêiner, na superfície de design da guia **Fluxo de Controle** ou **Manipulador de Eventos** , clique na tarefa ou no contêiner.  
  
4.  No menu **SSIS** , clique em **Variáveis**. Além disso, você pode exibir a janela **Variáveis** mapeando o comando View.Variables para uma combinação de teclas de sua escolha na página **Teclado** da caixa de diálogo **Opções** .  
  
5.  Na janela **variáveis** , clique no ícone **Adicionar variável** . A nova variável é adicionada à lista.  
  
6.  Se desejar, clique no ícone **Opções de Grade** , selecione as colunas adicionais a serem exibidas na caixa de diálogo **Opções de Grade Variáveis** e clique em **OK**.  
  
7.  Como opção, define as propriedades de variáveis. Para obter mais informações, consulte [Definir as propriedades de uma variável definida pelo usuário](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md).  
  
8.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
### <a name="to-delete-a-variable"></a>Para excluir uma variável  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse no pacote para abri-lo.  
  
3.  No menu **SSIS** , clique em **Variáveis**. Além disso, você pode exibir a janela **Variáveis** mapeando o comando View.Variables para uma combinação de teclas de sua escolha na página **Teclado** da caixa de diálogo **Opções** .  
  
4.  Selecione a variável a ser excluída e clique em **Excluir Variável**.  
  
     Se você não vir a variável na janela variáveis, clique em **Opções de grade** e selecione **Mostrar variáveis de todos os escopos**.  
  
5.  Se a caixa de diálogo **Confirmar Exclusão de Variáveis** abrir, clique em **Sim** para confirmar.  
  
6.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
### <a name="to-change-the-scope-of-a-variable"></a>Para alterar o escopo de uma variável  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse no pacote para abri-lo.  
  
3.  No menu **SSIS** , clique em **Variáveis**. Além disso, você pode exibir a janela **Variáveis** mapeando o comando View.Variables para uma combinação de teclas de sua escolha na página **Teclado** da caixa de diálogo **Opções** .  
  
4.  Selecione a variável e clique em **Mover Variável**.  
  
     Se você não vir a variável na janela variáveis, clique em **Opções de grade** e selecione **Mostrar variáveis de todos os escopos**.  
  
5.  Na caixa de diálogo **Selecionar Novo Escopo** , selecione o pacote ou um contêiner, tarefa ou manipulador de eventos no pacote, para alterar o escopo variável.  
  
6.  Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services &#40;as variáveis&#41; SSIS](integration-services-ssis-variables.md)   
 [Usar variáveis em pacotes](../../2014/integration-services/use-variables-in-packages.md)   
 [Definir as propriedades de uma variável definida pelo usuário](../../2014/integration-services/set-the-properties-of-a-user-defined-variable.md)   
 [Usar os valores de variáveis e parâmetros em um pacote filho](../../2014/integration-services/use-the-values-of-variables-and-parameters-in-a-child-package.md)  
  
  
