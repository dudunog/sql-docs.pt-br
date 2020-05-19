---
title: Colunas com um nome especificado como um caractere curinga | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: d9551df1-5bb4-4c0b-880a-5bb049834884
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 262fd4ec636b147db0cb9de9e8b520f064e710af
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717291"
---
# <a name="columns-with-a-name-specified-as-a-wildcard-character"></a>Colunas com um nome especificado como um caractere curinga
  Se o nome da coluna especificado for um caractere curinga (\*), o conteúdo dessa coluna será inserido como se não houvesse nenhum nome de coluna especificado. Se essa coluna não for do tipo `xml`, o conteúdo da coluna será inserido como um nó de texto, conforme mostrado no exemplo a seguir:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT E.BusinessEntityID "@EmpID",   
       FirstName "*",   
       MiddleName "*",   
       LastName "*"  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
    ON E.BusinessEntityID = P.BusinessEntityID  
WHERE E.BusinessEntityID=1  
FOR XML PATH;  
```  
  
 Este é o resultado:  
  
 `<row EmpID="1">KenJS??nchez</row>`  
  
 Se a coluna for do tipo `xml`, a árvore XML correspondente será inserida. Por exemplo, a coluna a seguir especifica "*" para o nome da coluna que contém o XML retornado pelo XQuery em relação à coluna Instructions.  
  
```  
SELECT   
       ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
                /MI:root/MI:Location   
              ') as "*"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH;   
GO  
```  
  
 Este é o resultado. O XML retornado por XQuery é inserido sem um elemento de encapsulamento.  
  
 `<row>`  
  
 `<ProductModelID>7</ProductModelID>`  
  
 `<Name>HL Touring Frame</Name>`  
  
 `<MI:Location LocationID="10">...</MI:Location>`  
  
 `<MI:Location LocationID="20">...</MI:Location>`  
  
 `...`  
  
 `</row>`  
  
## <a name="see-also"></a>Consulte Também  
 [Usar o modo PATH com FOR XML](use-path-mode-with-for-xml.md)  
  
  
