---
title: Como usar um procedimento armazenado sem parâmetros | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e9470a6d-a758-4c56-96ec-7b37139e36a7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 01f59f44d42af1d0880df48b043080525d9821ee
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "69027018"
---
# <a name="using-a-stored-procedure-with-no-parameters"></a>Como usar um procedimento armazenado sem parâmetros

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

O tipo mais simples de procedimento armazenado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que é possível chamar é aquele que não contém parâmetros e retorna um único conjunto de resultados. O [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] fornece a classe [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), que pode ser usada para chamar esse tipo de procedimento armazenado e processar os dados retornados.

Ao usar o driver JDBC para chamar um procedimento armazenado sem parâmetros, você deve usar a sequência de escape SQL `call`. A sintaxe da sequência de escape `call` sem parâmetros é a seguinte:

`{call procedure-name}`

> [!NOTE]  
> Para obter mais informações sobre as sequências de escape do SQL, confira [Como usar sequências de escape do SQL](../../connect/jdbc/using-sql-escape-sequences.md).

Como exemplo, crie o seguinte procedimento armazenado no banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)]:

```sql
CREATE PROCEDURE GetContactFormalNames
AS  
BEGIN  
   SELECT TOP 10 Title + ' ' + FirstName + ' ' + LastName AS FormalName
   FROM Person.Contact  
END  
```

Esse procedimento armazenado retorna um único conjunto de resultados que contém uma coluna de dados, uma combinação do título, do nome e do sobrenome dos 10 primeiros contatos presentes na tabela Person.Contact.

No exemplo a seguir, uma conexão aberta com o banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] é passada para a função, e o método [executeQuery](../../connect/jdbc/reference/executequery-method-sqlserverstatement.md) é usado para chamar o procedimento armazenado GetContactFormalNames.

```java
public static void executeSprocNoParams(Connection con) throws SQLException {  
    try(Statement stmt = con.createStatement();) {  

        ResultSet rs = stmt.executeQuery("{call dbo.GetContactFormalNames}");  
        while (rs.next()) {  
            System.out.println(rs.getString("FormalName"));  
        }  
    }  
}
```

## <a name="see-also"></a>Confira também

[Como usar instruções com procedimentos armazenados](../../connect/jdbc/using-statements-with-stored-procedures.md)
