---
title: Método supportsTableCorrelationNames (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsTableCorrelationNames
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 85d4eb84-6d0a-4671-b6e5-a7085e086fcf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5d55b8407614d45e0231bf16576cdd85a4241496
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80908752"
---
# <a name="supportstablecorrelationnames-method-sqlserverdatabasemetadata"></a>Método supportsTableCorrelationNames (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera se esse banco de dados oferece suporte a nomes de correlação de tabela.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public boolean supportsTableCorrelationNames()  
```  
  
## <a name="return-value"></a>Valor retornado  
 **true** se houver suporte. Caso contrário, **false**.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método supportsTableCorrelationNames é especificado pelo método supportsTableCorrelationNames na interface java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte Também  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Membros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Classe SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
