---
title: Função substring (XQuery) | Microsoft Docs
description: Saiba mais sobre a função do XQuery substring () que retorna a parte especificada de uma cadeia de caracteres de origem.
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- substring function [XQuery]
- fn:substring function
ms.assetid: 2b3b8651-de51-46dc-af82-c86c45eac871
author: rothja
ms.author: jroth
ms.openlocfilehash: 694fb912675a15055688956a18714185e25995c4
ms.sourcegitcommit: 5c7634b007f6808c87094174b80376cb20545d5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84881921"
---
# <a name="functions-on-string-values---substring"></a>Funções em Valores da Cadeia de Caracteres – substring
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna parte do valor de *$sourceString*, começando na posição indicada pelo valor de *$startingLoc* e continua para o número de caracteres indicado pelo valor de *$Length*.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?) as xs:string?  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?,  
                          $length as xs:decimal?) as xs:string?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$sourceString*  
 Cadeia de caracteres de origem.  
  
 *$startingLoc*  
 Ponto de partida na cadeia de caracteres de origem do qual a subcadeia de caracteres é iniciada. Se esse valor for negativo ou 0, apenas aqueles caracteres em posições maiores que zero serão retornados. Se for maior que o comprimento do *$sourceString*, a cadeia de caracteres de comprimento zero será retornada.  
  
 *$length*  
 [opcional] Número de caracteres a recuperar. Se não for especificado, ele retornará todos os caracteres do local especificado em *$startingLoc* até o final da cadeia de caracteres.  
  
## <a name="remarks"></a>Comentários  
 A versão de três argumentos da função retorna os caracteres em `$sourceString` cuja posição `$p` obedece:  
  
 `fn:round($startingLoc) <= $p < fn:round($startingLoc) + fn:round($length)`  
  
 O valor de *$Length* pode ser maior que o número de caracteres no valor de *$sourceString* após a posição inicial. Nesse caso, a subcadeia de caracteres retorna os caracteres até o final de *$sourceString*.  
  
 O primeiro caractere de uma cadeia de caracteres está situado na posição 1.  
  
 Se o valor de *$sourceString* for a sequência vazia, ele será tratado como a cadeia de caracteres de comprimento zero. Caso contrário, se *$startingLoc* ou *$Length* for a sequência vazia, a sequência vazia será retornada.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres suplementares (pares substitutos)  
 O comportamento de pares substitutos em funções XQuery depende do nível de compatibilidade do banco de dados e, em alguns casos, o URI do namespace padrão para funções. Para obter mais informações, consulte a seção "as funções do XQuery são de reconhecimento de substitutos" no tópico [alterações significativas em mecanismo de banco de dados recursos no SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md). Consulte também o [nível de compatibilidade de ALTER DATABASE &#40;&#41;](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) e [agrupamento e suporte a Unicode](../relational-databases/collations/collation-and-unicode-support.md)do Transact-SQL.  
  
## <a name="implementation-limitations"></a>Limitações de implementação  
 SQL Server requer que os parâmetros *$startingLoc* e *$Length* sejam do tipo xs: decimal em vez de xs: Double.  
  
 SQL Server permite que *$startingLoc* e *$Length* sejam a sequência vazia, porque a sequência vazia é um valor possível como resultado de os erros dinâmicos serem mapeados para ().  
  
## <a name="examples"></a>Exemplos  
 Este tópico fornece exemplos de XQuery em relação a instâncias XML armazenadas em várias colunas de tipo **XML** no [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] banco de dados.  
  
### <a name="a-using-the-substring-xquery-function-to-retrieve-partial-summary-product-model-descriptions"></a>a. Usando uma função substring() XQuery para recuperar descrições resumidas parciais de modelos de produtos  
 A consulta recupera os primeiros 50 caracteres do texto que descreve o modelo de produto, o <`Summary`> elemento no documento.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Prod>{ substring(string((/pd:ProductDescription/pd:Summary)[1]), 1, 50) }</Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('/pd:ProductDescription')  = 1;  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A função **String ()** retorna o valor da cadeia de caracteres do `Summary` elemento<>. Essa função é usada, porque o `Summary` elemento <> contém o texto e os subelementos (elementos de formatação HTML) e, como você vai ignorar esses elementos e recuperar todo o texto.  
  
-   A função **substring ()** recupera os primeiros 50 caracteres do valor de cadeia de caracteres recuperado pela **cadeia de caracteres ()**.  
  
 Este é um resultado parcial:  
  
```  
ProductModelID Result  
-------------- ----------------------------------------------------  
19      <Prod>Our top-of-the-line competition mountain bike.</Prod>   
23      <Prod>Suitable for any type of riding, on or off-roa</Prod>  
...  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções XQuery em tipos de dados xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
