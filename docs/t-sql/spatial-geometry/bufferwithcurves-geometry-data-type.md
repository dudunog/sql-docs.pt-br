---
description: BufferWithCurves (tipo de dados geometria)
title: BufferWithCurves (tipo de dados geometry) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- BufferWithCurves method (geometry)
ms.assetid: 8ffaba3f-d2dd-4e57-9f41-3ced9f14b600
author: MladjoA
ms.author: mlandzic
monikerRange: =azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 490c7fa9a046976dfa2e3390bf52c8f5fc3e274f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97476647"
---
# <a name="bufferwithcurves-geometry-data-type"></a>BufferWithCurves (tipo de dados geometria)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Retorna uma instância de **geometry** que representa o conjunto de todos os pontos cuja distância da instância de **geometry** de chamada é menor ou igual ao parâmetro *distance*.  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
.BufferWithCurves ( distance )  
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos  
 *distance*  
 É um **float** que indica a distância máxima em que os pontos que formam o buffer podem estar da instância de **geometry**.  
  
## <a name="return-types"></a>Tipos de retorno
Tipo de retorno do SQL Server: **geometry**  
  
 Tipo de retorno do CLR: **SqlGeometry**  
  
## <a name="exceptions"></a>Exceções  
 Os critérios a seguir gerarão uma **ArgumentException**.  
  
-   Nenhum parâmetro é passado ao método, como `@g.BufferWithCurves()`  
  
-   Um parâmetro não numérico é passado para o método, como `@g.BufferWithCurves('a')`  
  
-   **NULL** é passado ao método, como `@g.BufferWithCurves(NULL)`  
  
## <a name="remarks"></a>Comentários  
 A ilustração a seguir mostra um exemplo de uma instância de geometria retornado por este método.  
  
 ![Diagrama que mostra um exemplo de uma instância de geometria retornada por este método.](../../t-sql/spatial-geometry/media/bufferedcurve.gif)
  
 A tabela a seguir mostra os resultados retornados para obter valores de distância diferentes.  
  
|Valor de distância|Dimensões do tipo|Tipo espacial retornado|  
|--------------------|---------------------|---------------------------|  
|distância < 0|Zero ou um|Instância de **GeometryCollection** vazia|  
|distância < 0|Dois ou mais|Uma instância de **CurvePolygon** ou **GeometryCollection** com um buffer negativo. **Observação:** Um buffer negativo pode criar uma **GeometryCollection** vazia|  
|distância = 0|Todas as dimensões|Cópia da instância de **geometry** de invocação|  
|distância > 0|Todas as dimensões|Instância de **CurvePolygon** ou **GeometryCollection**|  
  
