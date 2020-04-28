---
title: Criar pacotes programaticamente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 7474b1f4-7607-4f28-a6fd-67f7db1dd3f8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f4227560fbaf3e618a25e3dd214a214ac68a736e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176551"
---
# <a name="building-packages-programmatically"></a>Compilando pacotes programaticamente
  Se precisar criar pacotes dinamicamente ou gerenciar e executar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] fora do ambiente de desenvolvimento, você poderá manipular pacotes programaticamente. Nessa abordagem, você tem uma série de opções:

-   Carregue e execute um pacote existente sem modificação.

-   Carregue um pacote existente, reconfigure-o (por exemplo, para uma fonte de dados diferente) e execute-o.

-   Crie um pacote novo, adicione e configure os componentes, objeto por objeto e propriedade por propriedade, salve-o e execute-o.

 É possível usar o modelo de objeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para escrever um código que crie, configure e execute pacotes em qualquer linguagem de programação gerenciada. Por exemplo, talvez você queira criar pacotes orientados a metadados que configurem suas conexões ou fontes de dados, transformações e destinos com base na fonte de dados selecionada e em suas tabelas e colunas.

 Essa seção descreve e demonstra como criar e configurar um pacote programaticamente linha a linha. Na extremidade menos complexa da gama de opções de programação de pacotes, você pode simplesmente carregar e executar um pacote existente sem fazer modificações, conforme descrito em [Executar e gerenciar pacotes programaticamente](../run-manage-packages-programmatically/running-and-managing-packages-programmatically.md).

 Uma opção intermediária não descrita aqui é o carregamento de um pacote existente como um modelo, sua reconfiguração (por exemplo, para outra fonte de dados) e sua execução. Você também pode usar as informações dessa seção para modificar os objetos existentes em um pacote.

> [!NOTE]
>  Ao usar um pacote existente como modelo e modificar colunas existentes no fluxo de dados, talvez você precise remover colunas existentes e chamar o método <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ReinitializeMetaData%2A> de componentes afetados.

## <a name="in-this-section"></a>Nesta seção
 [Criando um pacote programaticamente](../building-packages-programmatically/creating-a-package-programmatically.md) Descreve como criar um pacote programaticamente.

 [Adicionando tarefas programaticamente](../building-packages-programmatically/adding-tasks-programmatically.md) Descreve como adicionar tarefas ao pacote.

 [Conectando tarefas programaticamente](../building-packages-programmatically/connecting-tasks-programmatically.md) Descreve como controlar a execução de contêineres e tarefas em um pacote com base no resultado da execução de uma tarefa ou contêiner anterior.

 [Adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md) Descreve como adicionar gerenciadores de conexões a um pacote.

 [Trabalhando com variáveis programaticamente](../building-packages-programmatically/working-with-variables-programmatically.md) Descreve como adicionar e usar variáveis durante a execução do pacote.

 [Manipulando eventos programaticamente](../building-packages-programmatically/handling-events-programmatically.md) Descreve como lidar com eventos de pacote e tarefa.

 [Habilitando o log de forma programática](../building-packages-programmatically/enabling-logging-programmatically.md) Descreve como habilitar o registro em log para um pacote ou uma tarefa e como aplicar filtros personalizados a eventos de log.

 [Adicionando a tarefa de fluxo de dados programaticamente](../building-packages-programmatically/adding-the-data-flow-task-programmatically.md) Descreve como adicionar e configurar a tarefa de fluxo de dados e seus componentes.

 [Descobrindo componentes de fluxo de dados programaticamente](../building-packages-programmatically/discovering-data-flow-components-programmatically.md) Descreve como detectar os componentes instalados no computador local.

 [Adicionando componentes de fluxo de dados programaticamente](../building-packages-programmatically/adding-data-flow-components-programmatically.md) Descreve como adicionar um componente a uma tarefa de fluxo de dados.

 [Conectando componentes de fluxo de dados programaticamente](../building-packages-programmatically/connecting-data-flow-components-programmatically.md) Descreve como conectar dois componentes de fluxo de dados.

 [Selecionando colunas de entrada programaticamente](../building-packages-programmatically/selecting-input-columns-programmatically.md) Descreve como selecionar colunas de entrada das que são fornecidas a um componente por componentes upstream no fluxo de dados.

 [Salvando um pacote programaticamente](../building-packages-programmatically/saving-a-package-programmatically.md) Descreve como salvar um pacote programaticamente.

## <a name="reference"></a>Referência
 [Integration Services referência de erro e mensagem](../integration-services-error-and-message-reference.md) Lista os códigos [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de erro predefinidos com seus nomes simbólicos e descrições.

## <a name="related-sections"></a>Seções relacionadas
 [Estendendo pacotes com scripts](../extending-packages-scripting/extending-packages-with-scripting.md) Discute como estender o fluxo de controle usando a tarefa Script e como estender o fluxo de dados usando o componente Script.

 [Estendendo pacotes com objetos personalizados](../extending-packages-custom-objects/extending-packages-with-custom-objects.md) Discute como criar tarefas personalizadas do programa, componentes de fluxo de dados e outros objetos de pacote para uso em vários pacotes.

 [Executando e gerenciando pacotes programaticamente](../run-manage-packages-programmatically/running-and-managing-packages-programmatically.md) Discute como enumerar, executar e gerenciar pacotes e as pastas nas quais eles são armazenados.

## <a name="external-resources"></a>Recursos externos

-   Exemplos do CodePlex, [Exemplos de Produtos do Integration Services](https://go.microsoft.com/fwlink/?LinkID=131204), em www.codeplex.com/MSFTISProdSamples

-   Entrada de blog, [Criação de perfil de desempenho de suas extensões personalizadas](https://go.microsoft.com/fwlink/?LinkId=238831), em blogs.msdn.com.

![Ícone de Integration Services (pequeno)](../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.

## <a name="see-also"></a>Consulte Também
 [SQL Server Integration Services](../sql-server-integration-services.md)


