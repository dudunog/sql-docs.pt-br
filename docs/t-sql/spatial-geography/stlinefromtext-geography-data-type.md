---
title: STLineFromText (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STLineFromText (geography Data Type)
- STLineFromText_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STLineFromText method
ms.assetid: e0c05bde-077d-4ce2-b4ec-8861db9b996d
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 61aa713c0bf3862de4921c42c2fd879c36a51fc6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85736069"
---
# <a name="stlinefromtext-geography-data-type"></a>STLineFromText (tipo de dados de geografia)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna uma instância de **geography** de uma representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium), aumentada com valores Z (elevação) e M (medida) presentes na instância.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
STLineFromText ( 'linestring_tagged_text' , SRID )  
```  
  
## <a name="arguments"></a>Argumentos  
 *linestring_tagged_text*  
 É a representação WKT da instância de **geographyLineString** que você deseja retornar. *linestring_tagged_text* é uma expressão **nvarchar(max)** .  
  
 *SRID*  
 É uma expressão **int** que representa o SRID (ID de referência espacial) da instância de **geographyLineString** que você deseja retornar.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geography**  
  
 Tipo de retorno do CLR: **SqlGeography**  
  
 Tipo do OGC: **LineString**  
  
## <a name="remarks"></a>Comentários  
 Esse método gera uma **FormatException** se a entrada não está bem formatada.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir usa `STLineFromText()` para criar uma instância `geography`.  
  
```  
DECLARE @g geography;  
SET @g = geography::STLineFromText('LINESTRING(-122.360 47.656, -122.343 47.656 )', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [OGC Static Geography Methods](../../t-sql/spatial-geography/ogc-static-geography-methods.md)  
  
  
