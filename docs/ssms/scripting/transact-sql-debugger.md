---
title: Depurador do Transact-SQL
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: scripting
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, introduction
ms.assetid: 6e914699-0d85-46c2-aa2d-3e339ac2c4ce
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 12/04/2019
monikerRange: '>= sql-server-2014 || = sqlallproducts-allversions'
ms.openlocfilehash: 8e705be1cda43f0645b53f74f3f658a5bc8c2f2c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75252999"
---
# <a name="transact-sql-debugger"></a>Depurador do Transact-SQL

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] ajuda a localizar erros em códigos [!INCLUDE[tsql](../../includes/tsql-md.md)] investigando o comportamento do código em tempo real. Depois de definir a janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para modo de depuração, você pode pausar a execução em linhas específicas do código e inspecionar informações e dados que são usados por essas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] ou retornadas por elas.

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="stepping-through-transact-sql-code"></a>Como executar o código Transact-SQL em etapas

O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] fornece as seguintes opções, que você pode usar para navegar pelo código [!INCLUDE[tsql](../../includes/tsql-md.md)] quando a janela Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] está em modo de depuração:

- Definir pontos de interrupção em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] individuais.

    Um ponto de interrupção especifica um ponto no qual você deseja que a execução seja pausada para que seja possível examinar os dados. Quando você inicia o depurador, ele pausa na primeira linha de código da janela Editor de Consultas. Para executar ao primeiro ponto de interrupção que você definiu, você pode usar o recurso **Continuar** . Você também pode usar o recurso **Continuar** para executar o próximo ponto de interrupção em qualquer local em que a janela esteja pausada no momento. Você pode editar pontos de interrupção para especificar ações, como as condições sob as quais o ponto de interrupção deve pausar a execução, as informações para imprimir na janela **saída** e alterar o local do ponto de interrupção.  

- Avançar para a próxima instrução.  

    Esta opção permite navegar por um conjunto de instruções, uma a uma, e observar o comportamento delas à medida que você avança.  

- Avançar para ou passar por uma chamada para um procedimento armazenado ou função.  

    Se tiver certeza de que não há erros em um procedimento armazenado, você poderá passar por ele. O procedimento é executado por completo, e os resultados são retornados ao código.  

    Se você desejar depurar um procedimento armazenado ou uma função, poderá avançar no módulo. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] abre uma nova janela do Editor de Consultas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que é preenchida com o código de origem do módulo, coloca a janela no modo de depuração e pausa a execução na primeira instrução do módulo. Em seguida, você pode navegar pelo código do módulo, por exemplo, definindo pontos de interrupção ou percorrendo o código.  

Para obter mais informações sobre como o depurador permite navegar pelo código, veja [Percorrer código Transact-SQL](../../relational-databases/scripting/step-through-transact-sql-code.md).  

## <a name="viewing-debugger-information"></a>Como exibir informações do depurador

Toda vez que o depurador pausa a execução em uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] específica, você pode usar as seguintes janelas do depurador para exibir o estado de execução atual:  

- **Locais** e **Inspecionar.** Essas janelas exibem expressões [!INCLUDE[tsql](../../includes/tsql-md.md)] alocadas no momento. Expressões são cláusulas [!INCLUDE[tsql](../../includes/tsql-md.md)] que são avaliadas como uma única expressão escalar. O depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] dá suporte à exibição de expressões que fazem referência a variáveis [!INCLUDE[tsql](../../includes/tsql-md.md)], parâmetros ou as funções internas que têm nomes que começam com @@. Essas janelas também exibem os valores de dados que estão atribuídos às expressões no momento.  

- **QuickWatch.** Essa janela exibe o valor de uma expressão [!INCLUDE[tsql](../../includes/tsql-md.md)] e permite salvar essa expressão em uma janela **Inspecionar** .  

- **Pontos de interrupção.** Esta janela exibe os pontos de interrupção definidos no momento e permite gerenciá-los.  

- **Pilha de Chamadas.** Esta janela exibe o local de execução atual. Fornece também informações sobre como a execução passou da janela Editor de Consultas original por meio de funções, procedimentos armazenados ou gatilhos para alcançar o local de execução atual.  

- **Saída.** Esta janela exibe várias mensagens e dados de programa, como, por exemplo, mensagens de sistema do depurador.  

- **Resultados** e **Mensagens.** Essas guias da janela Editor de Consultas exibem os resultados de instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] executadas anteriormente.  

## <a name="transact-sql-debugger-tasks"></a>Tarefas do depurador do Transact-SQL  

|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como configurar o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] para a depuração remota.|[Configurar regras de firewall antes de executar o Depurador do TSQL](../../relational-databases/scripting/configure-firewall-rules-before-running-the-tsql-debugger.md)|  
|Descreve como iniciar, interromper e controlar a operação do depurador.|[Executar o depurador do Transact-SQL](../../relational-databases/scripting/run-the-transact-sql-debugger.md)|  
|Descreve como usar o depurador [!INCLUDE[tsql](../../includes/tsql-md.md)] para percorrer o código.|[Percorrer o código do Transact-SQL](../../relational-databases/scripting/step-through-transact-sql-code.md)|  
|Descreve como usar o depurador para exibir dados [!INCLUDE[tsql](../../includes/tsql-md.md)] , como, por exemplo, parâmetros e variáveis e informações do sistema.|[Informações do depurador Transact-SQL](../../relational-databases/scripting/transact-sql-debugger-information.md)|  

## <a name="see-also"></a>Confira também

[Editores de consultas e de texto &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)
