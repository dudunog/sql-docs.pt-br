---
title: Remover os colchetes da opção do JSON – WITHOUT_ARRAY_WRAPPER
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- WITHOUT_ARRAY_WRAPPER
ms.assetid: aa86c2d1-458e-465f-abfa-75470137d054
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7d4e2757f8ae471ae4e050612fb4e1e8d20fe550
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730396"
---
# <a name="remove-square-brackets-from-json---without_array_wrapper-option"></a>Remover os colchetes da opção do JSON – WITHOUT_ARRAY_WRAPPER
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Para remover, por padrão, os colchetes que envolvem a saída JSON da cláusula **FOR JSON** , especifique a opção **WITHOUT_ARRAY_WRAPPER** . Use essa opção com um resultado de linha única para gerar um único objeto JSON como saída em vez de uma matriz com um único elemento.

Se você usar essa opção com um resultado de várias linhas, a saída resultante não será um JSON válido devido aos vários elementos e aos colchetes ausentes.  
  
## <a name="example-single-row-result"></a>Exemplo (resultados de linha única)  
O exemplo a seguir mostra a saída da cláusula **FOR JSON** com e sem a opção **WITHOUT_ARRAY_WRAPPER** .  
  
 **Consulta**  
  
```sql  
SELECT 2015 as year, 12 as month, 15 as day  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  

 **Resultado** com a opção **WITHOUT_ARRAY_WRAPPER**  
  
```json  
{
    "year": 2015,
    "month": 12,
    "day": 15
} 
```  
  
 **Resultado** (padrão) sem a opção **WITHOUT_ARRAY_WRAPPER**  
  
```json  
[{
    "year": 2015,
    "month": 12,
    "day": 15
}]
```  

## <a name="example-multiple-row-result"></a>Exemplo (resultados de várias linhas)
Veja outro exemplo de uma cláusula **FOR JSON** com e sem a opção **WITHOUT_ARRAY_WRAPPER** . Este exemplo produz um resultado de várias linhas. A saída não é um JSON válido devido aos vários elementos e aos colchetes ausentes.
  
 **Consulta**  
  
```sql  
SELECT TOP 3 SalesOrderNumber, OrderDate, Status  
FROM Sales.SalesOrderHeader  
ORDER BY ModifiedDate  
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER 
```  
  
 **Resultado** com a opção **WITHOUT_ARRAY_WRAPPER**  
  
```json  
{
    "SalesOrderNumber": "SO43662",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43661",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
} 
```  
  
 **Resultado** (padrão) sem a opção **WITHOUT_ARRAY_WRAPPER**  
  
```json  
[{
    "SalesOrderNumber": "SO43662",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43661",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}, {
    "SalesOrderNumber": "SO43660",
    "OrderDate": "2011-05-31T00:00:00",
    "Status": 5
}]
```  

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>Saiba mais sobre JSON no SQL Server e no Banco de Dados SQL do Azure  
  
### <a name="microsoft-videos"></a>Vídeos da Microsoft

Para obter uma introdução visual ao suporte interno para JSON no SQL Server e no Banco de Dados SQL do Azure, consulte os seguintes vídeos:

-   [SQL Server 2016 e suporte para JSON](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [Usando JSON no SQL Server 2016 e no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [JSON é uma ponte entre o NoSQL e mundos relacionais](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>Consulte Também  
 [Cláusula FOR &#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)  
  
  
