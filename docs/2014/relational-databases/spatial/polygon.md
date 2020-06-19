---
title: Polígono | Microsoft Docs
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- geometry subtypes [SQL Server]
- Polygon geometry subtype [SQL Server]
ms.assetid: b6a21c3c-fdb8-4187-8229-1c488454fdfb
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 040bb8a2558cc57b1b99a3ce984bec3c8925bc0d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062992"
---
# <a name="polygon"></a>Polygon
  Um `Polygon` é uma superfície bidimensional armazenada como uma sequência de pontos que define um anel delimitador exterior e zero ou mais anéis interiores.

## <a name="polygon-instances"></a>Instâncias de polígono
 Uma instância `Polygon` pode ser formada de um anel que tem pelo menos três pontos distintos. Uma instância `Polygon` também pode estar vazia.

 Os anéis exteriores e todos os anéis interiores de um `Polygon` definem seu limite. O espaço dentro dos anéis define o interior do `Polygon`.

 A ilustração a seguir mostra exemplos de instâncias `Polygon`.

 ![Exemplos das instâncias geométricas Polygon](../../database-engine/media/polygon.gif "Exemplos das instâncias geométricas Polygon")

 Conforme mostrado na ilustração:

1.  A Figura 1 é uma instância `Polygon` cujo limite está definido por um anel exterior.

2.  A Figura 2 é uma instância `Polygon` cujo limite está definido por um anel exterior e dois anéis interiores. A área dentro dos anéis interiores faz parte do exterior da instância `Polygon`.

3.  A Figura 3 é uma instância `Polygon` válida porque seus anéis interiores cruzam em um único ponto tangente.

### <a name="accepted-instances"></a>Instâncias aceitas
 Instâncias `Polygon` aceitas são instâncias que podem ser armazenadas em uma variável `geometry` ou `geography` sem lançar uma exceção. As seguintes instâncias `Polygon` são aceitas:

-   Uma instância `Polygon` vazia

-   Uma instância `Polygon` que tem um anel exterior aceitável e zero ou mais anéis interiores aceitáveis

 Os critérios a seguir são necessários para que um anel seja aceitável.

-   A instância `LineString` deve ser aceita.

-   A instância `LineString` deve ter pelo menos quatro pontos.

-   Os pontos inicial e final da instância `LineString` devem ser iguais.

 O exemplo a seguir mostra instâncias `Polygon` aceitas.

```
DECLARE @g1 geometry = 'POLYGON EMPTY';
DECLARE @g2 geometry = 'POLYGON((1 1, 3 3, 3 1, 1 1))';
DECLARE @g3 geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(0 0, 3 0, 3 3, 0 3, 0 0))';
DECLARE @g4 geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(3 0, 6 0, 6 3, 3 3, 3 0))';
DECLARE @g5 geometry = 'POLYGON((1 1, 1 1, 1 1, 1 1))';
```

 Conforme mostrado por `@g4` e `@g5` uma instância aceita de `Polygon` talvez não seja uma instância válida de `Polygon`. `@g5` também mostra que uma instância do Polygon precisa conter apenas um anel com quatro pontos para ser aceita.

 Os exemplos a seguir lançam uma `System.FormatException` porque as instâncias `Polygon` não são aceitas.

```
DECLARE @g1 geometry = 'POLYGON((1 1, 3 3, 1 1))';
DECLARE @g2 geometry = 'POLYGON((1 1, 3 3, 3 1, 1 5))';
```

 `@g1` não é aceito porque a instância de `LineString` para o anel exterior não contém pontos suficientes. `@g2` não é aceito porque o ponto de início da instância `LineString` do anel exterior não é igual ao ponto de término. O exemplo a seguir tem um anel exterior aceitável, mas o anel interior não é aceitável. Isso também lança uma `System.FormatException`.

```
DECLARE @g geometry = 'POLYGON((-5 -5, -5 5, 5 5, 5 -5, -5 -5),(0 0, 3 0, 0 0))';
```

### <a name="valid-instances"></a>Instâncias válidas
 Os anéis interiores de um `Polygon` podem tocar em si mesmos e um no outro em pontos tangentes únicos, mas se os anéis interiores de um `Polygon` se cruzarem, a instância não será válida.

 O exemplo a seguir mostra instâncias `Polygon` válidas.

```
DECLARE @g1 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20))';
DECLARE @g2 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0))';
DECLARE @g3 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 0 10, -5 -10, -10 0))';
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();
```

 `@g3` é válido porque os dois anéis interiores se tocam em um único ponto e não se cruzam. O exemplo a seguir mostra instâncias `Polygon` que não são válidas.

