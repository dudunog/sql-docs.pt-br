---
title: STSrid (tipo de dados geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STSrid (geography Data Type)
- STSrid_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STSrid method
ms.assetid: 6b04f5a7-2e69-4d34-901e-b61ba6ca9c14
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 4561b52049da9c051b7e8eda3835545f600c0e70
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68120784"
---
# <a name="stsrid-geography-data-type"></a>STSrid (tipo de dados geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  **STSrid** é um inteiro que representa o SRID (identificador de referência espacial) da instância.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STSrid  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **int**  
  
 Tipo do CLR: **SqlInt32**  
  
## <a name="remarks"></a>Comentários  
 Essa propriedade pode ser modificada.  
  
## <a name="examples"></a>Exemplos  
 O primeiro exemplo cria uma instância de `geography` com o valor 4326 de SRID (WGS84) e usa `STSrid` para confirmar o SRID.  
  
```  
DECLARE @g geography;  
SET @g = geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656)', 4326);  
SELECT @g.STSrid;  
```  
  
 O segundo exemplo usa `STSrid` para alterar o valor de SRID da instância para 4267 (NAD27) e confirma o valor de SRID modificado.  
  
```  
SET @g.STSrid = 4267;  
SELECT @g.STSrid;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos do OGC em instâncias de geografia](../../t-sql/spatial-geography/ogc-methods-on-geography-instances.md)   
 [SRIDs &#40;Spatial Reference Identifiers&#41;](../../relational-databases/spatial/spatial-reference-identifiers-srids.md)  
  
  
