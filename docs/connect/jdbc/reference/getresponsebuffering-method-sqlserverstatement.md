---
title: Método getResponseBuffering (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getResponseBuffering()
apilocation:
- SQLServerStatement.getResponseBuffering()
apitype: Assembly
ms.assetid: a9a9ffdd-7ce3-4e0a-907c-34d6a54e6865
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5848bd6b1f77d3989bed1300a7127391e1ff3c27
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921863"
---
# <a name="getresponsebuffering-method-sqlserverstatement"></a>Método getResponseBuffering (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera o modo de buffer de resposta do objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final java.lang.String getResponseBuffering()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Uma **String** que contém um valor **full** ou **adaptive** em minúsculas.  
  
## <a name="remarks"></a>Comentários  
 **adaptive** especifica o armazenamento do mínimo possível de dados em buffer, quando necessário.  
  
 **full** especifica a leitura do resultado inteiro no servidor em tempo de execução.  
  
 **adaptive** é o valor padrão no JDBC Driver versão 2.0 e 3.0. **full** era o padrão antes do JDBC Driver versão 2.0.  
  
 Para obter mais informações sobre como usar o modo de buffer de resposta, confira [Como usar o buffer adaptável](../../../connect/jdbc/using-adaptive-buffering.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Método setResponseBuffering &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)   
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
