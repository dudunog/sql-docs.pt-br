---
title: Recuperar informações de esquema de banco de dados
description: Saiba mais sobre como usar o Provedor de Dados Microsoft SqlClient para SQL Server a fim de recuperar informações de esquema de banco de dados.
ms.date: 11/26/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 932f4ff2109e3754fb97c79274a5ffb93b9494d3
ms.sourcegitcommit: 2add15a99df7b85d271adb261523689984dfd134
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97051246"
---
# <a name="retrieving-database-schema-information"></a>Recuperar informações de esquema de banco de dados

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

A obtenção de informações de esquema de um banco de dados é realizada com o processo de descoberta de esquema. A descoberta de esquema permite que os aplicativos solicitem que os provedores gerenciados localizem e retornem informações sobre o esquema de banco de dados, também conhecidas como *metadados*, de determinado banco de dados. Os diferentes elementos de esquema de banco de dados, como tabelas, colunas e procedimentos armazenados, são expostos por meio de coleções de esquema. Cada coleção de esquema contém uma variedade de informações de esquema específicas ao provedor em uso.

O Provedor de Dados Microsoft SqlClient para SQL Server implementa o método **GetSchema** na classe **SqlConnection**, e as informações de esquema que são retornadas do método **GetSchema** são fornecidas na forma de uma <xref:System.Data.DataTable>. O método **GetSchema** é um método sobrecarregado que fornece parâmetros opcionais para especificar a coleção de esquemas a ser retornada e restringir a quantidade de informações retornada. O provedor de dados do SqlClient também fornece um método **GetSchemaTable** que retorna uma DataTable que descreve os metadados de coluna de **SqlDataReader**.

## <a name="in-this-section"></a>Nesta seção

[As coleções de esquemas e GetSchema](getschema-and-schema-collections.md)  
Descreve o método **GetSchema** e como ele pode ser usado para recuperar e restringir informações de esquema de um banco de dados.

[Restrições de esquemas](schema-restrictions.md)  
Descreve as restrições de esquema que podem ser usadas com **GetSchema**. 

[Coleções de esquemas comuns](common-schema-collections.md)  
Descreve todas as coleções de esquemas comuns compatíveis com todos os provedores gerenciados do .NET.  
  
[Coleções de esquema do SQL Server](sql-server-schema-collections.md)  
Descreve as coleções de esquemas adicionais compatíveis com o Provedor de Dados Microsoft SqlClient para SQL Server. 

## <a name="reference"></a>Referência

<xref:System.Data.Common.DbConnection.GetSchema%2A>  
Descreve o método **GetSchema** da classe <xref:System.Data.Common.DbConnection>.

<xref:Microsoft.Data.SqlClient.SqlConnection.GetSchema%2A>  
Descreve o método **GetSchema** da classe <xref:Microsoft.Data.SqlClient.SqlConnection>.

<xref:System.Data.Common.DbDataReader.GetSchemaTable%2A>  
Descreve o método **GetSchemaTable** da classe <xref:System.Data.Common.DbDataReader>. 

<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>  
Descreve o método **GetSchemaTable** da classe <xref:Microsoft.Data.SqlClient.SqlDataReader>.

## <a name="see-also"></a>Confira também

- [Recuperar e modificar dados no ADO.NET](retrieving-modifying-data.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
