---
description: InstanceOf (tipo de dados geography)
title: InstanceOf (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- InstanceOf
- InstanceOf_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- InstanceOf method
ms.assetid: 1eaed0e4-1c72-45a9-9926-5b513335cf33
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 384539d8978dd8ae169ae5cfb2b7b5abcf394686
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88422380"
---
# <a name="instanceof-geography-data-type"></a>InstanceOf (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Testa se a instância de **geography** é a mesma que o tipo especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
  
.InstanceOf ( 'geography_type')  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*geography_type*  
A cadeia de caracteres **nvarchar(4000)** que especifica um dos 16 tipos expostos na hierarquia de tipos de **geografia**.  
  
## <a name="return-types"></a>Tipos de retorno  
Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **bit**  
  
Tipo de retorno do CLR: **SqlBoolean**  
  
## <a name="remarks"></a>Comentários  
Retornará 1 se o tipo de uma instância de **geography** for o mesmo que o tipo especificado ou se o tipo especificado for um ancestral do tipo de instância, caso contrário, retornará 0.  
  
Esse método de tipo de dados de **geography** é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.  
  
A entrada para o método deve ser um destes tipos: Geometria, ponto, curva, LineString, CircularString, superfície, polígono, CurvePolygon, **GeometryCollection**, **MultiSurface**, **MultiPolygon, MultiCurve, MultiLineString**, **MultiPoint** ou **FullGlobe**.  
  
Esse método lançará uma `ArgumentException` se qualquer outra cadeia de caracteres for usada na entrada.  
  
Esse método não oferece precisão.  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir criará uma instância de `MultiPoint` e usará `InstanceOf()` para verificar se a instância é uma `GeometryCollection`.  
  
```sql  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('MULTIPOINT(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.InstanceOf('GEOMETRYCOLLECTION');  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
