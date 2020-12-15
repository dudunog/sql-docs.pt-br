---
title: Objeto SqlXmlAdapter (SQLXML)
description: Saiba mais sobre o objeto SqlXmlAdapter que fornece métodos que facilitam a interação com o conjunto de informações no .NET Framework.
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- void Update(DataSet ds) method
- SqlXmlAdapter object
- void Fill(DataSet ds) method
- SQLXML Managed Classes, SqlXmlAdapter object
- Managed Classes [SQLXML], SqlXmlAdapter object
ms.assetid: 0a16eddf-fc26-4d92-82d4-359b5fb905d5
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b58e0416907b32821c2d6dd99decf61ec0054917
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97414047"
---
# <a name="sqlxml-managed-classes---sqlxmladapter-object"></a>Classes gerenciadas SQLXML – Objeto SqlXmlAdapter
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Este objeto fornece métodos que facilitam a interação com o conjunto de dados no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework. Para obter um exemplo funcional, consulte [acessando a funcionalidade SQLXML no ambiente .net](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/accessing-sqlxml-functionality-in-the-net-environment.md).  
  
 O objeto SqlXmlAdapter dá suporte a esses métodos:  
  
 void Fill (DataSet DS)  
 Preenche o conjunto de dados no .NET Framework com os dados XML recuperados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 anular atualização (DataSet DS)  
 Aplica atualizações a registros no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a partir dos dados do conjunto de dados.  
  
 O objeto SqlXmlAdapter dá suporte a esses construtores:  
  
```  
public SqlXmlAdapter(SqlXmlCommand  cmd)   
  
public SqlXmlAdapter(  
                     string commandText,   
                     SqlXmlCommandType cmdType,   
                     string connectionString  
                      )   
  
public SqlXmlAdapter(  
                     Stream commandStream,   
                     SqlXmlCommandType cmdType,   
                     string connectionString  
                     )   
```  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto SqlXmlCommand &#40;classes gerenciadas SQLXML&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmlcommand-object.md)   
 [Objeto SqlXmlParameter &#40;classes gerenciadas SQLXML&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/net-framework-classes/sqlxml-managed-classes-sqlxmlparameter-object.md)  
  
  
