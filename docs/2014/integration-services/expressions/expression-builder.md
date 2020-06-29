---
title: Construtor de Expressões | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.expressionbuilder.f1
helpviewer_keywords:
- Expression Builder dialog box
ms.assetid: 4717ce33-bd4e-44bc-81e0-002de075b4d1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6f82b14f267cd9e62e526004e078ed78d151eeea
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85428783"
---
# <a name="expression-builder"></a>Construtor de Expressões
  Use a caixa de diálogo **Construtor de Expressões** para criar e editar uma expressão de propriedade ou para gravar a expressão que define o valor de uma variável usando uma interface gráfica do usuário que lista as variáveis e oferece uma referência interna às funções, às conversões de tipo e aos operadores que a linguagem de expressão [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui.  
  
 Uma expressão de propriedades é uma expressão que é atribuída a uma propriedade. Quando a expressão é avaliada, a propriedade é atualizada de forma dinâmica para usar o resultado da avaliação da expressão. Do mesmo modo, uma expressão usada em uma variável permite que o valor da mesma seja atualizado com o resultado da avaliação da expressão.  
  
 Há vários modos em que usar as expressões:  
  
-   **Tarefas** Atualize a linha Para que uma tarefa Enviar Mensagem usa inserindo um endereço de email armazenado em uma variável ou atualize a linha do Assunto concatenando uma cadeia de caracteres como “Vendas para:” e a data atual retornada pela função GETDATE.  
  
-   **Variáveis** Defina o valor de uma variável para o mês atual usando uma expressão como `DATEPART("mm",GETDATE())`; ou defina o valor de uma cadeia de caracteres concatenando esta cadeia literal e a data atual usando a expressão `"Today's date is " + (DT_WSTR,30)(GETDATE())`.  
  
-   **Gerenciadores de Conexões** Defina a página do código de um gerenciador de conexões de Arquivo Simples usando uma variável que contém um identificador de página de código diferente ou especifique o número de linhas no arquivo de dados a serem ignoradas, digitando um inteiro positivo como 3 na expressão.  
  
 Para saber mais sobre expressões de propriedade e como escrever expressões, consulte [Usar expressões de propriedade em pacotes](use-property-expressions-in-packages.md) e [Expressões do Integration Services &#40;SSIS&#41;](integration-services-ssis-expressions.md).  
  
## <a name="options"></a>Opções  
  
|Termo|Definição|  
|----------|----------------|  
|**Variáveis**|Expanda a pasta de **Variáveis** e arraste as mesmas para a caixa **Expressão** .|  
|**Funções matemáticas**<br /><br /> **Funções de cadeia de caracteres**<br /><br /> **Funções Data/Hora**<br /><br /> **Funções NULL**<br /><br /> **Conversões de Tipos**<br /><br /> **Operadores**|Expanda as pastas e arraste as funções, conversões de tipos e operadores para a caixa **Expressão** .|  
|**Expression**|Edite ou digite uma expressão.'|  
|**Valor avaliado**|Lista o resultado da avaliação da expressão.|  
|**Avaliar Expressão**|Clique em **Avaliar Expressão** para exibir o resultado de avaliação da expressão.|  
  
## <a name="see-also"></a>Consulte Também  
 [Página Expressões](expressions-page.md)   
 [Editor de expressões de propriedades](property-expressions-editor.md)   
 [Variáveis do SSIS &#40;Integration Services&#41;](../integration-services-ssis-variables.md)   
 [Variáveis do sistema](../system-variables.md)  
  
  
