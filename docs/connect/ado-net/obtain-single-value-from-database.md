---
title: Obter um único valor de um banco de dados
description: Saiba como retornar um único valor no ADO.NET. Esse exemplo de código retorna o valor da coluna de identidade para um registro inserido.
ms.date: 11/25/2020
dev_langs:
- csharp
ms.assetid: b38526cd-a62a-48cb-822a-e91dfa68e02d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 3937c1d4617f3cecb9012d82d590f75634ab1043
ms.sourcegitcommit: c938c12cf157962a5541347fcfae57588b90d929
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2020
ms.locfileid: "97771488"
---
# <a name="obtaining-a-single-value-from-a-database"></a>Obter um único valor de um banco de dados

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Talvez seja necessário retornar informações do banco de dados que sejam um único valor, não um formato de tabela ou fluxo de dados. Por exemplo, convém retornar o resultado de uma função de agregação, como COUNT(\*), SUM(Price) ou AVG(Quantity). O objeto **Command** fornece a capacidade de retornar valores únicos usando o método **ExecuteScalar**. O método **ExecuteScalar** retorna, como um valor escalar, o valor da primeira coluna da primeira linha do conjunto de resultados.

## <a name="example"></a>Exemplo

O exemplo de código a seguir insere um novo valor no banco de dados usando um <xref:Microsoft.Data.SqlClient.SqlCommand>. O método <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteScalar%2A> é usado para retornar o valor da coluna de identidade para o registro inserido.

[!code-csharp[DataWorks SqlCommand.ExecuteScalar#1](~/../sqlclient/doc/samples/SqlCommand_ExecuteScalar_Return_Id.cs#1)]

## <a name="see-also"></a>Confira também

- [Comandos e parâmetros](commands-parameters.md)
- [Executar um comando](execute-command.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
