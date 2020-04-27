---
title: Relações de atributo | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- member properties [Analysis Services], attribute relationships
- security [Analysis Services], properties
- PROPERTIES keyword
- storage [Analysis Services], attribute relationships
- natural hierarchies [Analysis Services]
- dimensions [Analysis Services], member properties
- queries [MDX], attribute relationships
- user-defined hierarchies [Analysis Services]
- attributes [Analysis Services], relationships
- member properties [Analysis Services]
- members [Analysis Services], attribute relationships
- storing data [Analysis Services], attribute relationships
- relationships [Analysis Services], attributes
ms.assetid: 2491422a-4cf5-4b23-b6ab-289222b22ce8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 81d51c8778cfbc6e3891dfb3b6783db48f0c65a2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62728512"
---
# <a name="attribute-relationships"></a>Relações de Atributo
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] No [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], os atributos dentro de uma dimensão são sempre relacionados direta ou indiretamente ao atributo de chave. Quando você define uma dimensão com base em um esquema em estrela, onde todos os atributos de dimensão são derivados da mesma tabela relacional, uma relação de atributo é automaticamente definida entre o atributo de chave e cada atributo não chave da dimensão. Quando você define uma dimensão com base em um esquema de floco de neve, onde todos os atributos de dimensão derivam de várias tabelas relacionadas, uma relação de atributo é automaticamente definida da seguinte maneira:  
  
-   Entre o atributo de chave e cada atributo não chave vinculado às colunas na tabela de dimensões principal.  
  
-   Entre o atributo de chave e atributo vinculado à chave estrangeira na tabela secundária que vincula as tabelas de dimensões subjacentes.  
  
-   Entre o atributo vinculado à chave estrangeira na tabela secundária e cada atributo não chave vinculado às colunas da tabela secundária.  
  
 Porém, há vários motivos pelos quais talvez queira alterar essas relações de atributo padrão. Por exemplo, você pode querer definir uma hierarquia natural, uma ordem de classificação personalizada ou uma granularidade de dimensão com base em um atributo não chave. Para obter mais informações, consulte [referência de propriedades de atributo de dimensão](../multidimensional-models/dimension-attribute-properties-reference.md).  
  
> [!NOTE]  
>  Relações de atributo são conhecidas em MDX como propriedades do membro.  
  
## <a name="natural-hierarchy-relationships"></a>Relações de hierarquia natural  
 Uma hierarquia é uma hierarquia natural quando cada atributo incluído na hierarquia definida pelo usuário possui uma relação um para muitos com o atributo imediatamente abaixo dele. Por exemplo, considere uma dimensão Cliente com base em uma tabela fonte relacional com oito colunas:  
  
-   CustomerKey  
  
-   CustomerName  
  
-   Idade  
  
-   Gênero  
  
-   Email  
  
-   City  
  
-   País/Região  
  
-   Região  
  
 A dimensão Analysis Services correspondente tem sete atributos:  
  
-   Cliente (com base em CustomerKey, com CustomerName que fornece os nomes dos membros)  
  
-   Idade, Sexo, Email, Cidade, Região, País  
  
 As relações representando hierarquias naturais são impostas pela criação de uma relação de atributo entre o atributo para um nível e o atributo para o nível abaixo dele. Para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], isso especifica uma relação natural e agregação de potencial. Na dimensão Cliente, uma hierarquia natural existe para os atributos País, Região, Cidade e Cliente. A hierarquia natural para `{Country, Region, City, Customer}` é descrita adicionando-se as seguintes relações de atributo:  
  
-   O atributo País como uma relação com o atributo Região.  
  
-   O atributo Região como uma relação com o atributo Cidade.  
  
-   O atributo Cidade como uma relação com o atributo Cliente.  
  
 Para navegar pelos dados no cubo, você também pode criar uma hierarquia definida pelo usuário que não represente uma hierarquia natural nos dados (que é chamada de hierarquia *ad hoc* ou *relatório* ). Por exemplo, você pode criar uma hierarquia definida pelo usuário com base em `{Age, Gender}`. Os usuários não veem nenhuma diferença em como as duas hierarquias se comportam, embora a hierarquia natural se beneficie das estruturas de agregação e indexação – ocultas do usuário-essa conta para as relações naturais nos dados de origem.  
  
 A propriedade `SourceAttribute` de um nível determina qual atributo é usado para descrever o nível. A propriedade `KeyColumns` no atributo especifica a coluna na exibição da fonte de dados que fornece os membros. A propriedade `NameColumn` no atributo pode especificar um nome de coluna diferente para os membros.  
  
 Para definir um nível em uma hierarquia definida pelo usuário usando [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], o **Designer de dimensão** permite que você selecione um atributo de dimensão, uma coluna em uma tabela de dimensão ou uma coluna de uma tabela relacionada incluída na exibição da fonte de dados para o cubo. Para obter mais informações sobre como criar hierarquias definidas pelo usuário, consulte [criar hierarquias definidas pelo usuário](../multidimensional-models/user-defined-hierarchies-create.md).  
  
 No Analysis Services, uma suposição é normalmente feita sobre o conteúdo dos membros. Os membros folha não têm nenhum descendente e contêm dados derivados de fontes de dados subjacentes. Os membros não folha têm descendentes e contêm dados derivados de agregações executadas em membros filhos. Em níveis de agregação, os membros são com base em agregações de níveis subordinados. Portanto, quando a propriedade `IsAggregatable` estiver configurada como `False` no atributo de origem de um nível, nenhum atributo agregável poderá ser adicionado como nível acima dele.  
  
## <a name="defining-an-attribute-relationship"></a>Definindo uma relação de atributo  
 A principal restrição ao criar uma relação de atributo é certificar-se de que o atributo referenciado pela relação de atributo, não possui mais que um valor para qualquer membro no atributo ao qual a relação de atributo pertence. Por exemplo, se você definir uma relação entre um atributo Cidade e um atributo Estado, cada cidade pode apenas estar relacionada a um único estado.  
  
## <a name="attribute-relationship-queries"></a>Consultas de relação de atributo  
 Você pode usar consultas MDX para recuperar dados de relações de atributo, na forma de propriedades de membro com a palavra-chave `PROPERTIES` da instrução MDX `SELECT`. Para obter mais informações sobre como usar o MDX para recuperar propriedades do membro, consulte [usando propriedades do membro &#40;MDX&#41;](../multidimensional-models/mdx/mdx-member-properties.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Atributos e hierarquias de atributo](attributes-and-attribute-hierarchies.md)   
 [Referência de propriedades de atributo de dimensão](../multidimensional-models/dimension-attribute-properties-reference.md)   
 [Hierarquias de usuário](user-hierarchies.md)   
 [Propriedades de hierarquia do usuário](user-hierarchies-properties.md)  
  
  
