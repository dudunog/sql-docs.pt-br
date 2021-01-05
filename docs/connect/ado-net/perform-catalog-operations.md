---
title: Executar de operações de catálogo
description: Descreve como executar comandos que modificam o esquema de banco de dados.
ms.date: 11/25/2020
dev_langs:
- csharp
ms.assetid: e60f542f-6271-495b-a9e4-48553481c2a3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 79eef694b3c6294eb12630f27c4b3688823581c7
ms.sourcegitcommit: c938c12cf157962a5541347fcfae57588b90d929
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2020
ms.locfileid: "97771528"
---
# <a name="performing-catalog-operations"></a>Executar de operações de catálogo

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Para executar um comando a fim de modificar um banco de dados ou catálogo, como a instrução CREATE TABLE ou CREATE PROCEDURE, crie um objeto **Command** usando as instruções SQL apropriadas e um objeto **Connection**. Execute o comando com o método <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> do objeto <xref:Microsoft.Data.SqlClient.SqlCommand>.

## <a name="example"></a>Exemplo

O exemplo de código a seguir cria um procedimento armazenado em um banco de dados do Microsoft SQL Server.

[!code-csharp[DataWorks SqlCommand.ExecuteNonQuery#3](~/../sqlclient/doc/samples/SqlCommand_ExecuteNonQuery_SP_DML.cs#3)]

## <a name="see-also"></a>Confira também

- [Usar comandos para modificar dados](use-commands-to-modify-data.md)
- [Comandos e parâmetros](commands-parameters.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
