---
title: Método getTrustStore (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getTrustStore Method (SQLServerDataSource)
apilocation:
- getTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 8f5850e4-8627-49a8-ba0e-b1f4014322a5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 43b537a20cf39d64e06baf6f0cae78ed46526915
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80911153"
---
# <a name="gettruststore-method-sqlserverdatasource"></a>Método getTrustStore (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Retorna o caminho (inclusive o nome do arquivo) para o arquivo trustStore do certificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public java.lang.String getTrustStore()  
```  
  
## <a name="return-value"></a>Valor retornado  
 Uma **cadeia de caracteres** que contém o caminho (inclusive o nome do arquivo) para o arquivo trustStore do certificado ou nulo se nenhum valor for definido.  
  
## <a name="remarks"></a>Comentários  
 Se a propriedade trustStore não for definida, o método [getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md) retornará nulo.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
