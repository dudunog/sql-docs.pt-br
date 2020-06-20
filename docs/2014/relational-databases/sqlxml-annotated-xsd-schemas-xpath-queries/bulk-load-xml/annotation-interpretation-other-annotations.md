---
title: Outras anotações (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- url-encode annotation
- sql:key-fields
- use-cdata annotation
- sql:is-mapping-schema
- sql:url-encode
- sql:id-prefix
- sql:use-cdata
- key-fields annotation
- id-prefix annotation [SQLXML]
- is-mapping-schema annotation
ms.assetid: f7b4d37b-d6d3-4ac3-b2fd-a0b534a924e4
author: rothja
ms.author: jroth
ms.openlocfilehash: b654568c93df0a0c3e08cf6eaa615b7026a9c18a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85003123"
---
# <a name="other-annotations-sqlxml-40"></a>Outras anotações (SQLXML 4.0)
  Além das anotações discutidas nos tópicos anteriores nesta seção, o carregamento em massa de XML interpreta estas outras anotações:  
  
 `sql:id-prefix`  
 Se o esquema especificar prefixos aos dados XML, o carregamento em massa de XML removerá os prefixos antes de enviar os dados ao Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 `sql:use-cdata`  
 O carregamento em massa de XML lê o texto que é armazenado nas seções CDATA e os envia para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 `sql:url-encode`  
 O carregamento em massa de XML não dá suporte esta anotação. Por exemplo, você não pode especificar uma URL na entrada de dados XML e esperar que o carregamento em massa de XML leia os dados desse local para armazená-los no banco de dados.  
  
 `sql:is-mapping-schema`  
 O carregamento em massa de XML não dá suporte esta anotação, nem dá suporte a `sql:id`.  
  
> [!NOTE]  
>  O carregamento em massa de XML não dá suporte a esquemas de mapeamento embutidos.  
  
 `sql:key-fields`  
 O carregamento em massa de XML sempre ignora esta anotação.  
  
## <a name="see-also"></a>Consulte Também  
 [Interpretação de anotação &#40;SQLXML 4,0&#41;](annotation-interpretation-sqlxml-4-0.md)  
  
  
