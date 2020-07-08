---
title: AsTextZM (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AsTextZM_TSQL
- AsTextZM
- AsTextZM (geometry Data Type)
- AsTextZM_(geometry_Data_Type)_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- AsTextZM (geometry Data Type)
ms.assetid: 08ac8aa0-aff7-4b22-87e0-1a1d55dcbc04
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 7754190fe629412ddc08e7087626b05ff2c093d9
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85700829"
---
# <a name="astextzm-geometry-data-type"></a>AsTextZM (tipo de dados geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna a representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) de uma instância de geometria, aumentada com um valor **Z** (elevação) e **M** (medida) presente na instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.AsTextZM ()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **nvarchar(max)**  
  
 Tipo de retorno do CLR: **SqlChars**  
  
## <a name="remarks"></a>Comentários  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `Point` que contém valores de **Z** (elevação) e **M** (medida). `STAsText()` seleciona os valores WKT, (1 2); `AsTextZM()` seleciona os mesmos valores WKT e também retorna os valores de **Z** e **M**, com um resultado (1 2 3 4).  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('POINT(1 2 3 4)', 0);  
SELECT @g.STAsText();  
SELECT @g.AsTextZM();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias de geometria](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)   
 [M &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/m-geometry-data-type.md)   
 [Z &#40;tipo de dados geometry&#41;](../../t-sql/spatial-geometry/z-geometry-data-type.md)  
  
  

