---
title: geografia (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- geography
dev_langs:
- TSQL
helpviewer_keywords:
- geography data type [SQL Server], Transact-SQL
- spatial data types [SQL Server]
ms.assetid: d9e4952a-1841-4465-a64b-11e9288dba1d
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: 5b98f2283cfb9d89277ad97ffc7a883e43a42b4f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68042524"
---
# <a name="spatial-types---geography"></a>Tipos espaciais – geografia
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  O tipo de dados espaciais de geografia, **geography**, é implementado como um tipo de dados CLR (Common Language Runtime) do .NET no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse tipo representa dados em um sistema de coordenadas de terra redonda. O tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]geography**do** armazena dados elipsoidais (terra redonda), como coordenadas de latitude e longitude de GPS.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é compatível com um conjunto de métodos do tipo de dados espaciais de **geografia**. Estão inclusos métodos de **geografia** que são definidos pelo padrão OGC (Open Geospatial Consortium) e um conjunto de extensões da [!INCLUDE[msCoName](../../includes/msconame-md.md)] para esse padrão.  
 
 A tolerância de erro para os métodos de **geografia** pode chegar até as extensões de 1.0e-7 *. As extensões referem-se à distância máxima aproximada entre os pontos do objeto de **geografia**.
  

## <a name="registering-the-geography-type"></a>Registrando o tipo de geografia  
 O tipo **geography** é predefinido e está disponível em cada banco de dados. É possível criar colunas de tabelas do tipo **geography** e operar em dados de **geography** da mesma maneira como outros tipos fornecidos pelo sistema são usados. Pode ser usado em colunas computadas persistidas e não persistidas.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-showing-how-to-add-and-query-geography-data"></a>a. Mostrando como adicionar e consultar dados de geografia  
 Os exemplos a seguir mostram como adicionar e consultar dados de geografia. O primeiro exemplo cria uma tabela com uma coluna de identidade e uma coluna de `geography`, a `GeogCol1`. Uma terceira coluna renderiza a coluna de `geography` em sua representação WKT (Well-Known Text) do Open Geospatial Consortium (OGC) e usa o método `STAsText()` . Em seguida, duas linhas são inseridas: uma linha que contém uma instância `LineString` de `geography`e uma linha que contém uma instância de `Polygon` .  
  
```  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable   
    ( id int IDENTITY (1,1),  
    GeogCol1 geography,   
    GeogCol2 AS GeogCol1.STAsText() );  
GO  
  
INSERT INTO SpatialTable (GeogCol1)  
VALUES (geography::STGeomFromText('LINESTRING(-122.360 47.656, -122.343 47.656 )', 4326));  
  
INSERT INTO SpatialTable (GeogCol1)  
VALUES (geography::STGeomFromText('POLYGON((-122.358 47.653 , -122.348 47.649, -122.348 47.658, -122.358 47.658, -122.358 47.653))', 4326));  
GO  
```  
  
### <a name="b-returning-the-intersection-of-two-geography-instances"></a>B. Retornando a interseção de duas instâncias de geografia  
 O exemplo a seguir usa o método `STIntersection()` para retornar os pontos onde as duas instâncias `geography` se cruzam.  
  
```  
DECLARE @geog1 geography;  
DECLARE @geog2 geography;  
DECLARE @result geography;  
  
SELECT @geog1 = GeogCol1 FROM SpatialTable WHERE id = 1;  
SELECT @geog2 = GeogCol1 FROM SpatialTable WHERE id = 2;  
SELECT @result = @geog1.STIntersection(@geog2);  
SELECT @result.STAsText();  
```  
  
### <a name="c-using-geography-in-a-computed-column"></a>C. Usando geografia em uma coluna computada  
 O exemplo a seguir cria uma tabela com uma coluna computada persistente usando um tipo de **geografia**.  
  
```  
IF OBJECT_ID ( 'dbo.SpatialTable', 'U' ) IS NOT NULL   
    DROP TABLE dbo.SpatialTable;  
GO  
  
CREATE TABLE SpatialTable  
(  
    locationId int IDENTITY(1,1),  
    location geography,  
    deliveryArea as location.STBuffer(10) persisted  
)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Dados espaciais &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   

  
  
