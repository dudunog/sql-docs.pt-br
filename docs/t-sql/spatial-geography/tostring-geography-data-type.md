---
title: ToString (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ToString (geography Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- ToString method
ms.assetid: 045c12fa-8fc6-441a-9500-7021cb4ff13e
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 3e4ca89d9fa8dccf2e819e76db188f84b25f0b59
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68120677"
---
# <a name="tostring-geography-data-type"></a>ToString (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna a representação WKT (Well-Known Text) do OGC (Open Geospatial Consortium) de uma instância de **geography**, aumentada com os valores de Z (elevação) e de M (medida) presentes na instância.  
  
 Esse método de tipo de dados de geography é compatível com instâncias **FullGlobe** ou instâncias espaciais maiores que um hemisfério.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.ToString ()  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **nvarchar(max)**  
  
 Tipo de retorno do CLR: **SqlString**  
  
## <a name="remarks"></a>Comentários  
 Esse método retorna a cadeia de caracteres "Null" quando chamado em instâncias nulas. No [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o conjunto de possíveis resultados no servidor foi estendido para instâncias de **FullGlobe**. Esse método retornará o mesmo valor que `AsTextZM()`.  
  
 Esse método não é preciso.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância de `LineString` e usa `ToString()` para retornar a descrição de texto da instância.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias de geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [AsTextZM &#40;tipo de dados geography&#41;](../../t-sql/spatial-geography/astextzm-geography-data-type.md)  
  
  
