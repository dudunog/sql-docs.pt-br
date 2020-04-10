---
title: Classe SQLServerPreparedStatement | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: a8481c06-fbba-432b-8c69-4f4619c20ad4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7a1a8b95814cbd9a75dad0b9a42a474d932a88d4
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923474"
---
# <a name="sqlserverpreparedstatement-class"></a>Classe SQLServerPreparedStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa a implementação básica da funcionalidade de instrução preparada JDBC.  
  
 **Pacote:** com.microsoft.sqlserver.jdbc  
  
 **Estende:** SQLServerStatement  
  
 **Implementa:** [ISQLServerPreparedStatement](../../../connect/jdbc/reference/isqlserverpreparedstatement-interface.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
public class SQLServerPreparedStatement  
```  
  
## <a name="remarks"></a>Comentários  
 SQLServerPreparedStatement fornece métodos que permitem que você forneça parâmetros como qualquer tipo nativo do Java e vários tipos de objetos Java. SQLServerPreparedStatement prepara uma instrução usando o procedimento armazenado [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **sp_prepare** e, em seguida, reutiliza o identificador de instrução retornada para cada execução subsequente da instrução, normalmente usando diferentes parâmetros fornecidos pelo usuário.  
  
 SQLServerPreparedStatement é compatível com o processamento em lotes, em que um conjunto de instruções preparadas é executado em uma viagem de ida e volta do banco de dados individual, para melhorar o desempenho do runtime.  
  
 Essa classe dá suporte ao desencapsulamento da classe SQLServerPreparedStatement, da interface ISQLServerPreparedStatement, da interface java.sql.PreparedStatement e das classes e interfaces compatíveis com o SQLServerStatement para desencapsulamento. Para obter mais informações, confira [Wrappers e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Membros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Referência de API do JDBC Driver](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
