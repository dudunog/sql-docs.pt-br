---
title: Método setLockTimeout (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLockTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 10dca5aa-1851-4326-9ae9-7a8430d12d11
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8143233de52f1272cf63a31f79ed280cf5124a9a
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80925765"
---
# <a name="setlocktimeout-method-sqlserverdatasource"></a>Método setLockTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Define um valor **int** que indica o número de milissegundos que o banco de dados precisa aguardar antes de informar um tempo limite de bloqueio.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void setLockTimeout(int lockTimeout)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *lockTimeout*  
  
 Um valor **int** que contém o número de milissegundos de espera.  
  
## <a name="remarks"></a>Comentários  
 O tempo limite de bloqueio é o número de milissegundos de espera antes de o banco de dados informar um tempo limite de bloqueio. O valor padrão de -1 significa que ele aguardará por tempo indefinido. Se for especificado, esse valor será o padrão para todas as instruções na conexão.  
  
> [!NOTE]  
>  Um valor de 0 significa que não haverá espera. Se a propriedade lockTimeout não estiver definida, o método [getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md) retornará o valor padrão de -1.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Classe SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
