---
description: Definição de dados MDX – CREATE SET
title: Instrução CREATE SET (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d1712d109f7aa984e4b7b2b2a5512ce043869aad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483879"
---
# <a name="mdx-data-definition---create-set"></a>Definição de dados MDX – CREATE SET


  Cria um conjunto nomeado com escopo de sessão para o cubo atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE [SESSION] [ STATIC | DYNAMIC ] [HIDDEN] SET   
   CURRENTCUBE | Cube_Name  
      .Set_Name AS 'Set_Expression'  
      [,Property_Name = Property_Value, ...n]  
```  
  
## <a name="arguments"></a>Argumentos  
 *Cube_Name*  
 Uma expressão de cadeia de caracteres válida que fornece o nome do cubo.  
  
 *Set_Name*  
 Uma expressão de cadeia de caracteres válida que fornece o nome para o conjunto nomeado que está sendo criado.  
  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Property_Name*  
 Uma cadeia de caracteres válida que fornece o nome de uma propriedade de conjunto.  
  
 *Property_Value*  
 Uma expressão escalar válida que define o valor de propriedade de conjunto.  
  
## <a name="remarks"></a>Comentários  
 Um conjunto nomeado é um conjunto de membros de dimensão (ou uma expressão que define um conjunto) que você cria para usar novamente. Por exemplo, um conjunto nomeado possibilita a definição de um conjunto de membros de dimensão que consiste no conjunto das dez principais lojas por vendas. Esse conjunto pode ser definido estaticamente ou por meio de uma função como [TopCount](../mdx/topcount-mdx.md). Esse conjunto nomeado pode ser usado onde quer que o conjunto das 10 lojas principais se faça necessário.  
  
 A instrução CREATE SET cria um conjunto nomeado que permanece disponível em toda a sessão e, portanto, pode ser usada em várias consultas em uma sessão. Para obter mais informações, consulte [Criando membros calculados no escopo da sessão &#40;&#41;MDX ](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members).  
  
 Também é possível definir um conjunto nomeado para ser usado por uma consulta única. Para definir tal conjunto, use a cláusula WITH na instrução SELECT. Para obter mais informações sobre a cláusula WITH, consulte [criando conjuntos nomeados no escopo da consulta &#40;&#41;MDX ](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets).  
  
 A cláusula *Set_Expression* pode conter qualquer função que ofereça suporte à sintaxe MDX. Conjuntos criados com a instrução CREATE SET que não especifiquem a cláusula SESSION têm escopo de sessão. Use a cláusula WITH para criar um conjunto com escopo de consulta.  
  
 A especificação de um cubo diferente daquele conectado no momento causa um erro. Portanto, deve-se usar CURRENTCUBE no lugar de um nome de cubo para indicar o cubo atual.  
  
## <a name="scope"></a>Escopo  
 Um conjunto definido pelo usuário pode ocorrer dentro de um dos escopos listados na tabela a seguir.  
  
 Escopo da consulta  
 A visibilidade e o tempo de vida do conjunto estão limitados à consulta. O conjunto é definido como uma consulta individual. Escopo de consulta substitui escopo de sessão. Para obter mais informações, consulte [criando conjuntos nomeados com escopo de consulta &#40;&#41;MDX ](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/mdx-named-sets-creating-query-scoped-named-sets).  
  
 Escopo de sessão  
 A visibilidade e o tempo de vida do conjunto estão limitados à sessão em que são criados. (O tempo de vida é menor que a duração da sessão se uma instrução DROP SET é emitida no conjunto.) A instrução CREATE SET cria um conjunto com escopo de sessão. Use a cláusula WITH para criar um conjunto com escopo de consulta.  
  
### <a name="example"></a>Exemplo  
 O exemplo a seguir cria um conjunto chamado Core Products. A consulta de SELECT demonstra isso chamando o conjunto recentemente criado. A instrução CREATE SET deve ser executada antes da execução da consulta SELECT – elas não podem ser executadas no mesmo lote.  
  
```  
CREATE SET [Adventure Works].[Core Products] AS '{[Product].[Category].[Bikes]}'  
  
SELECT [Core Products] ON 0  
  FROM [Adventure Works]  
```  
  
## <a name="set-evaluation"></a>Avaliação de conjunto  
 A avaliação de conjunto pode ser definida para ocorrer de maneira diferente; ela pode ser definida para ocorrer somente uma vez, quando da criação do conjunto, ou pode ser definida para ocorrer sempre que o conjunto for usado.  
  
 STATIC  
 Indica que o conjunto só é avaliado uma vez, quando a instrução CREATE SET é avaliada.  
  
 DYNAMIC  
 Indica que o conjunto será avaliado toda vez que for usado em uma consulta.  
  
## <a name="set-visibility"></a>Visibilidade do conjunto  
 O conjunto pode ser visível ou não para outros usuários que consultam o cubo.  
  
 HIDDEN  
 Especifica que o conjunto não é visível a usuários que consultam o cubo.  
  
## <a name="standard-properties"></a>Propriedades padrão  
 Cada conjunto tem um conjunto de propriedades padrão. Quando um aplicativo cliente é conectado ao [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , as propriedades padrão têm suporte ou estão disponíveis para serem compatíveis, conforme escolhe o administrador.  
  
|Identificador de propriedade|Significado|  
|-------------------------|-------------|  
|CAPTION|Uma cadeia de caracteres que o aplicativo cliente usa como legenda para o conjunto.|  
|DISPLAY_FOLDER|Uma cadeia de caracteres que identifica o caminho da pasta de exibição que o aplicativo cliente usa para mostrar o conjunto. O separador de nível de pasta é definido pelo aplicativo cliente. Para as ferramentas e os clientes fornecidos pelo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , a barra invertida ( \\ ) é o separador de nível. Para fornecer várias pastas de exibição para um conjunto definido, use um ponto-e-vírgula (;) para separar as pastas.|  
  
## <a name="see-also"></a>Consulte Também  
 [Instrução DROP SET &#40;MDX&#41;](../mdx/mdx-data-definition-drop-set.md)   
 [Instruções de definição de dados MDX &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
