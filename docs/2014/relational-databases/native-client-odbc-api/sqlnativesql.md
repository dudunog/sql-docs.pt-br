---
title: SQLNativeSql | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLNativeSql function
ms.assetid: 2d999fec-9e22-4514-ad5f-22a64b82f95b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0556d4e3b06c68e70513d68a5c2616bf47fc299c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63046731"
---
# <a name="sqlnativesql"></a>SQLNativeSql
  O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client atende a solicitações de **SQLNativeSql** sem visitar o servidor. A função testa a sintaxe de instruções SQL de forma eficaz. A verificação de sintaxe não determina se os identificadores ou os resultados de expressões nas instruções SQL são válidos e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native SQL retornado pela função **SQLNativeSql** pode apresentar falha na execução.  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLNativeSql](https://go.microsoft.com/fwlink/?LinkID=59358)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
