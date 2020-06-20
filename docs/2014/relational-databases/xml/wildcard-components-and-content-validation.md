---
title: Componentes curinga e validação de conteúdo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- wildcard components [XML]
- content validation [XML]
ms.assetid: ffa7d974-3645-446c-8425-f0b22b6b060a
author: rothja
ms.author: jroth
ms.openlocfilehash: 07cff70d32d7d39619ecf3ee4ce36e37f2dee924
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85012877"
---
# <a name="wildcard-components-and-content-validation"></a>Componentes curinga e validação de conteúdo
  Componentes curinga são usados para aumentar a flexibilidade do que é permitido aparecer em um modelo de conteúdo. Esses componentes têm suporte na linguagem XSD das seguintes maneiras:  
  
-   Componentes curinga de elemento. Eles são representados pelo **\<xsd:any>** elemento.  
  
-   Componentes curinga de atributo. Eles são representados pelo **\<xsd:anyAttribute>** elemento.  
  
 Ambos os elementos de caractere curinga **\<xsd:any>** e **\<xsd:anyAttribute>** oferecem suporte ao uso de um atributo **ProcessContents** . Isso permite especificar um valor que indica como aplicativos XML tratam a validação do conteúdo do documento associado a esses elementos de caracteres curinga. Estes são os diferentes valores e seus efeitos:  
  
-   O valor **strict** especifica que o conteúdo é completamente validado.  
  
-   O valor **skip** especifica que o conteúdo não é validado.  
  
-   O valor **lax** especifica que apenas elementos e atributos para os quais definições de esquema estão disponíveis são validados.  
  
## <a name="lax-validation-and-xsanytype-elements"></a>Validação incerta e elementos xs:anyType  
 A especificação do Esquema XML usa validação **lax** para elementos do tipo **anyType** . Como o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] não dá suporte à validação incerta, a validação estrita foi aplicada para elementos do **anyType**. A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], há suporte para a validação incerta. Conteúdo de elementos do tipo **anyType** serão validados usando a validação incerta.  
  
 O exemplo a seguir ilustra a validação incerta. O elemento do esquema `e` é do tipo **anyType** . O exemplo cria variáveis **xml** com tipo e ilustra a validação incerta do elemento do tipo **anyType** .  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema"   
        targetNamespace="http://ns">  
   <element name="e" type="anyType"/>  
   <element name="a" type="byte"/>  
   <element name="b" type="string"/>  
 </schema>'  
GO  
```  
  
 O exemplo a seguir tem êxito, porque a validação de `<e>` tem êxito:  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>1</a><b>data</b></e>'  
GO  
```  
  
 O seguinte exemplo tem êxito. A instância é aceita, embora nenhum elemento `<c>` esteja definido no esquema:  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>1</a><c>Wrong</c><b>data</b></e>'  
GO  
```  
  
 A instância XML no exemplo a seguir é rejeitada, porque a definição do elemento `<a>` não permite um valor de cadeia de caracteres.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="http://ns"><a>Wrong</a><b>data</b></e>'  
SELECT @var  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Requisitos e limitações para o uso de Coleções de Esquemas XML no servidor](requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
