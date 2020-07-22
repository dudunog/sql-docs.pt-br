---
title: CompoundCurve | Microsoft Docs
ms.date: 07/16/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: ae357f9b-e3e2-4cdf-af02-012acda2e466
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1ada315623e41e188a93eb7bef8df2295e437429
ms.sourcegitcommit: 56f6892b3795da308d226d4b3c5c859ead2e830a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86438188"
---
# <a name="compoundcurve"></a>CompoundCurve
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Uma **CompoundCurve** é uma coleção de zero ou mais instâncias **CircularString** ou **LineString** contínuas dos tipos geometry ou geography.  
  
Pode ser criada uma instância **CompoundCurve** vazia, mas para que **CompoundCurve** seja válida, ela deverá atender aos seguintes critérios:  
  
1.  Deve conter, pelo menos, uma instância **CircularString** ou **LineString** .  
  
2.  A sequência das instâncias **CircularString** ou **LineString** deve ser contínua.  

Se uma **CompoundCurve** contiver uma sequência de várias instâncias **CircularString** e **LineString** , o ponto de extremidade final de cada instância, exceto a última, deverá ser o ponto de extremidade inicial da próxima instância na sequência. Isso significa que, se o ponto final de uma instância anterior na sequência for (4 3 7 2), o ponto inicial da próxima instância na sequência deverá ser (4 3 7 2). Observe que os valores Z (elevação) e M (medida) do ponto também devem ser iguais. Se houver uma diferença nos dois pontos, será lançada uma `System.FormatException` . Pontos em uma **CircularString** não precisam ter um valor Z ou M. Se não forem fornecidos valores Z ou M para o ponto final da instância anterior, o ponto inicial da próxima instância não poderá incluir valores Z ou M. Se o ponto final da sequência anterior for (4 3), o ponto inicial da próxima sequência deverá ser (4 3); ele não poderá ser (4 3 7 2). Todos os pontos em uma instância **CompoundCurve** não devem ter nenhum valor Z ou devem ter o mesmo valor Z.  
  
## <a name="compoundcurve-instances"></a>Instâncias CompoundCurve  
A ilustração a seguir mostra tipos **CompoundCurve** válidos.  
  
![f278742e-b861-4555-8b51-3d972b7602bf](../../relational-databases/spatial/media/f278742e-b861-4555-8b51-3d972b7602bf.gif)  
 
### <a name="accepted-instances"></a>Instâncias aceitas  
 A instância**CompoundCurve** será aceita se for uma instância vazia ou se atender aos critérios a seguir.  
  
1.  Todas as instâncias contidas na instância **CompoundCurve** são instâncias de segmento de arco circular aceitas. Para obter mais informações sobre instâncias de segmento de arco circular aceitas, veja [LineString](../../relational-databases/spatial/linestring.md) e [CircularString](../../relational-databases/spatial/circularstring.md).  
  
2.  Todos os segmentos de arco circular na instância **CompoundCurve** estão conectados. O primeiro ponto de cada segmento de arco circular sucessivo é igual ao último ponto no segmento de arco circular anterior.  
  
    > [!NOTE]  
    > Isso inclui as coordenadas Z e M. Assim, as quatro coordenadas X, Y, Z e M devem ser iguais.  
  
3.  Nenhuma das instâncias contidas é uma instância vazia.  
  
O exemplo a seguir mostra instâncias **CompoundCurve** aceitas.  
  
```sql  
DECLARE @g1 geometry = 'COMPOUNDCURVE EMPTY';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (-1 0, 2 0))';  
```  
  
O exemplo a seguir mostra instâncias **CompoundCurve** que não são aceitas. Essas instâncias lançam `System.FormatException`.  
  
```sql  
DECLARE @g1 geometry = 'COMPOUNDCURVE(CIRCULARSTRING EMPTY)';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (1 0, 2 0))';  
```  
  
### <a name="valid-instances"></a>Instâncias válidas  
 Uma instância **CompoundCurve** será válida se atender aos critérios a seguir.  
  
1.  A instância **CompoundCurve** é aceita.  
  
