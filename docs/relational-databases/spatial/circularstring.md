---
title: CircularString | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: 9fe06b03-d98c-4337-9f89-54da98f49f9f
author: MladjoA
ms.author: mlandzic
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7c08dd6c0e04c3c323af592ca015b5e1604a05e4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751145"
---
# <a name="circularstring"></a>CircularString
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Um **CircularString** é uma coleção de zero ou mais segmentos de arco circulares contínuos. Um segmento de arco circular é um segmento curvado definido por três pontos em um plano bidimensional; o primeiro ponto não pode ser igual ao terceiro ponto. Se todos os três pontos de um segmento de arco circular forem colineares, o segmento de arco será tratado como um segmento de linha.  
  
> [!IMPORTANT]  
> Para obter uma descrição detalhada e exemplos dos novos recursos espaciais introduzidos no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], incluindo o subtipo **CircularString** , baixe o white paper [New Spatial Features in SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=226407)(Novos recursos espaciais no SQL Server 2012).  
  
## <a name="circularstring-instances"></a>Instâncias CircularString  
 O desenho seguinte mostra instâncias **CircularString** válidas:  
  
 ![5ff17e34-b578-4873-9d33-79500940d0bc](../../relational-databases/spatial/media/5ff17e34-b578-4873-9d33-79500940d0bc.gif)
  
### <a name="accepted-instances"></a>Instâncias aceitas  
 Uma instância **CircularString** será aceita se estiver vazia ou contiver um número ímpar de pontos, n, em que n > 1. As instâncias **CircularString** a seguir são aceitas.  
  
```sql  
DECLARE @g1 geometry = 'CIRCULARSTRING EMPTY';  
DECLARE @g2 geometry = 'CIRCULARSTRING(1 1, 2 0, -1 1)';  
DECLARE @g3 geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 2 0, 1 1)';  
```  
  
 `@g3` mostra que a instância **CircularString** pode ser aceita, mas não é válida. A declaração da instância CircularString a seguir não é aceita. Esta declaração lança uma `System.FormatException`.  
  
```sql  
DECLARE @g geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 1 1)';  
```  
  
### <a name="valid-instances"></a>Instâncias válidas  
 Uma instância **CircularString** válida deve estar vazia ou ter os seguintes atributos:  
  
-   Deve conter, pelo menos, um segmento de arco circular (ou seja, que tenha um mínimo de três pontos).  
-   O último ponto de extremidade para cada segmento de arco circular na sequência, com exceção do último segmento, deve ser o primeiro ponto de extremidade para o próximo segmento na sequência.  
-   Deve ter um número ímpar de pontos.  
-   Não pode se sobrepor a um intervalo.  
-   Embora instâncias **CircularString** possam conter segmentos de linha, esses segmentos devem ser definidos por três pontos colineares.  
  
O exemplo a seguir mostra instâncias **CircularString** válidas.  
  
```sql  
DECLARE @g1 geometry = 'CIRCULARSTRING EMPTY';  
DECLARE @g2 geometry = 'CIRCULARSTRING(1 1, 2 0, -1 1)';  
DECLARE @g3 geometry = 'CIRCULARSTRING(1 1, 2 0, 2 0, 1 1, 0 1)';  
DECLARE @g4 geometry = 'CIRCULARSTRING(1 1, 2 2, 2 2)';  
SELECT @g1.STIsValid(), @g2.STIsValid(), @g3.STIsValid(),@g4.STIsValid();  
```  
  
Uma instância **CircularString** deve conter, pelo menos, dois segmentos de arco circulares para definir um círculo completo. Uma instância **CircularString** não pode usar um único segmento de arco circular (como [1 1, 3 1, 1 1]) para definir um círculo completo. Use (1 1, 2 2, 3 1, 2 0, 1 1) para definir o círculo.  
  
O exemplo a seguir mostra instâncias CircularString que não são válidas.  
  
```sql  
DECLARE @g1 geometry = 'CIRCULARSTRING(1 1, 2 0, 1 1)';  
DECLARE @g2 geometry = 'CIRCULARSTRING(0 0, 0 0, 0 0)';  
SELECT @g1.STIsValid(), @g2.STIsValid();  
```  
  
### <a name="instances-with-collinear-points"></a>Instâncias com pontos colineares  
Nos casos a seguir, um segmento de arco circular será tratado como um segmento de linha:  
  
