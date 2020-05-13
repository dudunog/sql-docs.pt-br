---
title: Visão geral de tipos de dados espaciais | Microsoft Docs
ms.date: 05/04/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geometry data type [SQL Server], understanding
- geography data type [SQL Server], spatial data
- planar spatial data [SQL Server], geometry data type
- spatial data types [SQL Server]
ms.assetid: 1615db50-69de-4778-8be6-4e058c00ccd4
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9fb9acb0aa03184f038c2dda9be10b36e6ca32ee
ms.sourcegitcommit: f6200d3d9cdf2627b243384835dc37d2bd40480e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82784671"
---
# <a name="spatial-data-types-overview"></a>Visão geral de tipos de dados espaciais
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  
Há dois tipos de dados espaciais. O tipo de dados **geometry** dá suporte a dados planares ou a dados euclidianos (planisfério). O tipo de dados **geometry** está de acordo com os Recursos Simples do Open Geospatial Consortium (OGC) para o SQL Specification versão 1.1.0 e compatível com o SQL MM (padrão ISO).
Além disso, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte ao tipo de dados **geometry** que armazena dados elipsoidais (globo), como coordenadas de latitude e longitude de GPS.

##  <a name="spatial-data-objects"></a><a name="objects"></a> Objetos de dados espaciais  
Os tipos de dados **geometry** e **geography** oferecem suporte a dezesseis objetos de dados espaciais, ou tipos de instâncias. No entanto, apenas onze desses tipos de instâncias *podem ser instanciados*. É possível criar e trabalhar com essas instâncias (ou criar uma instância delas) em um banco de dados. Essas instâncias derivam determinadas propriedades de seus tipos de dados pai que as distingue como **Points**, **LineStrings, CircularStrings**, **CompoundCurves**, **Polygons**, **CurvePolygons** ou como instâncias **geometry** ou **geography** múltiplas em uma **GeometryCollection**. O tipo**Geography** tem um tipo de instância adicional, **FullGlobe**.  

A figura a seguir ilustra a hierarquia **geometry** na qual os tipos de dados **geometry** e **geography** se baseiam. Os tipos a partir dos quais se podem criar instâncias de **geometry** e **geography** são indicados em azul.  

![geom_hierarchy](../../relational-databases/spatial/media/geom-hierarchy.gif) 

Como a figura indica, os dez tipos dos quais se pode criar uma instância dos tipos de dados **geometry** e **geography** são **Point**, **MultiPoint**, **LineString**, **CircularString**, **MultiLineString**, **CompoundCurve**, **Polygon**, **CurvePolygon**, **MultiPolygon**e **GeometryCollection**. Há um tipo adicional do qual se pode criar uma instância para o tipo de dados de geography: **FullGlobe**. Os tipos **geometry** e **geography** podem reconhecer uma instância específica desde que ela esteja bem-formada, ainda que não esteja definida explicitamente. Por exemplo, se você definir uma instância de **Point** explicitamente usando o método STPointFromText(), **geometry** e **geography** a reconhecerão como uma instância de **Point**, desde que a entrada do método esteja bem formada. Se você definir a mesma instância usando o método `STGeomFromText()` , os tipos de dados **geometry** e **geography** reconhecem a instância como um **Point**.  

Os subtipos dos tipos geometry e geography são divididos em tipos simples e de coleção.  Alguns métodos como `STNumCurves()` só funcionam com tipos simples.  

Os tipos simples incluem:  
-   [Ponto](../../relational-databases/spatial/point.md)  
-   [LineString](../../relational-databases/spatial/linestring.md)  
-   [CircularString](../../relational-databases/spatial/circularstring.md)  
-   [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)  
-   [Polygon](../../relational-databases/spatial/polygon.md)  
-   [CurvePolygon](../../relational-databases/spatial/curvepolygon.md)  

Os tipos de coleção incluem:  
-   [MultiPoint](../../relational-databases/spatial/multipoint.md)  
-   [MultiLineString](../../relational-databases/spatial/multilinestring.md)  
-   [MultiPolygon](../../relational-databases/spatial/multipolygon.md)  
-   [GeometryCollection](../../relational-databases/spatial/geometrycollection.md)  

