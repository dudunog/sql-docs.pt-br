---
title: 'Erro (Visual C++ índice de sintaxe com #import) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- 'Error collection [ADO], Visual C++ syntax index with #import'
ms.assetid: 1ee59754-59c8-48e2-a4fb-242fa788c1f9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 23208742a3c103bd25a38477a55106485fea018d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918908"
---
# <a name="error-visual-c-syntax-index-with-import"></a>Erro (Visual C++ índice de sintaxe com #import)
## <a name="properties"></a>Propriedades  
  
```  
_bstr_t GetDescription( );  
__declspec(property(get=GetDescription)) _bstr_t Description;  
  
long GetHelpContext( );  
__declspec(property(get=GetHelpContext)) long HelpContext;  
  
_bstr_t GetHelpFile( );  
__declspec(property(get=GetHelpFile)) _bstr_t HelpFile;  
  
long GetNativeError( );  
__declspec(property(get=GetNativeError)) long NativeError;  
  
long GetNumber( );  
__declspec(property(get=GetNumber)) long Number;  
  
_bstr_t GetSource( );  
__declspec(property(get=GetSource)) _bstr_t Source;  
  
_bstr_t GetSQLState( );  
__declspec(property(get=GetSQLState)) _bstr_t SQLState;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto de erro](../../../ado/reference/ado-api/error-object.md)