```
DECLARE @g1 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (20 0, 0 10, 0 -20, 20 0))';
DECLARE @g2 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (5 0, 1 5, 1 -5, 5 0))';
DECLARE @g3 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 0 10, 0 -10, -10 0))';
DECLARE @g4 geometry = 'POLYGON((-20 -20, -20 20, 20 20, 20 -20, -20 -20), (10 0, 0 10, 0 -10, 10 0), (-10 0, 1 5, 0 -10, -10 0))';
DECLARE @g5 geometry = 'POLYGON((10 0, 0 10, 0 -10, 10 0), (-20 -20, -20 20, 20 20, 20 -20, -20 -20) )';
DECLARE @g6 geometry = 'POLYGON((1 1, 1 1, 1 1, 1 1))';
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(), @g4.STIsValid(), @g5.STIsValid(), @g6.STIsValid();
```

 `@g1` não é válido porque o anel interno toca o anel exterior em dois locais. `@g2` não é válido porque o segundo anel interno está no interior do primeiro anel interno. `@g3` não é válido porque os dois anéis internos tocam-se em vários pontos sucessivos. `@g4` não é válido porque os interiores dos dois anéis internos estão sobrepostos. `@g5` não é válido porque o anel exterior não é o primeiro anel. `@g6` não é válido porque o anel não tem três pontos distintos pelo menos.

## <a name="examples"></a>Exemplos
 O exemplo a seguir cria uma instância de `geometry``Polygon` simples com um espaço e SRID 10.

```
DECLARE @g geometry;
SET @g = geometry::STPolyFromText('POLYGON((0 0, 0 3, 3 3, 3 0, 0 0), (1 1, 1 2, 2 1, 1 1))', 10);
```

 Uma instância que não é válida pode ser inserida e convertida em uma instância `geometry` válida. No exemplo seguinte de um `Polygon`, os anéis interiores e exteriores se sobrepõem e a instância não é válida.

```
DECLARE @g geometry;
SET @g = geometry::Parse('POLYGON((1 0, 0 1, 1 2, 2 1, 1 0), (2 0, 1 1, 2 2, 3 1, 2 0))');
```

 No exemplo a seguir, a instância inválida é tornada válida com `MakeValid()`.

```
SET @g = @g.MakeValid();
SELECT @g.ToString();
```

 A instância de `geometry` retornada do exemplo acima é um `MultiPolygon`.

```
MULTIPOLYGON (((2 0, 3 1, 2 2, 1.5 1.5, 2 1, 1.5 0.5, 2 0)), ((1 0, 1.5 0.5, 1 1, 1.5 1.5, 1 2, 0 1, 1 0)))
```

 Este é outro exemplo de conversão de uma instância inválida em uma instância de geometry válida. No exemplo a seguir, a instância `Polygon` foi criada usando três pontos que são exatamente iguais:

```sql
DECLARE @g geometry
SET @g = geometry::Parse('POLYGON((1 3, 1 3, 1 3, 1 3))');
SET @g = @g.MakeValid();
SELECT @g.ToString()
```

 A instância de geometry retornada acima é um `Point(1 3)`.  Se o `Polygon` fornecido for `POLYGON((1 3, 1 5, 1 3, 1 3))` , `MakeValid()` retornaria `LINESTRING(1 3, 1 5)`.

## <a name="see-also"></a>Consulte Também
 [A área de &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/starea-geometry-data-type) [STExteriorRing &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stexteriorring-geometry-data-type) [STNumInteriorRing &#40;tipo de dados geometry&#41;](/sql/t-sql/spatial-geometry/stnuminteriorring-geometry-data-type) [STInteriorRingN &#40;](/sql/t-sql/spatial-geometry/stinteriorringn-geometry-data-type) tipo de dados geometry&#41;o &#40;[do tipo de](/sql/t-sql/spatial-geometry/stcentroid-geometry-data-type) dados geometry&#41;o tipo de dados geometry &#40;[STPointOnSurface](/sql/t-sql/spatial-geometry/stpointonsurface-geometry-data-type)&#41;[o tipo de](/sql/t-sql/spatial-geometry/stisvalid-geometry-data-type) dados [espaciaI](../spatial/spatial-data-sql-server.md) &#40;[MultiPolygon](../spatial/polygon.md) SQL Server o tipo de [dados geography](/sql/t-sql/spatial-geography/stisvalid-geography-data-type)&#41;


