---
description: STPointN (tipo de dados geometry)
title: STPointN (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 08/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STPointN_TSQL
- STPointN (geometry Data Type)
dev_langs:
- TSQL
helpviewer_keywords:
- STPointN (geometry Data Type)
ms.assetid: 8f0bb3b7-5cd9-42c2-b9f8-f04628653bd0
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 751fc973188d7fe12ea0034a14c4620808912545
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88444915"
---
# <a name="stpointn-geometry-data-type"></a>STPointN (tipo de dados geometry)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Retorna um ponto especificado em uma instância de **geometry**.
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
.STPointN ( expression )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *expressão*  
 É uma expressão **int** entre 1 e o número de pontos na instância de **geometry**.  
  
## <a name="return-types"></a>Tipos de retorno  
 Tipo de retorno do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: **geometry**  
  
 Tipo de retorno do CLR: **SqlGeometry**  
  
 Tipo do OGC (Open Geospatial Consortium): **Point**  
  
## <a name="remarks"></a>Comentários  
 Se uma instância de **geometry** for criada pelo usuário, `STPointN()` retornará o ponto especificado pela *expressão* ordenando os pontos pela ordem de entrada original.  
  
 Se uma instância de **geometry** for construída pelo sistema, `STPointN()` retornará o ponto especificado por *expressão* ordenando os pontos na mesma ordem em que eles seriam emitidos: primeiro pela geometria, depois pelo anel na geometria (se apropriado) e, em seguida, pelo ponto dentro do anel. Essa ordem é determinística.  
  
 Se esse método for chamado com um valor menor que 1, ele gerará uma **ArgumentOutOfRangeException**.  
  
 Se esse método for chamado com um valor maior que o número de pontos na instância, retornará nulo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria uma instância `LineString` e usa `STPointN()` para recuperar o segundo o ponto na descrição da instância.  
  
```  
DECLARE @g geometry;  
SET @g = geometry::STGeomFromText('LINESTRING(0 0, 2 2, 1 0)', 0);  
SELECT @g.STPointN(2).ToString();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos OGC em instâncias geometry](../../t-sql/spatial-geometry/ogc-methods-on-geometry-instances.md)  
  
  

