---
title: Método executeUpdate (java.lang.String, java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.executeUpdate (java.lang.String[])
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2f44a689-65c8-4c94-9574-e9c08ea7918e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f99b9153b09ed268444a90dd054535c0e61ae060
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924266"
---
# <a name="executeupdate-method-javalangstring-javalangstring"></a>Método executeUpdate (java.lang.String, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Executa a instrução SQL fornecida e sinaliza ao [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] que as chaves geradas automaticamente, indicadas na matriz fornecida, devem ser disponibilizadas para recuperação.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public final int executeUpdate(java.lang.String sql,  
                               java.lang.String[] columnNames)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *sql*  
  
 Uma **String** que contém uma instrução SQL.  
  
 *columnNames*  
  
 Uma matriz do tipo **String** que indica quais nomes de coluna das chaves geradas automaticamente devem ser disponibilizados.  
  
## <a name="return-value"></a>Valor retornado  
 Um **int** que indica o número de linhas afetadas; 0 se estiver sendo usada uma instrução DDL.  
  
## <a name="exceptions"></a>Exceções  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentários  
 Esse método executeUpdate é especificado pelo método executeUpdate na interface java.sql.Statement.  
  
 Se a execução de um procedimento armazenado resultar em uma contagem de atualização maior que um, ou que gere mais de um conjunto de resultados, use o método [execute](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md) para executar o procedimento armazenado.  
  
## <a name="see-also"></a>Consulte Também  
 [Método executeUpdate &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)   
 [Membros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Classe SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
