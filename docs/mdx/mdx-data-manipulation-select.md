---
description: Manipulação de dados MDX – SELECT
title: Instrução SELECT (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 623d798a3794da7577cf036cb8a32b2cf9cd7b84
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88477008"
---
# <a name="mdx-data-manipulation---select"></a>Manipulação de dados MDX – SELECT


  Recupera dados de um cubo especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
[ WITH <SELECT WITH clause>   
   [ , <SELECT WITH clause>...n ]   
]   
SELECT   
     [ *   
    | ( <SELECT query axis clause>   
                  [ , <SELECT query axis clause>,...n ]   
            )   
            ]  
FROM   
   <SELECT subcube clause>   
      [ <SELECT slicer axis clause> ]  
      [ <SELECT cell property list clause> ]  
  
<SELECT WITH clause> ::=  
     ( CELL CALCULATION <CREATE CELL CALCULATION body clause> )   
   | ( [ CALCULATED ] MEMBER <CREATE MEMBER body clause>)   
   | ( SET <CREATE SET body clause>)  
   | ( MEASURE = <measure body clause> )  
  
<SELECT query axis clause> ::=  
   [ NON EMPTY ] Set_Expression  
   [ <SELECT dimension property list clause> ]   
      ON   
            Integer_Expression   
       | AXIS(Integer)   
       | COLUMNS   
       | ROWS   
       | PAGES   
       | SECTIONS   
       | CHAPTERS   
  
<SELECT subcube clause> ::=  
      Cube_Name   
   | [NON VISUAL] (SELECT   
                  [ *   
       | ( <SELECT query axis clause> [ ,   
           <SELECT query axis clause>,...n ] )   
         ]   
            FROM   
         <SELECT subcube clause>   
         <SELECT slicer axis clause> )  
  
<SELECT slicer axis clause> ::=   
      WHERE Tuple_Expression  
  
<SELECT cell property list clause> ::=   
   [ CELL ] PROPERTIES CellProperty_Name   
      [ , CellProperty_Name,...n ]  
  
<SELECT dimension property list clause> ::=  
   [DIMENSION] PROPERTIES   
      (DimensionProperty_Name   
         [,DimensionProperty_Name,...n ] )   
    | (LevelProperty_Name   
         [, LevelProperty_Name,...n ] )   
    | (MemberProperty_Name   
         [, MemberProperty_Name,...n ] )  
```  
  
## <a name="arguments"></a>Argumentos  
 *Set_Expression*  
 Uma expressão MDX (Multidimensional Expressions) válida que retorna um conjunto.  
  
 *Inteiro*  
 Um inteiro entre 0 e 127.  
  
 *Cube_Name*  
 Uma cadeia de caracteres válida que fornece um nome de cubo.  
  
 *Tuple_Expression*  
 Uma linguagem MDX válida que retorna uma tupla.  
  
 *CellProperty_Name*  
 Uma cadeia de caracteres válida que representa uma propriedade de célula.  
  
 *DimensionProperty_Name*  
 Uma cadeia de caracteres que representa uma propriedade de dimensão.  
  
 *LevelProperty_Name*  
 Uma cadeia de caracteres válida que representa uma propriedade de nível.  
  
 *MemberProperty_Name*  
 Uma cadeia de caracteres válida que representa uma propriedade de membro.  
  
## <a name="remarks"></a>Comentários  
 A expressão `<SELECT slicer axis clause>` deve conter membros em dimensões e hierarquias diferentes daquelas mencionadas nas expressões `<SELECT query axis clause>` especificadas.  
  
 Se um atributo no cubo for omitido das expressões `<SELECT query axis clause>` e do valor `<SELECT slicer axis clause>` especificados, o membro padrão do atributo será implicitamente adicionado ao eixo do slicer.  
  
 A opção NON VISUAL na instrução subselect lhe permite filtrar os membros enquanto mantém os totais verdadeiros, em vez dos totais filtrados. Isso lhe permite consultar as dez vendas principais (pessoas/produtos/regiões) e obter o total verdadeiro das vendas para todos os membros consultados, em vez do valor total das vendas para os dez principais retornados. Veja os exemplos abaixo para obter mais informações.  
  
 Os membros calculados podem ser incluídos no \<SELECT query axis clause> sempre que a conexão for aberta usando as *subconsultas*do parâmetro da cadeia de conexão = 1; consulte [propriedades xmla com suporte &#40;&#41;XMLA ](https://docs.microsoft.com/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) e <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> para uso do parâmetro. Um exemplo é fornecido nos membros calculados em subseleções.  
  
## <a name="autoexists"></a>autoexists  
 Quando dois ou mais atributos da dimensão são usados em uma instrução SELECT, o Analysis Services avalia as expressões dos atributos para assegurar que os membros desses atributos sejam devidamente confinados para atender aos critérios de todos os outros atributos. Por exemplo, vamos supor que você esteja trabalhando com atributos da dimensão Geografia. Se houver uma expressão que retorne todos os membros do atributo Cidade, e outra expressão que confine os membros do atributo País a todos os países na Europa, isso resultará no confinamento dos membros de Cidade apenas às cidades que pertencem a países na Europa. Essas característica do Analysis Services é denominada Autoexists e se aplica apenas aos atributos na mesma dimensão. Autoexists somente se aplica a atributos da mesma dimensão porque tenta impedir que os registros da dimensão excluídos em uma expressão do atributo sejam incluídos pelas outras expressões do atributo. Autoexists também pode ser entendido como a interseção resultante das diferentes expressões de atributo sobre os registros da dimensão. Consulte estes exemplos abaixo:  
  
 `//Obtain the Top 10 best reseller selling products by Name`  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 O conjunto de resultados obtido é:  
  
|Nome do modelo + medidas|Reseller Sales Amount|Valor do desconto|Desconto PCT|  
|-|-|-|-|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13%**|  
|**Road-250**|**$9,377,457.68**|**$4,032.47**|**0, 4%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**Road-650**|**$7,442,141.81**|**$39,698.30**|**0.53%**|  
|**Touring-1000**|**$6,723,794.29**|**$166,144.17**|**2,47%**|  
|**Road-550-W**|**$3,668,383.88**|**$1,901.97**|**0, 5%**|  
|**Road-350-W**|**$3,665,932.31**|**$20,946.50**|**0,57%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0, 1%**|  
|**Road-150**|**$2,363,805.16**|**$0**|**0, 0%**|  
|**Touring-3000**|**$2,046,508.26**|**$79,582.15**|**3,89%**|  
  
 O conjunto obtido com base nos produtos parece ser igual a Preferred10Products; assim, verificando o conjunto Preferred10Products:  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Preferred10Products on 1`  
  
 `from [Adventure Works]`  
  
 De acordo com os resultados a seguir, os dois conjuntos (Top10SellingProducts, Preferred10Products) são iguais  
  
|Nome do modelo + medidas|Reseller Sales Amount|Valor do desconto|Desconto PCT|  
|-|-|-|-|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13%**|  
|**Road-250**|**$9,377,457.68**|**$4,032.47**|**0, 4%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**Road-650**|**$7,442,141.81**|**$39,698.30**|**0.53%**|  
|**Touring-1000**|**$6,723,794.29**|**$166,144.17**|**2,47%**|  
|**Road-550-W**|**$3,668,383.88**|**$1,901.97**|**0, 5%**|  
|**Road-350-W**|**$3,665,932.31**|**$20,946.50**|**0,57%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0, 1%**|  
|**Road-150**|**$2,363,805.16**|**$0**|**0, 0%**|  
|**Touring-3000**|**$2,046,508.26**|**$79,582.15**|**3,89%**|  
  
 Nos exemplos anteriores, nós criamos dois conjuntos: um como uma expressão calculada e o outro como uma expressão constante. Esses exemplos ilustram as diferentes opções de Autoexists.  
  
 Autoexists pode ser aplicado de modo profundo ou superficial às expressões. A configuração padrão é profundamente. O exemplo a seguir ilustrará o conceito de Autoexists profundo. No exemplo, nós estamos filtrando Top10SellingProducts pelo atributo [Product].[Product Line] para os itens no grupo [Mountain]. Observe que os dois atributos (slicer e axis) pertencem a mesma dimensão, [Product].  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `// Preferred10Products set removed for clarity`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 Gera o seguinte conjunto de resultados:  
  
|Nome do modelo + medidas|Reseller Sales Amount|Valor do desconto|Desconto PCT|  
|-|-|-|-|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0, 1%**|  
|**Mountain-300**|**$1,907,249.38**|**$876.95**|**0, 5%**|  
|**Mountain-500**|**$1,067,327.31**|**$17,266.09**|**1,62%**|  
|**Mountain-400-W**|**$592,450.05**|**$303.49**|**0, 5%**|  
|**LL Mountain Frame**|**$521,864.42**|**$252.41**|**0, 5%**|  
|**ML Mountain Frame-W**|**$482,953.16**|**$206.95**|**0, 4%**|  
|**ML Mountain Frame**|**$343,785.29**|**$161.82**|**0, 5%**|  
|**Women's Mountain Shorts**|**$260,304.09**|**$6,675.56**|**2,56%**|  
  
 No conjunto de resultados anterior, havia sete itens novos na lista Top10SellingProducts e Mountain-200, Mountain-100 e HL Mountain Frame foram movidos para o início da lista. No conjunto de resultados anterior, esses três valores foram intercalados  
  
 Isso se chama Deep Autoexists, porque o conjunto Top10SellingProducts é avaliado para atender às condições de divisão da consulta. Deep Autoexists significa que todas as expressões serão avaliadas para atender o espaço mais profundo possível após a aplicação das expressões de segmentação de dados, das expressões de subseleção no eixo etc.  
  
 No entanto, pode ser que alguém queira ser capaz de executar a análise sobre Top10SellingProducts como equivalente a Preferred10Products, como no exemplo a seguir:  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `set Preferred10Products as '`  
  
 `{[Product].[Model Name].&[Mountain-200],`  
  
 `[Product].[Model Name].&[Road-250],`  
  
 `[Product].[Model Name].&[Mountain-100],`  
  
 `[Product].[Model Name].&[Road-650],`  
  
 `[Product].[Model Name].&[Touring-1000],`  
  
 `[Product].[Model Name].&[Road-550-W],`  
  
 `[Product].[Model Name].&[Road-350-W],`  
  
 `[Product].[Model Name].&[HL Mountain Frame],`  
  
 `[Product].[Model Name].&[Road-150],`  
  
 `[Product].[Model Name].&[Touring-3000]`  
  
 `}'`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Preferred10Products on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 Gera o seguinte conjunto de resultados:  
  
|Nome do modelo + medidas|Reseller Sales Amount|Valor do desconto|Desconto PCT|  
|-|-|-|-|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0, 1%**|  
  
 Nos resultados acima, a segmentação de dados dá um resultado que contém apenas os produtos de Preferred10Products que fazem parte do grupo [Mountain] em [Product].[Product Line]; conforme o esperado, porque Preferred10Products é uma expressão constante.  
  
 Esse conjunto de resultados também é entendido como Autoexists superficial. Isso ocorre porque a expressão é avaliada antes da cláusula de divisão. No exemplo anterior, a expressão era uma expressão constante para fins de ilustração, para introduzir o conceito.  
  
 O comportamento de Autoexists pode ser modificado no nível da sessão com o uso da propriedade da cadeia de caracteres de conexão **Autoexists** . O exemplo a seguir começa abrindo uma nova sessão e adicionando a propriedade *Autoexists=3* à cadeia de conexão. Você deve abrir uma nova conexão para executar o exemplo. Após o estabelecimento da conexão com a configuração Autoexist, ela permanecerá em efeito até que a conexão seja encerrada.  
  
 `with member [Measures].[PCT Discount] AS '[Measures].[Discount Amount]/[Measures].[Reseller Sales Amount]', FORMAT_STRING = 'Percent'`  
  
 `set Top10SellingProducts as 'topcount([Product].[Model Name].children, 10, [Measures].[Reseller Sales Amount])'`  
  
 `//Preferred10Products set removed for clarity`  
  
 `select {[Measures].[Reseller Sales Amount], [Measures].[Discount Amount], [Measures].[PCT Discount]} on 0,`  
  
 `Top10SellingProducts on 1`  
  
 `from [Adventure Works]`  
  
 `where [Product].[Product Line].[Mountain]`  
  
 O conjunto de resultados a seguir agora mostra o comportamento superficial de Autoexists.  
  
|Nome do modelo + medidas|Reseller Sales Amount|Valor do desconto|Desconto PCT|  
|-|-|-|-|  
|**Mountain-200**|**$14,356,699.36**|**$19,012.71**|**0,13%**|  
|**Mountain-100**|**$8,568,958.27**|**$139,393.27**|**1,63%**|  
|**HL Mountain Frame**|**$3,365,069.27**|**$174.11**|**0, 1%**|  
  
 O comportamento de autoexisteções pode ser modificado usando o parâmetro Autoexists = [1 | 2 | 3] na cadeia de conexão; consulte [Propriedades XMLA com suporte &#40;&#41;XMLA ](https://docs.microsoft.com/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties) e <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A> para uso de parâmetro.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a soma do `Measures.[Order Quantity]` membro, agregados nos primeiros oito meses do ano civil 2003 que estão contidos na `Date` dimensão, do cubo **Adventure Works** .  
  
```  
WITH MEMBER [Date].[Calendar].[First8Months2003] AS  
    Aggregate(  
        PeriodsToDate(  
            [Date].[Calendar].[Calendar Year],   
            [Date].[Calendar].[Month].[August 2003]  
        )  
    )  
SELECT   
    [Date].[Calendar].[First8Months2003] ON COLUMNS,  
    [Product].[Category].Children ON ROWS  
FROM  
    [Adventure Works]  
WHERE  
    [Measures].[Order Quantity]  
```  
  
 Para entender o **não visual,** o exemplo a seguir é uma consulta de [Adventure Works] para obter as figuras [valor de vendas do revendedor] em uma tabela em que as categorias de produto são as colunas e os tipos de negócios revendedor são as linhas. Observe que os totais são atribuídos para produtos e revendedores.  
  
 A seguinte instrução SELECT:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from [Adventure Works]`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Gera os seguintes resultados:  
  
|Tipo de negócio + categoria|Todos os Produtos|Acessórios|Bikes|Clothing|Componentes|  
|-|-|-|-|-|-|  
|**Todos os Revendedores**|**$80,450,596.98**|**$571,297.93**|**$66,302,381.56**|**$1,777,840.84**|**$11,799,076.66**|  
|**Specialty Bike Shop**|**$6,756,166.18**|**$65,125.48**|**$6,080,117.73**|**$252,933.91**|**$357,989.07**|  
|**Revendedor de Valor Agregado**|**$34,967,517.33**|**$175,002.81**|**$30,892,354.33**|**$592,385.71**|**$3,307,774.48**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$29,329,909.50**|**$932,521.23**|**$8,133,313.11**|  
  
 Para produzir uma tabela com dados somente para os produtos Acessórios e Roupas, os revendedores Value Added Reseller e Warehouse, embora mantenham os totais gerias, poderiam ser escritos da seguinte forma com o uso de NON VISUAL:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0,`  
  
 `{[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 1`  
  
 `from [Adventure Works])`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Gera os seguintes resultados:  
  
|Tipo de negócio + categoria|Todos os Produtos|Acessórios|Clothing|  
|-|-|-|-|  
|**Todos os Revendedores**|**$80,450,596.98**|**$571,297.93**|**$1,777,840.84**|  
|**Revendedor de Valor Agregado**|**$34,967,517.33**|**$175,002.81**|**$592,385.71**|  
|**Warehouse**|**$38,726,913.48**|**$331,169.64**|**$932,521.23**|  
  
 Para criar uma tabela que totalize visualmente as colunas, mas nos totais de linhas exiba o total verdadeiro de todos os itens em [Category], a seguinte consulta deve ser emitida:  
  
 `select [Category].members on 0,`  
  
 `[Business Type].members on 1`  
  
 `from NON VISUAL (Select {[Category].Accessories, [Category].Clothing} on 0`  
  
 `from ( Select {[Business Type].[Value Added Reseller], [Business Type].[Warehouse]} on 0`  
  
 `from [Adventure Works])`  
  
 `)`  
  
 `where [Measures].[Reseller Sales Amount]`  
  
 Observe como NON VISUAL é aplicado somente a [Category].  
  
 A consulta anterior gera os seguintes resultados:  
  
|Tipo de negócio + categoria|Todos os Produtos|Acessórios|Clothing|  
|-|-|-|-|  
|Todos os Revendedores|$73,694,430.80|$506,172.45|$1,524,906.93|  
|Revendedor de Valor Agregado|$34,967,517.33|$175,002.81|$592,385.71|  
|Warehouse|$38,726,913.48|$331,169.64|$932,521.23|  
  
 Quando comparados aos resultados anteriores, você poderá observar que a linha [Todos os Revendedores] agora soma os valores exibidos para [Revendedor de Valor Agregado] e [Warehouse], mas a coluna [Todos os Produtos] mostra o valor total para todos os produtos, inclusive aqueles não exibidos.  
  
 O exemplo a seguir demonstra como usar membros calculados em subseleções para filtrá-los. Para poder reproduzir esse exemplo, a conexão deve ser estabelecida usando as *subconsultas*do parâmetro da cadeia de conexão = 1.  
  
 `select Measures.allmembers on 0`  
  
 `from (`  
  
 `Select { [Measures].[Reseller Sales Amount]`  
  
 `, [Measures].[Reseller Total Product Cost]`  
  
 `, [Measures].[Reseller Gross Profit]`  
  
 `, [Measures].[Reseller Gross Profit Margin]`  
  
 `} on 0`  
  
 `from [Adventure Works]`  
  
 `)`  
  
 A consulta anterior gera os seguintes resultados:  
  
|Reseller Sales Amount|Custo do produto total do revendedor|Lucro bruto do revendedor|Margem de lucro bruto do revendedor|  
|-|-|-|-|  
|$80,450,596.98|$79980114.38|$470482.60|0,58%|  
  
## <a name="see-also"></a>Consulte Também  
 [Conceitos principais em MDX &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services)   
 [Instruções de manipulação de dados MDX &#40;&#41;MDX ](../mdx/mdx-data-manipulation-statements-mdx.md)   
 [Restringindo a consulta com os eixos de consulta e segmentação &#40;MDX&#41;](~/analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md)  
  
  

