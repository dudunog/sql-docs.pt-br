---
title: Contêiner do Loop For | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.forloopcontainerdetails.f1
helpviewer_keywords:
- repeating control flow
- containers [Integration Services], For Loop
- For Loop containers
ms.assetid: 44cf7355-992b-4bbf-a28c-bfb012de06f6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ec872407dbec3885f72c4300b90cb3e11d1bcf92
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85433033"
---
# <a name="for-loop-container"></a>Contêiner Loop For
  O contêiner Loop For define um fluxo de controle repetitivo em um pacote. A implementação de loop é semelhante à estrutura de loop **For** em linguagens de programação. Em cada repetição do loop, o contêiner Loop For avalia uma expressão e repete seu fluxo de trabalho até a expressão ser avaliada como `False`.  
  
 O contêiner Loop For usa os seguintes elementos para definir o loop:  
  
-   Uma expressão de inicialização opcional que atribui valores aos contadores de loop.  
  
-   Uma expressão de avaliação que contém a expressão usada para testar se o loop deve parar ou continuar.  
  
-   Uma expressão de iteração opcional que incrementa ou diminui o contador de loop.  
  
 O diagrama a seguir mostra um contêiner Loop For com uma tarefa Enviar Email. Se a expressão de inicialização é `@Counter = 0`, a expressão de avaliação é `@Counter < 4`e a expressão de iteração é `@Counter = @Counter + 1`, o loop é repetido quatro vezes e envia quatro mensagens de email.  
  
 ![Um contêiner Loop For repete uma tarefa quatro vezes](../media/ssis-forloop.gif "Um contêiner Loop For repete uma tarefa quatro vezes")  
  
 As expressões devem ser expressões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] válidas.  
  
 Para criar as expressões de inicialização e de atribuição, você pode usar o operador de atribuição (=). Não há suporte para esse operador pela gramática de expressão do Integration Services e só pode ser usado pelos tipos de expressão de inicialização e de atribuição no contêiner Loop For. Qualquer expressão que usa o operador de atribuição deve ter a sintaxe `@Var = <expression>` , em que **var** é uma variável de tempo de execução e \<expression> é uma expressão que segue as regras da [!INCLUDE[ssIS](../../../includes/ssis-md.md)] sintaxe da expressão. A expressão pode incluir as variáveis, literais e quaisquer operadores e funções que a gramática de expressão SSIS ofereça suporte. A expressão deve avaliar um tipo de dados que pode ser convertido em tipo de dados da variável.  
  
 Um contêiner Loop For pode ter só uma expressão de avaliação. Isso significa que o contêiner Loop For executa todos os seus elementos de fluxo de controle o mesmo número de vezes. Como o contêiner Loop For pode incluir outros contêineres Loop For, você pode construir loops aninhados e implementar loop complexo em pacotes.  
  
 Você pode definir uma propriedade de transação no contêiner Loop For para estabelecer uma transação para um subconjunto do fluxo de controle de pacote. Desse modo, é possível gerenciar as transações em um nível mais granular. Por exemplo, se um contêiner Loop For repetir um fluxo de controle que atualiza dados em uma tabela várias vezes, você poderá configurar o Loop For e seu fluxo de controle para usar uma transação para garantir que, se todos os dados não forem atualizados com êxito, nenhum dado seja atualizado. Para obter mais informações, consulte [Transações do Integration Services](../integration-services-transactions.md).  
  
## <a name="configuration-of-the-for-loop-container"></a>Configuração do contêiner Loop For  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no [!INCLUDE[ssIS](../../../includes/ssis-md.md)] Designer, clique em um dos seguintes tópicos:  
  
-   [Editor do Loop For](../for-loop-editor.md)  
  
-   [Página Expressões](../expressions/expressions-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades programaticamente, consulte a documentação da classe **T:Microsoft.SqlServer.Dts.Runtime.ForLoop** no Guia do Desenvolvedor.  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter informações sobre como configurar um contêiner Loop For, consulte os tópicos a seguir:  
  
-   [Configurar um contêiner Loop For](for-loop-container.md)  
  
-   [Definir as propriedades de uma tarefa ou de um contêiner](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Fluxo de Controle](control-flow.md)   
 [Expressões do SSIS &#40;Integration Services&#41;](../expressions/integration-services-ssis-expressions.md)  
  
  