2.  Todas as instâncias de segmento de arco circular contidas na instância **CompoundCurve** são instâncias válidas.  
  
O exemplo a seguir mostra instâncias **CompoundCurve** válidas.  
  
```sql  
DECLARE @g1 geometry = 'COMPOUNDCURVE EMPTY';  
DECLARE @g2 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 0, 0 1, -1 0), (-1 0, 2 0))';  
DECLARE @g3 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 1 1, 1 1), (1 1, 3 5, 5 4))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
`@g3` é válida, pois a instância **CircularString** é válida. Para obter mais informações sobre a validade da instância **CircularString** , veja [CircularString](../../relational-databases/spatial/circularstring.md).  
  
O exemplo a seguir mostra instâncias **CompoundCurve** que não são válidas.  
  
```sql  
DECLARE @g1 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 1 1, 1 1), (1 1, 3 5, 5 4, 3 5))';  
DECLARE @g2 geometry = 'COMPOUNDCURVE((1 1, 1 1))';  
DECLARE @g3 geometry = 'COMPOUNDCURVE(CIRCULARSTRING(1 1, 2 3, 1 1))';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid();  
```  
  
`@g1` não é válido porque a segunda instância não é uma instância de LineString válida. `@g2` não é válido porque a instância **LineString** não é válida. `@g3` não é válida, pois a instância **CircularString** não é válida. Para obter mais informações sobre instâncias **CircularString** e **LineString** válidas, veja [CircularString](../../relational-databases/spatial/circularstring.md) e [LineString](../../relational-databases/spatial/linestring.md).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-instantiating-a-geometry-instance-with-an-empty-compooundcurve"></a>a. Criando uma instância de geometry com uma CompoundCurve vazia  
 O exemplo a seguir mostra como criar uma instância `CompoundCurve` vazia:  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE EMPTY');  
```  
  
### <a name="b-declaring-and-instantiating-a-geometry-instance-using-a-compoundcurve-in-the-same-statement"></a>B. Declarando e criando uma instância de geometry usando uma CompoundCurve na mesma instrução  
 O seguinte exemplo mostra como declarar e inicializar uma instância `geometry` com um `CompoundCurve`na mesma instrução:  
  
```sql  
DECLARE @g geometry = 'COMPOUNDCURVE ((2 2, 0 0),CIRCULARSTRING (0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0))';  
```  
  
### <a name="c-instantiating-a-geography-instance-with-a-compoundcurve"></a>C. Criando uma instância de geography com uma CompoundCurve  
 O seguinte exemplo mostra como declarar e inicializar uma instância **geography** com um `CompoundCurve`:  
  
```sql  
DECLARE @g geography = 'COMPOUNDCURVE(CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))';  
```  
  
### <a name="d-storing-a-square-in-a-compoundcurve-instance"></a>D. Armazenando um quadrado em uma instância CompoundCurve  
 O exemplo seguinte usa uma instância `CompoundCurve` de duas maneiras diferentes para armazenar um quadrado.  
  
```sql  
DECLARE @g1 geometry, @g2 geometry;  
SET @g1 = geometry::Parse('COMPOUNDCURVE((1 1, 1 3), (1 3, 3 3),(3 3, 3 1), (3 1, 1 1))');  
SET @g2 = geometry::Parse('COMPOUNDCURVE((1 1, 1 3, 3 3, 3 1, 1 1))');  
SELECT @g1.STLength(), @g2.STLength();  
```  
  
 Os comprimentos de `@g1` e `@g2` são iguais. Observe que, no exemplo, uma instância **CompoundCurve** pode armazenar uma ou mais instâncias `LineString`.  
  
### <a name="e-instantiating-a-geometry-instance-using-a-compoundcurve-with-multiple-circularstrings"></a>E. Criando uma instância de geometry que usa uma CompoundCurve com várias CircularStrings  
 O exemplo a seguir mostra como usar duas instâncias `CircularString` diferentes para inicializar uma `CompoundCurve`:  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), CIRCULARSTRING(4 2, 2 4, 0 2))');  
