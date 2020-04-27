---
title: Criando subcubos em MDX (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- queries [MDX], subcubes
- subcubes [MDX]
- filtered views [MDX]
- MDX [Analysis Services], subcubes
- Multidimensional Expressions [Analysis Services], subcubes
- CREATE SUBCUBE statement
ms.assetid: 5403a62b-99ac-4d83-b02a-89bf78bf0f46
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 197ee30aa65179e8a434d04d20a5f5b643b42efd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074715"
---
# <a name="building-subcubes-in-mdx-mdx"></a>Criando subcubos em MDX (MDX)
  Um subcubo é um subconjunto de um cubo representando uma exibição filtrada dos dados subjacentes. Limitando o cubo a um subcubo, é possível melhorar o desempenho das consultas.  
  
 Para definir um subcubo, use a instrução [CREATE SUBCUBE](/sql/mdx/mdx-data-definition-create-subcube) , como descrito neste tópico.  
  
## <a name="create-subcube-syntax"></a>Sintaxe de CREATE SUBCUBE  
 Use a sintaxe a seguir para criar um subcubo:  
  
```  
CREATE SUBCUBE Subcube_Identifier AS Subcube_Expression  
```  
  
 A sintaxe de CREATE SUBCUBE é bem simples. O parâmetro *Subcube_Identifier* identifica o cubo que servirá de base para o subcubo. O parâmetro *Subcube_Expression* seleciona a parte do cubo que se tornará o subcubo  
  
 Criado um subcubo, ele passa a ser o contexto de todas as consultas MDX até que a sessão seja encerrada ou você execute a instrução [DROP SUBCUBE](/sql/mdx/mdx-data-definition-drop-subcube) .  
  
### <a name="what-a-subcube-contains"></a>O que um subcubo contém  
 Embora a instrução CREATE SUBCUBE seja bem simples de usar, a instrução em si não mostra explicitamente todos os membros que se tornam parte integrante do subcubo. Aplicam-se as regras a seguir na definição de um subcubo:  
  
-   Se você incluir o membro `(All)` de uma hierarquia, incluirá todos os membros dessa hierarquia.  
  
-   Se você incluir qualquer membro, incluirá seus ascendentes e descendentes.  
  
-   Se você incluir todos os membros de um nível, incluirá todos os membros da hierarquia. Membros de outras hierarquias serão excluídos se eles não existirem com os membros do nível (por exemplo, uma hierarquia desequilibrada, como uma cidade, não contém clientes).  
  
-   Um subcubo sempre conterá todos os membros `(All)` do cubo.  
  
 Além disso, valores de agregação de um subcubo são visualmente totalizados. Por exemplo, um subcubo contém `USA`, `WA`e `OR`. O valor de agregação para `USA` será a soma de `{WA,OR}` , pois `WA` e `OR` são os únicos estados definidos pelo subcubo. Todos os outros estados serão ignorados.  
  
 Além disso, referências explicitas a células fora do subcubo retornarão valores de células que são avaliados no contexto do cubo inteiro. Por exemplo, você cria um subcubo limitado ao ano atual. Você usa a função [ParallelPeriod](/sql/mdx/parallelperiod-mdx) para comparar o ano atual ao anterior. A diferença nos valores será retornada mesmo que o valor do ano anterior esteja fora do subcubo.  
  
 Por fim, se o contexto original não for substituído, as funções de conjunto de uma subseleção serão avaliadas no contexto da subseleção. Se o contexto for substituído, as funções de conjunto serão avaliadas no contexto do cubo inteiro.  
  
## <a name="create-subcube-example"></a>Exemplo de CREATE SUBCUBE  
 O exemplo a seguir cria um subcubo que restringe o cubo Orçamento às contas 4200 e 4300:  
  
 `CREATE SUBCUBE Budget AS SELECT {[Account].[Account].&[4200], [Account].[Account].&[4300] } ON 0 FROM Budget`  
  
 Havendo um subcubo criado para a sessão, qualquer consulta subsequente será feita no subcubo, e não no cubo inteiro. Por exemplo, você executa a consulta abaixo. Ela retornará apenas os membros das contas 4200 e 4300.  
  
 `SELECT [Account].[Account].Members ON 0, Measures.Members ON 1 FROM Budget`  
  
## <a name="see-also"></a>Consulte Também  
 [Estabelecendo o contexto de cubo em uma consulta &#40;MDX&#41;](establishing-cube-context-in-a-query-mdx.md)   
 [Conceitos básicos de consulta MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
