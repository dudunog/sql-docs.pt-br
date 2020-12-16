---
description: JSON_VALUE (Transact-SQL)
title: JSON_VALUE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2020
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- JSON_VALUE
- JSON_VALUE_TSQL
helpviewer_keywords:
- JSON_VALUE function
- JSON, extracting
- JSON, querying
ms.assetid: cd016e14-11eb-4eaf-bf05-c7cfcc820a10
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017
ms.openlocfilehash: 567395526bdf514153d21645da5dc5a5454c00ce
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472067"
---
# <a name="json_value-transact-sql"></a>JSON_VALUE (Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi-asa](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa.md)]

 Extrai um valor escalar de uma cadeia de caracteres JSON.  
  
 Para extrair um objeto ou uma matriz de uma cadeia de caracteres JSON em vez de um valor escalar, confira [JSON_QUERY &#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md). Para obter informações sobre as diferenças entre **JSON_VALUE** e **JSON_QUERY**, confira [Comparar JSON_VALUE e JSON_QUERY](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
JSON_VALUE ( expression , path )  
```  
  
## <a name="arguments"></a>Argumentos

 *expressão*  
 Uma expressão. Normalmente, o nome de uma variável ou de uma coluna que contém o texto JSON.  

 Se **JSON_VALUE** localizar um JSON que não seja válido na *expressão* antes de localizar o valor identificado por *path*, a função retornará um erro. Se **JSON_VALUE** não localizar o valor identificado por *path*, ele examinará todo o texto e retornará um erro se localizar um JSON que não seja válido em nenhum lugar na *expressão*.
  
 *path*  
 Um demarcador JSON que especifica a propriedade a ser extraída. Para obter mais informações, confira [Expressões de demarcador JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  

No [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] e no [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)], você pode fornecer uma variável como o valor de *path*.
  
 Se o formato de *path* não for válido, **JSON_VALUE** retornará um erro.  
  
## <a name="return-value"></a>Valor retornado

 Retorna um valor de texto único do tipo nvarchar(4000). A ordenação do valor retornado é a mesma que a ordenação da expressão de entrada.  
  
 Se o valor tiver mais que 4000 caracteres:  
  
- No modo incerto **JSON_VALUE** retorna nulo.  
  
- No modo estrito, **JSON_VALUE** retorna um erro.  
  
 Se você precisar retornar valores escalares com mais de 4000 caracteres, use **OPENJSON** em vez de **JSON_VALUE**. Para obter mais informações, veja [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).  
  
## <a name="remarks"></a>Comentários

### <a name="lax-mode-and-strict-mode"></a>Modo incerto e modo estrito

 Considere o seguinte texto JSON:  
  
```json  
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=N'{  
     "info":{    
       "type":1,  
       "address":{    
         "town":"Bristol",  
         "county":"Avon",  
         "country":"England"  
       },  
       "tags":["Sport", "Water polo"]  
    },  
    "type":"Basic"  
 }'  
```  
  
 A tabela a seguir compara o comportamento de **JSON_VALUE** no modo incerto e no modo estrito. Para obter mais informações sobre a especificação de modo de demarcador opcional (incerto ou estrito), confira [Expressões de demarcador JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|Caminho|Valor retornado no modo incerto|Valor retornado no modo estrito|Obter mais informações|  
|----------|------------------------------|---------------------------------|---------------|  
|$|NULO|Erro|Não é um valor escalar.<br /><br /> Use **JSON_QUERY** nesse caso.|  
|$.info.type|N'1'|N'1'|N/A|  
|$.info.address.town|N'Bristol'|N'Bristol'|N/A|  
|$.info."address"|NULO|Erro|Não é um valor escalar.<br /><br /> Use **JSON_QUERY** nesse caso.|  
|$.info.tags|NULO|Erro|Não é um valor escalar.<br /><br /> Use **JSON_QUERY** nesse caso.|  
|$.info.type[0]|NULO|Erro|Não é uma matriz.|  
|$.info.none|NULO|Erro|A propriedade não existe.|  
| &nbsp; | &nbsp; | &nbsp; | &nbsp; |
  
## <a name="examples"></a>Exemplos  
  
### <a name="example-1"></a>Exemplo 1
 O exemplo a seguir usa os valores das propriedades JSON `town` e `state` nos resultados da consulta. Como **JSON_VALUE** preserva a ordenação da origem, a ordem de classificação dos resultados depende da ordenação da coluna `jsonInfo`. 

> [!NOTE]
> (Este exemplo assume que uma tabela denominada `Person.Person` contém uma coluna `jsonInfo` de texto JSON e que essa coluna tem a estrutura mostrada anteriormente na discussão sobre modo incerto e modo estrito. No banco de dados AdventureWorks de exemplo, a tabela `Person` realmente não contém uma coluna `jsonInfo`.)
  
```sql  
SELECT FirstName, LastName,
 JSON_VALUE(jsonInfo,'$.info.address[0].town') AS Town
FROM Person.Person
WHERE JSON_VALUE(jsonInfo,'$.info.address[0].state') LIKE 'US%'
ORDER BY JSON_VALUE(jsonInfo,'$.info.address[0].town')
```  
  
### <a name="example-2"></a>Exemplo 2
 O exemplo a seguir extrai o valor da propriedade JSON `town` para uma variável local.  
  
```sql
DECLARE @jsonInfo NVARCHAR(MAX)
DECLARE @town NVARCHAR(32)

SET @jsonInfo=N'{"info":{"address":[{"town":"Paris"},{"town":"London"}]}}';

SET @town=JSON_VALUE(@jsonInfo,'$.info.address[0].town'); -- Paris
SET @town=JSON_VALUE(@jsonInfo,'$.info.address[1].town'); -- London
```  
  
### <a name="example-3"></a>Exemplo 3
 O exemplo a seguir cria as colunas computadas com base nos valores das propriedades JSON.  
  
```sql  
CREATE TABLE dbo.Store
 (
  StoreID INT IDENTITY(1,1) NOT NULL,
  Address VARCHAR(500),
  jsonContent NVARCHAR(4000),
  Longitude AS JSON_VALUE(jsonContent, '$.address[0].longitude'),
  Latitude AS JSON_VALUE(jsonContent, '$.address[0].latitude')
 )
```  
  
## <a name="see-also"></a>Confira também
 [Expressões de demarcador JSON &#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [Dados JSON &#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  
  
