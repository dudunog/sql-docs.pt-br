---
title: Usar variáveis no componente de Script | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- Script component [Integration Services], using variables
ms.assetid: 92d1881a-1ef1-43ae-b1ca-48d0536bdbc2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bb913313c77ca98cb3155afa73aab533918fd3de
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85426053"
---
# <a name="using-variables-in-the-script-component"></a>Usando variáveis no componente Script
  As variáveis armazenam valores que um pacote e seus contêineres, tarefas e manipuladores de eventos podem usar em tempo de execução. Para obter mais informações, consulte [Variáveis do SSIS &#40;Integration Services&#41;](../../integration-services-ssis-variables.md).  
  
 Você pode disponibilizar as variáveis existentes para acesso somente leitura ou de leitura/gravação por seu script personalizado, inserindo listas delimitadas por vírgulas de variáveis nos `ReadOnlyVariables` `ReadWriteVariables` campos e na página **script** do **Editor de transformação scripts**. Lembre-se de que os nomes de variáveis diferenciam maiúsculas de minúsculas. Use a propriedade `Value` para ler e gravar em variáveis individuais. O componente Script trata qualquer bloqueio necessário em segundo plano, à medida que seu script manipula as variáveis em tempo de execução.  
  
> [!IMPORTANT]  
>  A coleção de `ReadWriteVariables` está disponível somente no método `PostExecute` para maximizar o desempenho e minimizar o risco de conflitos de bloqueio. Portanto, não será possível incrementar diretamente o valor de uma variável de pacote ao processar cada linha de dados. Em vez disso, incremente o valor de uma variável local e defina o valor da variável do pacote como o valor da variável local no método `PostExecute` depois de todos os dados terem sido processados. Você também pode usar a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> para funcionar nesta limitação, conforme descrito posteriormente neste tópico. Entretanto, gravar diretamente em uma variável de pacote, à medida que cada linha for processada, afetará negativamente o desempenho e aumentará o risco de conflitos de bloqueio.  
  
 Para obter mais informações sobre a página **Script** do **Editor de Transformação Scripts**, consulte [Configurando o componente Script no Editor de Componentes de Script](configuring-the-script-component-in-the-script-component-editor.md) e [Editor de Transformação Scripts &#40;Página Script&#41;](../../script-transformation-editor-script-page.md).  
  
 O componente Script cria uma classe de coleção `Variables` no item de projeto `ComponentWrapper` com uma propriedade de acessador com rigidez de tipos para o valor de cada variável pré-configurada  onde a propriedade tem o mesmo nome que a variável em si. Esta coleção é exposta pela propriedade `Variables` da classe `ScriptMain`. A propriedade de acessador fornece permissão somente leitura ou de leitura/gravação ao valor da variável conforme apropriado. Por exemplo, se você tiver adicionado uma variável de inteiro nomeada `MyIntegerVariable` à lista `ReadOnlyVariables`, poderá recuperar seu valor em seu script utilizando o seguinte código:  
  
 `Dim myIntegerVariableValue As Integer = Me.Variables.MyIntegerVariable`  
  
 Você também pode usar a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>, acessada chamando `Me.VariableDispenser`, para trabalhar com variáveis no componente Script. Neste caso você não está utilizando as propriedades de acessador digitadas e nomeadas para variáveis, mas acessando as variáveis diretamente. Ao usar o <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A>, você deve tratar as semânticas de bloqueio e a conversão de tipos de dados para obter valores variáveis em seu próprio código. Você deve usar a propriedade <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.VariableDispenser%2A> em vez das propriedades de acessador nomeadas e tipadas, se desejar trabalhar com uma variável que não esteja disponível no tempo de design, mas é criada programaticamente no tempo de execução.  
  
![Ícone de Integration Services (pequeno)](../../media/dts-16.gif "Ícone do Integration Services (pequeno)")  **Mantenha-se atualizado com Integration Services**<br /> Para obter os downloads, artigos, exemplos e vídeos mais recentes da Microsoft, assim como soluções selecionadas pela comunidade, visite a página do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] no MSDN:<br /><br /> [Visite a página do Integration Services no MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para receber uma notificação automática dessas atualizações, assine os RSS feeds disponíveis na página.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services &#40;as variáveis&#41; SSIS](../../integration-services-ssis-variables.md)   
 [Usar variáveis em pacotes](../../use-variables-in-packages.md)  
  
  
