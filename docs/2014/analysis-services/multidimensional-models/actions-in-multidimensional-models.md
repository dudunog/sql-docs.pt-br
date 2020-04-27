---
title: Ações em modelos multidimensionais | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- actions [Analysis Services], creating
- report actions [Analysis Services]
- drillthrough actions [Analysis Services]
- cubes [Analysis Services], actions
ms.assetid: b9fee2b9-05a5-4077-848d-d8457326dc27
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 825343c58feeb7ffb217a8b1c8c53d8f81ae7441
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66077501"
---
# <a name="actions-in-multidimensional-models"></a>Ações em modelos multidimensionais
  Uma ação é uma operação iniciada pelo usuário final em um cubo selecionado ou em parte de um cubo. A operação pode iniciar um aplicativo com o item selecionado como parâmetro ou pode recuperar informações sobre o item selecionado. Para obter mais informações sobre ações, consulte [Ações &#40;Analysis Services – Dados Multidimensionais&#41;](actions-analysis-services-multidimensional-data.md).  
  
 Use a guia **Ações** do Designer de Cubo para criar ações para um cubo. Especifique o seguinte:  
  
 **Nome**  
 Selecione um nome que identifica a ação.  
  
 **Destino da Ação**  
 Selecione o objeto ao qual a ação será anexada. Em geral, em aplicativos cliente, a ação é exibida quando os usuários finais selecionam o objeto de destino; no entanto, o aplicativo cliente determina qual operação do usuário final exibe ações. Para **Tipo de destino**, selecione entre os objetos a seguir:  
  
-   Membros de atributo  
  
-   Células  
  
-   Cube  
  
-   Membros de dimensão  
  
-   Hierarquia  
  
-   Membros de hierarquia  
  
-   Nível  
  
-   Membros de nível  
  
 Depois de selecionar o tipo de objeto de destino, em **Objeto de destino**, selecione o objeto de cubo do tipo designado.  
  
 **Condição (Opcional)**  
 Especifique uma expressão MDX opcional que resolve um valor booliano. Se o valor for `True`, a ação será executada no destino especificado. Se for `False`, a ação não será executada.  
  
 **Conteúdo da Ação**  
 Selecione o tipo de ação. A tabela a seguir resume os tipos disponíveis:  
  
|Tipo|Descrição|  
|----------|-----------------|  
|Conjunto de Dados|Recupera um conjunto de dados.|  
|Proprietário|Executa uma operação usando uma interface diferente das listadas nesta tabela.|  
|Conjunto de Linhas|Recupera um conjunto de linhas.|  
|de|Executa um comando OLE DB.|  
|URL|Exibe uma página variável em um navegador de Internet.|  
  
 Para **Expressão da Ação**, especifique os parâmetros que são passados quando a ação é executada. A sintaxe deve avaliar uma cadeia de caracteres e você deve incluir uma expressão escrita em MDX. Por exemplo, a expressão MDX pode indicar uma parte do cubo incluída na sintaxe. Expressões MDX são avaliadas antes de os parâmetros serem passados. Além disso, o Construtor MDX está disponível para lhe ajudar a construir expressões MDX.  
  
 **Propriedades Adicionais**  
 Selecione a propriedade. A tabela a seguir resume as propriedades disponíveis:  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**Invocação**|Especifica como a ação é executada. Interativo, o padrão, especifica que a ação será executada quando um usuário acessar um objeto. Os configurações possíveis são:<br /><br /> Lote<br /><br /> Interactive (Interativo)<br /><br /> Em Aberto|  
|**Aplicativo**|Descreve o aplicativo da ação.|  
|**Descrição**|Descreve a ação.|  
|**Legenda**|Fornece uma legenda que é exibida para a ação. Se a legenda for MDX, especifique `True` for **Caption é MDX**.|  
|**A legenda é MDX**|Especifique `True` se a legenda for MDX ou `False` se não for.|  
  
> [!NOTE]  
>  Use o Analysis Services Scripting Language (ASSL) ou o Objetos de Gerenciamento de Análise (AMO) para definir tipos de ação HTML ou de linha de comando. Para obter mais informações, consulte [Elemento Action &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/objects/action-element-assl), [Elemento Type &#40;Ação&#41; &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/type-element-action-assl) e [Programando objetos OLAP AMO avançados](https://docs.microsoft.com/bi-reference/amo/programming-amo-olap-advanced-objects).  
  
## <a name="creating-a-reporting-action"></a>Criando uma ação de relatório  
 O servidor de relatório responde a solicitações baseadas na URL para relatórios. Para criar uma ação de relatório, no menu **Cubo** , clique em **Nova Ação de Relatório**. As opções a seguir são específicas de uma ação de relatório.  
  
 **Servidor de relatório**  
 As propriedades descritas na tabela a seguir são especificadas para o servidor de relatório.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**Nome do servidor**|O nome do computador que executa o servidor de relatório.|  
|**Caminho do servidor**|O caminho exibido pelo servidor de relatório.|  
|**Formato do relatório**|HTML5, HTML3, Excel ou PDF.|  
  
 **Parâmetros (Opcional)**  
 Os parâmetros serão enviados ao servidor como parte da cadeia de caracteres de URL quando a ação for criada. Incluem **Nome do Parâmetro** e **Valor do Parâmetro**, que são uma expressão MDX.  
  
 A URL do servidor de relatório é construída da seguinte maneira:  
  
```  
  
http://  
host  
/  
virtualdirectory  
/Path&  
parametername1  
=  
parametervalue1  
& ...  
```  
  
 Por exemplo:  
  
```  
http://localhost/ReportServer/Sales/YearlySalesByCategory?rs:Command=Render&Region=West  
```  
  
## <a name="creating-a-drillthrough-action"></a>Criando um ação de detalhamento  
 Uma ação de extração de detalhes é definida por uma ação de conjunto de linhas, retornada ao aplicativo cliente como uma instrução de extração de detalhes. O destino de ação é um membro de um grupo de medidas. Para criar uma nova ação de drillthrough, no menu **Cubo** , clique em **Nova Ação de Drillthrough**. As opções a seguir são específicas de uma ação de extração de detalhes:  
  
 **Colunas de Extração de Detalhes**  
 Selecione uma ou mais dimensões e, para cada uma, as colunas de detalhamento retornadas ao aplicativo cliente pela ação.  
  
## <a name="see-also"></a>Consulte Também  
 [Cubos em modelos multidimensionais](cubes-in-multidimensional-models.md)  
  
  