> [!NOTE]  
>  Como *distance* é um **float**, um valor muito pequeno pode ser igualado a zero nos cálculos. Quando isto ocorre, uma cópia da instância de **geometry** de chamada é retornada. Consulte [float e real &#40;Transact-SQL&#41;](../../t-sql/data-types/float-and-real-transact-sql.md).  
  
 Um buffer negativo remove todos os pontos incluídos na distância especificada do limite da geometria. A ilustração a seguir mostra um buffer negativo como a área sombreada mais clara do círculo. A linha pontilhada é o limite do polígono original e a linha sólida é o limite do polígono resultante.  
  
 Se um parâmetro **string** for passado ao método, ele será convertido em um **float** ou gerará uma `ArgumentException`.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-calling-bufferwithcurves-with-a-parameter-value--0-on-one-dimensional-geometry-instance"></a>a. Como chamar BufferWithCurves() com um valor de parâmetro < 0 em uma instância de geometria unidimensional  
 O exemplo a seguir retorna uma instância `GeometryCollection` vazia:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(-1).ToString(); 
 ```
  
### <a name="b-calling-bufferwithcurves-with-a-parameter-value--0-on-a-two-dimensional-geometry-instance"></a>B. Como chamar BufferWithCurves() com um valor de parâmetro < 0 em uma instância de geometria bidimensional  
 O exemplo a seguir retorna uma instância `CurvePolygon` com um buffer negativo:  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.BufferWithCurves(-1).ToString()
 ```  
  
### <a name="c-calling-bufferwithcurves-with-a-parameter-value--0-that-returns-an-empty-geometrycollection"></a>C. Como chamar BufferWithCurves() com um valor de parâmetro < 0 que retorna uma GeometryCollection vazia  
 O seguinte exemplo mostra o que ocorre quando o parâmetro *distance* é igual a -2:  
  
```
 DECLARE @g geometry = 'CURVEPOLYGON(COMPOUNDCURVE(CIRCULARSTRING(0 4, 4 0, 8 4), (8 4, 0 4)))'; 
 SELECT @g.BufferWithCurves(-2).ToString();
 ```  
  
 Esta instrução **SELECT** retorna `GEOMETRYCOLLECTION EMPTY`  
  
### <a name="d-calling-bufferwithcurves-with-a-parameter-value--0"></a>D. Chamando BufferWithCurves() com um valor de parâmetro = 0  
 O seguinte exemplo retorna uma cópia da instância de **geometry** de chamada:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(0).ToString();
 ```  
  
### <a name="e-calling-bufferwithcurves-with-a-non-zero-parameter-value-that-is-extremely-small"></a>E. Chamando BufferWithCurves() com um valor de parâmetro diferente de zero que é extremamente pequeno  
 O seguinte exemplo também retorna uma cópia da instância de **geometry** de chamada:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)'; 
 DECLARE @distance float = 1e-20; 
 SELECT @g.BufferWithCurves(@distance).ToString();
 ```  
  
### <a name="f-calling-bufferwithcurves-with-a-parameter-value--0"></a>F. Como chamar BufferWithCurves() com um valor de parâmetro > 0  
 O exemplo a seguir retorna uma instância `CurvePolygon`:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves(2).ToString();
 ```  
  
### <a name="g-passing-a-valid-string-parameter"></a>G. Transmitindo um parâmetro de cadeia de caracteres válido  
 O exemplo a seguir retorna a mesma instância `CurvePolygon` como mencionado anteriormente, mas um parâmetro de cadeia de caracteres é passado ao método:  
  
```
 DECLARE @g geometry= 'LINESTRING(3 4, 8 11)'; 
 SELECT @g.BufferWithCurves('2').ToString();
 ```  
  
### <a name="h-passing-an-invalid-string-parameter"></a>H. Transmitindo um parâmetro de cadeia de caracteres inválido  
 O exemplo a seguir lançará um erro:  
  
```
 DECLARE @g geometry = 'LINESTRING(3 4, 8 11)' 
 SELECT @g.BufferWithCurves('a').ToString();
 ```  
  
 Observe que os dois exemplos anteriores transmitiram uma cadeia de caracteres literal ao método `BufferWithCurves()`. O primeiro exemplo funciona porque o literal de cadeia de caracteres pode ser convertido em um valor numérico. Porém, o segundo exemplo lança `ArgumentException`.  
  
### <a name="i-calling-bufferwithcurves-on-multipoint-instance"></a>I. Chamando BufferWithCurves() em instância de MultiPoint  
 O exemplo a seguir retorna duas instâncias `GeometryCollection` e uma instância `CurvePolygon`:  
  
```
 DECLARE @g geometry = 'MULTIPOINT((1 1),(1 4))'; 
 SELECT @g.BufferWithCurves(1).ToString(); 
 SELECT @g.BufferWithCurves(1.5).ToString(); 
 SELECT @g.BufferWithCurves(1.6).ToString();
 ```  
  
 As duas primeiras instruções **SELECT** retornam uma instância de `GeometryCollection` porque o parâmetro *distance* é menor ou igual a 1/2 da distância entre os dois pontos, (1 1) e (1 4). A terceira instrução **SELECT** retorna uma instância de `CurvePolygon` porque as instâncias armazenadas em buffer dos dois pontos, (1 1) e (1 4), se sobrepõem.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos estendidos em instâncias geometry](../../t-sql/spatial-geometry/extended-methods-on-geometry-instances.md)  
 