##  <a name="differences-between-the-geometry-and-geography-data-types"></a><a name="differences"></a> Diferenças entre os tipos de dados de geometria e geografia  
Os dois tipos de dados espaciais sempre se comportam de maneira muito semelhante, mas há algumas diferenças importantes na maneira como eles são armazenados e manipulados.  

### <a name="how-connecting-edges-are-defined"></a>Como bordas de conexão são definidas  
Os dados definidos para os tipos **LineString** e **Polygon** são somente vértices.  A borda de conexão entre dois vértices em um tipo geometry é uma linha reta.  No entanto, a borda de conexão entre dois vértices em um tipo de geografia é um amplo arco elíptico curto entre os dois vértices.  Uma grande elipse é a interseção do elipsoide com um plano no centro, e um amplo arco elíptico é um segmento de arco na grande elipse.  

### <a name="how-circular-arc-segments-are-defined"></a>Como são definidos segmentos de arco circular  
Os segmentos de arco circular para tipos geometry são definidos no plano de coordenadas cartesianas XY (são ignorados valores Z). Os segmentos de arco circular para tipos geography são definidos por segmentos de curva em uma esfera de referência. Qualquer paralelo na esfera de referência pode ser definido por dois arcos circulares complementares, onde os pontos para ambos os arcos têm um ângulo de latitude constante.  

### <a name="measurements-in-spatial-data-types"></a>Medidas em tipos de dados espaciais  
No sistema planar ou de terra plana, as medidas de distâncias e de áreas são fornecidas na mesma unidade de medida das coordenadas. Usando o tipo de dados **geometry** , a distância entre (2, 2) e (5, 6) é de 5 unidades, independentemente das unidades usadas.  

No sistema elipsoidal ou de terra redonda, as coordenadas são fornecidas em graus de latitude ou de longitude. No entanto os comprimentos e áreas são normalmente medidos em metros e metros quadrados, embora a medida possa depender do SRID (identificador de referência espacial) da instância de **geography** . A unidade de medida mais comum para o tipo de dados **geography** é em metros.  

### <a name="orientation-of-spatial-data"></a>Orientação de dados espaciais  
No sistema de planar, a orientação de anel de um polígono não é um fator importante. Por exemplo, um polígono descrito por ((0, 0), (10, 0), (0, 20), (0, 0)) é o mesmo que um polígono descrito por ((0, 0), (0, 20), (10, 0), (0, 0)). Os Recursos Simples do OGC para SQL Specification não ditam uma ordenação de anel e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não impõe ordenação de anel.  

Em um sistema elipsoidal, um polígono não tem nenhum significado ou é ambíguo, sem uma orientação. Por exemplo, um anel ao redor do equador descreve o hemisfério norte ou o sul? Se usarmos o tipo de dados **geography** para armazenar a instância espacial, deveremos especificar a orientação do anel e descrever precisamente o local da instância. O interior do polígono em um sistema elipsoidal é definido pela "regra à esquerda": se você imaginar que está caminhando ao longo do anel de um polígono de Geografia, seguindo os pontos na ordem em que são listados, a área à esquerda será tratada como o interior do polígono e a área à direita, como o exterior do polígono.

Quando o nível de compatibilidade é 100 ou abaixo no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , o tipo de dados **geography** tem as seguintes restrições:  
-   Cada instância de **geography** deve se ajustar dentro de um único hemisfério. Nenhum objeto espacial maior do que um hemisfério pode ser armazenado.  
-   Qualquer instância de **geography** de uma representação WKT (Well-Known Text) ou WKB (Well-Known Binary) do Open Geospatial Consortium (OGC) que reproduza um objeto maior do que um hemisfério aciona uma **ArgumentException**.  
-   Os métodos de tipo de dados **geography** que requerem a entrada de duas instâncias de **geography** , como STIntersection(), STUnion(), STDifference() e STSymDifference(), retornarão nulo se os resultados dos métodos não se ajustarem dentro de um único hemisfério. STBuffer() também retornará nulo se a saída ultrapassar um único hemisfério.  

