---
title: 'Exemplo: especificando XSINIL com a diretiva ELEMENTS | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, specifying XSINIL example
ms.assetid: 07c873ff-1f9d-480e-8536-862c39eb8249
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 34cc4479a26d633e689963a945095248f683993f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63287282"
---
# <a name="example-specifying-xsinil-with-the-elements-directive"></a>Exemplo: especificando XSINIL com a política ELEMENTS
  A consulta a seguir especifica a política `ELEMENTS` para gerar XML centrado em elemento a partir do resultado da consulta.  
  
## <a name="example"></a>Exemplo  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name, Color  
FROM Production.Product  
FOR XML RAW, ELEMENTS;  
GO  
```  
  
 Este é o resultado parcial.  
  
```  
<row>  
  <ProductID>1</ProductID>  
  <Name>Adjustable Race</Name>  
</row>  
...  
<row>  
  <ProductID>317</ProductID>  
  <Name>LL Crankarm</Name>  
  <Color>Black</Color>  
</row>  
```  
  
 Como a coluna `Color` tem valores nulos para alguns produtos, o XML resultante não gerará o elemento <`Color`> correspondente. Adicionando a política `XSINIL` com `ELEMENTS`, é possível gerar o elemento <`Color`> mesmo para valores de cor NULL no conjunto de resultados.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductID, Name, Color  
FROM Production.Product  
FOR XML RAW, ELEMENTS XSINIL ;  
```  
  
 Este é o resultado parcial:  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <ProductID>1</ProductID>  
  <Name>Adjustable Race</Name>  
  <Color xsi:nil="true" />  
</row>  
...  
<row>  
  <ProductID>317</ProductID>  
  <Name>LL Crankarm</Name>  
  <Color>Black</Color>  
</row>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usar o modo RAW com FOR XML](use-raw-mode-with-for-xml.md)  
  
  
