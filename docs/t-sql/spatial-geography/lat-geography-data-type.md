---
description: Lat (tipo de dados geography)
title: LAT (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Lat
- Lat_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- Lat method
ms.assetid: 051d66bc-04de-4c58-861c-760dc5b859b5
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: e6aff42dafc123d19fd8a2ea9a2ffa637cc54ee3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88422360"
---
# <a name="lat-geography-data-type"></a>Lat (tipo de dados geography)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  A propriedade de latitude da instância de **geography**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
.Lat  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
 Tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **float**  
  
 Tipo CLR: **SqlDouble**  
  
## <a name="remarks"></a>Comentários  
 No modelo OpenGIS, Lat só é definida nas instâncias de **geografia** compostas por um único ponto. Essa propriedade retornará NULL se instâncias de **geography** contiverem mais de um ponto. Essa propriedade é exata e somente leitura.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo cria um ponto e retorna a latitude do ponto.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('POINT(-122.34900 47.65100)', 4326);  
SELECT @g.Lat;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias geography](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)  
  
  
