---
description: Método moveToInsertRow (SQLServerResultSet)
title: Método moveToInsertRow (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.moveToInsertRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f3c54bfe-d5b7-4f6e-ae6c-3e8954e5b1c9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 637aab5fb6ea678bd95784c118367c1f4254d525
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433208"
---
# <a name="movetoinsertrow-method-sqlserverresultset"></a>Método moveToInsertRow (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Move o cursor para a linha de inserção.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public void moveToInsertRow()  
```  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método moveToInsertRow é especificado pelo método moveToInsertRow na interface java.sql.ResultSet.  
  
 A posição do cursor atual será lembrada enquanto o cursor estiver posicionado na linha de inserção. A linha de inserção é uma linha especial associada a um conjunto de resultados atualizável. É essencialmente um buffer onde uma nova linha pode ser construída chamando os métodos updater antes de adicionar a linha ao conjunto de resultados.  
  
 Apenas os métodos updater, getter e [insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md) poderão ser chamados quando o cursor estiver na linha de inserção. Todas as colunas em um conjunto de resultados precisam receber um valor toda vez que esse método é chamado e antes de chamar insertRow. Um método updater deve ser chamado antes que um método getter possa ser chamado em um valor de coluna.  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Classe SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
