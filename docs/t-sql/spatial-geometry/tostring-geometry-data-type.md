---
description: ToString (tipo de dados geometry)
title: ToString (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ToString (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- ToString (geometry Data Type)
ms.assetid: 2e55fa98-aa22-4baa-a516-7c233a33e212
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: d5b8e9d4c027dd364c9aaf84b4b8e56680548d0c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88305493"
---
# <a name="tostring-geometry-data-type"></a>ToString (tipo de dados geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna a representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) de uma instância geométrica, aumentada com qualquer valor Z (elevação) e M (medida) presente na instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.ToString ()  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **nvarchar(max)**  
  
 Tipo de retorno do CLR: **SqlString**  
  
## <a name="remarks"></a>Comentários  
 Esse método retornará a cadeia de caracteres "Nulo" quando chamado em instâncias nulas.  
  
 Em instâncias não nulas, esse método é equivalente a usar `AsTextZM().`  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `LineString` e usa `ToString()` para buscar a descrição de texto da instância.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 0 1, 1 0)', 0);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [STAsText &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/stastext-geometry-data-type.md)   
 [Métodos estendidos em instâncias geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
  
  