SELECT @g.STLength();  
```  
  
Isso produz a saída `12.5663706143592`, que é o equivalente do 4?. A instância `CompoundCurve` do exemplo armazena um círculo com raio 2. Os dois exemplos de código anteriores não precisavam usar uma `CompoundCurve`. Teria sido mais simples usar uma instância `LineString` no primeiro exemplo e uma instância `CircularString` no segundo exemplo. Porém, o próximo exemplo mostra onde uma `CompoundCurve` oferece uma alternativa melhor.  
  
### <a name="f-using-a-compoundcurve-to-store-a-semicircle"></a>F. Usando uma CompoundCurve para armazenar um semicírculo  
 O exemplo a seguir usa uma instância `CompoundCurve` para armazenar um semicírculo.  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 0 2))');  
SELECT @g.STLength();  
```  
  
### <a name="g-storing-multiple-circularstring-and-linestring-instances-in-a-compoundcurve"></a>G. Armazenando várias instâncias CircularString e LineString em uma CompoundCurve  
 O exemplo a seguir mostra como várias instâncias `CircularString` e `LineString` podem ser armazenadas usando uma `CompoundCurve`.  
  
```sql  
DECLARE @g geometry  
SET @g = geometry::Parse('COMPOUNDCURVE((3 5, 3 3), CIRCULARSTRING(3 3, 5 1, 7 3), (7 3, 7 5), CIRCULARSTRING(7 5, 5 7, 3 5))');  
SELECT @g.STLength();  
```  
  
### <a name="h-storing-instances-with-z-and-m-values"></a>H. Armazenando instâncias com valores Z e M  
 O exemplo a seguir mostra como usar uma instância `CompoundCurve` para armazenar uma sequência de instâncias `CircularString` e `LineString` com valores Z e M.  
  
```sql  
SET @g = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(7 5 4 2, 5 7 4 2, 3 5 4 2), (3 5 4 2, 8 7 4 2))');  
```  
  
### <a name="i-illustrating-why-circularstring-instances-must-be-explicitly-declared"></a>I. Ilustrando por que as instâncias CircularString devem ser declaradas explicitamente  
 O exemplo a seguir mostra por que as instâncias `CircularString` devem ser declaradas explicitamente. O programador está tentando armazenar um círculo em uma instância `CompoundCurve` .  
  
```sql  
DECLARE @g1 geometry;    
DECLARE @g2 geometry;  
SET @g1 = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), (4 2, 2 4, 0 2))');  
SELECT 'Circle One', @g1.STLength() AS Perimeter;  -- gives an inaccurate amount  
SET @g2 = geometry::Parse('COMPOUNDCURVE(CIRCULARSTRING(0 2, 2 0, 4 2), CIRCULARSTRING(4 2, 2 4, 0 2))');  
SELECT 'Circle Two', @g2.STLength() AS Perimeter;  -- now we get an accurate amount  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Circle One11.940039...  
Circle Two12.566370...  
```  
  
O perímetro de Circle Two é aproximadamente 4?, que é o valor real do perímetro. Porém, o perímetro de Circle One é significativamente inexato. A instância `CompoundCurve` de Circle One armazena um segmento de arco circular (ABC) e dois segmentos de linha (CD, DA). A instância `CompoundCurve` deve armazenar dois segmentos de arco circular (ABC, CDA) para definir um círculo. Uma instância `LineString` define o segundo conjunto de pontos (4 2, 2 4, 0 2) na instância `CompoundCurve` de Circle One. Você deve declarar uma instância `CircularString` explicitamente dentro de uma `CompoundCurve`.  
  
## <a name="see-also"></a>Consulte Também  
 [STIsValid &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [STLength &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STStartPoint &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/ststartpoint-geometry-data-type.md)   
 [STEndpoint &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stendpoint-geometry-data-type.md)   
 [LineString](../../relational-databases/spatial/linestring.md)   
 [CircularString](../../relational-databases/spatial/circularstring.md)   
 [Visão geral de tipos de dados espaciais](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [Ponto](../../relational-databases/spatial/point.md)  
  
