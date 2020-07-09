---
title: STCrosses (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STCrosses (geometry Data Type)
- STCrosses_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STCrosses (geometry Data Type)
ms.assetid: 3e3fc065-555a-4bee-8b71-e92f3dc62a4f
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: b78da062fb43d04afb53b8e4743ad222d873fe32
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85748713"
---
# <a name="stcrosses-geometry-data-type"></a>STCrosses (tipo de dados geometry)
[!INCLUDE [SQL Server Azure SQL Database ](../../includes/applies-to-version/sql-asdb.md)]

Retorna 1 se uma instância de **geometry** cruza outra instância de **geometry**. Retornará 0 se isso não ocorrer.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STCrosses ( other_geometry )  
```  
  
## <a name="arguments"></a>Argumentos  
 *other_geometry*  
 É outra instância de **geometry** a ser comparada com a instância na qual `STCrosses()` é invocado.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
 Tipo de retorno do CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentários  
 Duas instâncias de **geometry** se cruzarão se as seguintes condições forem verdadeiras:  
  
-   A interseção de duas instâncias de **geometry** resulta em uma geometria cujas dimensões são menores que a dimensão máxima das instâncias de **geometry** de origem.  
  
-   O conjunto de interseções é interior a ambas as instâncias de **geometry** de origem.  
  
 Esse método sempre retornará nulo se as SRIDs (IDs de referência espacial) das instâncias de **geometry** não forem correspondentes.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STCrosses()` para testar duas instâncias de `geometry` para verificar se elas se cruzam.  
  
```  
DECLARE @g geometry;  
DECLARE @h geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 2, 2 0)', 0);  
SET @h = geometry::STGeomFromText('LINESTRING(0 0, 2 2)', 0);  
SELECT @g.STCrosses(@h);  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