No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], **FullGlobe** é um tipo especial de polígono que abrange o globo inteiro. **FullGlobe** tem uma área, mas nenhuma borda ou vértices.  

### <a name="outer-and-inner-rings-not-important-in-geography-data-type"></a>Anéis externos e internos não são importantes no tipo de dados `geography`  
A Especificação Recursos Simples do OGC para SQL aborda anéis externos e internos, mas essa distinção faz pouco sentido para o tipo de dados **geography** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: qualquer anel de um polígono pode ser usado como o anel externo.  

Para obter mais informações sobre especificações do OCG, consulte o seguinte:  
-   [OGC Specifications, Simple Feature Access Part 1 - Common Architecture](https://go.microsoft.com/fwlink/?LinkId=93627)  
-   [Especificações do OGC, Simple Feature Access Part 2 – SQL Options](https://go.microsoft.com/fwlink/?LinkId=93628) (Acesso de recurso simples Parte 2 – opções de SQL)  

##  <a name="circular-arc-segments"></a><a name="circular"></a> Segmentos de arco circular  
Três tipos instanciáveis podem adotar segmentos de arco circular: **CircularString**, **CompoundCurve** e **CurvePolygon**.  Um segmento de arco circular é definido por três pontos em um plano bidimensional, e o terceiro ponto não pode ser igual ao primeiro.  

As figuras A e B mostram segmentos de arco circular típicos. Observe como cada um dos três pontos se situa no perímetro de um círculo.  

As figuras C e D mostram como um segmento de linha pode ser definido como um segmento de arco circular.  Observe que três pontos ainda são necessários para definir o segmento de arco circular, ao contrário de um segmento de linha normal, que pode ser definido por apenas dois pontos.  
Os métodos que operam em tipos de segmento de arco circular usam segmentos de linha reta para aproximar o arco circular. O número de segmentos de linha usado para aproximar o arco dependerá do comprimento e da curvatura do arco. Podem ser armazenados valores Z para cada um dos tipos de segmento de arco circular; porém, os métodos não usarão os valores Z em seus cálculos.  

> [!NOTE]  
> Se forem fornecidos valores Z para segmentos de arco circular, eles deverão ser iguais para todos os pontos no segmento de arco circular para que o segmento seja aceito para entrada. Por exemplo, `CIRCULARSTRING(0 0 1, 2 2 1, 4 0 1)` é aceito, mas `CIRCULARSTRING(0 0 1, 2 2 2, 4 0 1)` não é.  

### <a name="linestring-and-circularstring-comparison"></a>Comparação de LineString e CircularString  
Este exemplo mostra como armazenar triângulos isósceles idênticos que usam uma instância **LineString** e uma instância **CircularString**:  

```sql
DECLARE @g1 geometry;
DECLARE @g2 geometry;
SET @g1 = geometry::STGeomFromText('LINESTRING(1 1, 5 1, 3 5, 1 1)', 0);
SET @g2 = geometry::STGeomFromText('CIRCULARSTRING(1 1, 3 1, 5 1, 4 3, 3 5, 2 3, 1 1)', 0);
IF @g1.STIsValid() = 1 AND @g2.STIsValid() = 1
  BEGIN
      SELECT @g1.ToString(), @g2.ToString()
      SELECT @g1.STLength() AS [LS Length], @g2.STLength() AS [CS Length]
  END
```  

Note que uma instância **CircularString** requer sete pontos para definir o triângulo, mas uma instância **LineString** requer somente quatro pontos para definir o triângulo. O motivo para isso é que uma instância **CircularString** armazena segmentos de arco circular e não segmentos de linha. Portanto, os lados do triângulo armazenados na instância **CircularString** são ABC, CDE e EFA, ao passo que os lados do triângulo armazenados na instância **LineString** são AC, CE e EA.  

Considere o exemplo a seguir:  

```sql
SET @g1 = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 4 0)', 0);
SET @g2 = geometry::STGeomFromText('CIRCULARSTRING(0 0, 2 2, 4 0)', 0);
SELECT @g1.STLength() AS [LS Length], @g2.STLength() AS [CS Length];
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```
LS LengthCS Length
5.65685...6.28318...
```

As instâncias **CircularString** usam menos pontos para armazenar limites de curva com maior precisão que as instâncias **LineString**. As instâncias**CircularString** são úteis para armazenar limites circulares como um raio de pesquisa de vinte milhas de um ponto específico. Instâncias**LineString** são boas para armazenar limites que são lineares como um quarteirão de cidade.  

### <a name="linestring-and-compoundcurve-comparison"></a>Comparação de LineString e CompoundCurve  
Os exemplos de código seguintes mostram como armazenar a mesma figura usando instâncias **LineString** e **CompoundCurve** :

```sql
SET @g = geometry::Parse('LINESTRING(2 2, 4 2, 4 4, 2 4, 2 2)');
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2), (4 2, 4 4), (4 4, 2 4), (2 4, 2 2))');
SET @g = geometry::Parse('COMPOUNDCURVE((2 2, 4 2, 4 4, 2 4, 2 2))');
```

Nos exemplos anteriores, uma instância **LineString** ou uma instância **CompoundCurve** poderiam armazenar a figura.  Este próximo exemplo usa uma **CompoundCurve** para armazenar uma fatia de pizza:  

```sql
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(2 2, 1 3, 0 2),(0 2, 1 0, 2 2))');  
```  

Uma instância **CompoundCurve** pode armazenar o segmento de arco circular (2 2, 1 3, 0 2) diretamente, ao passo que uma instância **LineString** teria que converter a curva em vários segmentos de linha menores.  

### <a name="circularstring-and-compoundcurve-comparison"></a>Comparação de CircularString e CompoundCurve  
O exemplo de código a seguir mostra como a fatia de pizza pode ser armazenada em uma instância **CircularString** :  

```sql
DECLARE @g geometry;
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)');
SELECT @g.ToString(), @g.STLength();
```

Para armazenar a fatia de pizza usando uma instância **CircularString** , é necessário que três pontos sejam usados para cada segmento de linha.  Se um ponto intermediário não for conhecido, ele deverá ser calculado ou o ponto de extremidade do segmento de linha deverá ser dobrado como mostra o seguinte snippet:  

```sql
SET @g = geometry::Parse('CIRCULARSTRING( 0 0, 3 6.3246, 3 6.3246, 0 7, -3 6.3246, 0 0, 0 0)');
```

As instâncias**CompoundCurve** permitem componentes **LineString** e **CircularString** , de forma que somente dois pontos para os segmentos de linha da fatia de pizza precisam ser conhecidos.  Este exemplo de código mostra como usar uma **CompoundCurve** para armazenar a mesma figura:  
```sql
DECLARE @g geometry;
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING( 3 6.3246, 0 7, -3 6.3246), (-3 6.3246, 0 0, 3 6.3246))');
SELECT @g.ToString(), @g.STLength();
```

### <a name="polygon-and-curvepolygon-comparison"></a>Comparação de Polygon e CurvePolygon  
Instâncias**CurvePolygon** podem usar instâncias **CircularString** e **CompoundCurve** instances when defining their exterior e interior rings.  Instâncias de **Polígono** não podem usar os tipos de segmento de arco circular: **CircularString** e **CompoundCurve**.  

## <a name="see-also"></a>Consulte Também  
- [Dados espaciais (SQL Server)](https://msdn.microsoft.com/library/bb933790.aspx) 
- [Referência de método de tipo de dados geometry](https://msdn.microsoft.com/library/bb933973.aspx) 
- [Referência de método de tipo de dados geography](https://msdn.microsoft.com/library/028e6137-7128-4c74-90a7-f7bdd2d79f5e)   
- [STNumCurves &#40;Tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stnumcurves-geometry-data-type.md)   
- [STNumCurves &#40;Tipo de dados geography&#41;](../../t-sql/spatial-geography/stnumcurves-geography-data-type.md)   
- [STGeomFromText &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stgeomfromtext-geometry-data-type.md)   
- [STGeomFromText &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/stgeomfromtext-geography-data-type.md)  