-   Quando todos os três pontos são colineares (por exemplo, (1 3, 4 4, 7 5)).  
-   Quando o primeiro ponto e o ponto mediano são os mesmos, mas o terceiro ponto é diferente (por exemplo, (1 3, 1 3, 7 5)).  
-   Quando o primeiro e o último pontos são os mesmos, mas o primeiro ponto é diferente (por exemplo, (1 3, 4 4, 4 4)).  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-instantiating-a-geometry-instance-with-an-empty-circularstring"></a>a. Criando uma instância de geometry com uma CircularString vazia  
 Esse exemplo mostra como criar uma instância **CircularString** vazia:  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CIRCULARSTRING EMPTY');  
```  
  
### <a name="b-instantiating-a-geometry-instance-using-a-circularstring-with-one-circular-arc-segment"></a>B. Criando uma instância de geometry usando uma CircularString com um segmento de arco circular  
 O seguinte exemplo mostra como criar uma instância **CircularString** com um único segmento de arco circular (meio-círculo):  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry:: STGeomFromText('CIRCULARSTRING(2 0, 1 1, 0 0)', 0);  
SELECT @g.ToString();  
```  
  
### <a name="c-instantiating-a-geometry-instance-using-a-circularstring-with-multiple-circular-arc-segments"></a>C. Criando uma instância de geometry usando uma CircularString com vários segmentos de arco circular  
 O seguinte exemplo mostra como criar uma instância **CircularString** com mais de um segmento de arco circular (círculo cheio):  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::Parse('CIRCULARSTRING(2 1, 1 2, 0 1, 1 0, 2 1)');  
SELECT 'Circumference = ' + CAST(@g.STLength() AS NVARCHAR(10));    
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```  
Circumference = 6.28319  
```  
  
Compare a saída quando **LineString** é usada em vez de **CircularString**:  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(2 1, 1 2, 0 1, 1 0, 2 1)', 0);  
SELECT 'Perimeter = ' + CAST(@g.STLength() AS NVARCHAR(10));  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```  
Perimeter = 5.65685  
```  
  
Observe que o valor do exemplo de **CircularString** está perto de 2∏, que é a circunferência real do círculo.  
  
### <a name="d-declaring-and-instantiating-a-geometry-instance-with-a-circularstring-in-the-same-statement"></a>D. Declarando e criando uma instância de geometry com uma CircularString na mesma instrução  
 Este snippet mostra como declarar e criar uma instância de **geometry** com uma **CircularString** na mesma instrução:  
  
```sql  
DECLARE @g geometry = 'CIRCULARSTRING(0 0, 1 2.1082, 3 6.3246, 0 7, -3 6.3246, -1 2.1082, 0 0)';  
```  
  
### <a name="e-instantiating-a-geography-instance-with-a-circularstring"></a>E. Criando uma instância de geography com uma CircularString  
 O exemplo a seguir mostra como declarar e criar uma instância de **geography** com uma **CircularString**:  
  
```sql  
DECLARE @g geography = 'CIRCULARSTRING(-122.358 47.653, -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653)';  
```  
  
### <a name="f-instantiating-a-geometry-instance-with-a-circularstring-that-is-a-straight-line"></a>F. Criando uma instância de geometry com uma CircularString que é uma linha reta  
 O exemplo a seguir mostra como criar uma instância **CircularString** que é uma linha reta:  
  
```sql  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('CIRCULARSTRING(0 0, 1 2, 2 4)', 0);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral de tipos de dados espaciais](../../relational-databases/spatial/spatial-data-types-overview.md)   
 [CompoundCurve](../../relational-databases/spatial/compoundcurve.md)   
 [MakeValid &#40;tipos de dados geography&#41;](../../t-sql/spatial-geography/makevalid-geography-data-type.md)   
 [MakeValid &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/makevalid-geometry-data-type.md)   
 [STIsValid &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stisvalid-geometry-data-type.md)   
 [STIsValid &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/stisvalid-geography-data-type.md)   
 [STLength &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stlength-geometry-data-type.md)   
 [STStartPoint &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/ststartpoint-geometry-data-type.md)   
 [STEndpoint &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stendpoint-geometry-data-type.md)   
 [STPointN &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stpointn-geometry-data-type.md)   
 [STNumPoints &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stnumpoints-geometry-data-type.md)   
 [STIsRing &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stisring-geometry-data-type.md)   
 [STIsClosed &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stisclosed-geometry-data-type.md)   
 [STPointOnSurface &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stpointonsurface-geometry-data-type.md)   
 [LineString](../../relational-databases/spatial/linestring.md)  
  
  
