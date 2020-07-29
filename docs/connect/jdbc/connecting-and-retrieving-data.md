---
title: Conectando e recuperando dados
description: Saiba como se conectar a um banco de dados SQL e recuperar dados usando o Microsoft JDBC Driver for SQL Server e estes exemplos de código.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ce43cc20-46a3-42ff-a3fb-75ad1ed10e08
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 92565d42605b67f61d3ab5e3842e3fb9f110b626
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86922882"
---
# <a name="connecting-and-retrieving-data"></a>Conectando e recuperando dados

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Quando você trabalha com o [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], há dois métodos principais para estabelecer uma conexão com um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um é definir as propriedades de conexão na URL de conexão e, em seguida, chamar o método getConnection da classe DriverManager para retornar um objeto [SQLServerConnection](reference/sqlserverconnection-class.md).

> [!NOTE]
> Para obter uma lista das propriedades de conexão compatíveis com o driver JDBC, confira [Configuração das propriedades de conexão](setting-the-connection-properties.md).

O segundo método envolve definir as propriedades de conexão usando métodos setter da classe [SQLServerDataSource](reference/sqlserverdatasource-class.md) e, em seguida, chamar o método [getConnection](reference/getconnection-method-sqlserverdatasource.md) para retornar um objeto SQLServerConnection.

Os tópicos nesta seção descrevem os modos diferentes nos quais você pode se conectar a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e também demonstram técnicas diferentes para recuperar dados.

## <a name="in-this-section"></a>Nesta seção

| Tópico                                             | Descrição                                                                                                                                                   |
| ------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Exemplo de URL de conexão](connection-url-sample.md) | Descreve como usar uma URL de conexão para se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e usar uma instrução SQL para recuperar dados. |
| [Exemplo de fonte de dados](data-source-sample.md)       | Descreve como usar uma fonte de dados para se conectar ao SQL Server e, em seguida, usar um procedimento armazenado para recuperar dados.                                                 |

## <a name="see-also"></a>Confira também

[Aplicativos de exemplo do JDBC Driver](sample-jdbc-driver-applications.md)
