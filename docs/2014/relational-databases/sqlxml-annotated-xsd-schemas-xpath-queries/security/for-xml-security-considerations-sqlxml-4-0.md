---
title: Considerações de segurança para FOR XML (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- NESTED mode
- client-side XML formatting
- FOR XML clause, security
- server-side XML formatting
- AUTO mode
- security [SQLXML], FOR XML
ms.assetid: facba279-df93-475b-ad43-0043dc5bae03
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6ee2ac48e03d7436f2671faa8f4883b10210a380
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717614"
---
# <a name="for-xml-security-considerations-sqlxml-40"></a>Considerações de segurança de FOR XML (SQLXML 4.0)
  O modo FOR XML AUTO gera uma hierarquia de XML na qual os nomes de elemento mapeiam para nomes de tabela e nomes de atributo mapeiam para nomes de coluna. Dessa forma, a tabela e as informações de coluna do banco de dados são expostas. Você pode ocultar as informações do banco de dados quando usar modo AUTO (formatação no lado de servidor) especificando aliases de coluna e da tabela na consulta. Esses aliases são retornados no documento XML resultante como nomes de elemento e atributos.  
  
 Por exemplo, a seguinte consulta especifica o modo de AUTO; portanto, a formatação XML é feita no servidor:  
  
```  
SELECT C.FirstName as F,C.LastName as L   
FROM Person.Contact C   
FOR XML AUTO  
```  
  
 No documento XML resultante, os aliases são usados para nomes do elemento e do atributo:  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <C F="Nancy" L="Fuller" />   
  <CE F="Andrew" L="Peacock" />   
  <C F="Janet" L="Leverling" />   
  ...  
</root>  
```  
  
 Quando você usar modo NESTED (formatação no lado do cliente), só são retornados aliases para atributos no documento XML resultante. Os nomes das tabelas base são sempre retornados como nomes de elemento. Por exemplo, a seguinte consulta especifica o modo NESTED:  
  
```  
SELECT C.FirstName as F,C.LastName as L   
FROM Person.Contact C   
FOR XML AUTO  
```  
  
 No documento XML resultante, os nomes das tabelas base são retornados como nomes de elemento, e os aliases da tabela não são usados:  
  
```  
<?xml version="1.0" encoding="utf-8" ?>   
<root>  
  <Person.Contact F="Nancy" L="Fuller" />   
  <Person.Contact F="Andrew" L="Peacock" />   
  <Person.Contact F="Janet" L="Leverling" />   
       ...  
</root>  
```  
  
  
