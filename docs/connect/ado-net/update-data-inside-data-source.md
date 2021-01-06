---
title: Atualizar dados em uma fonte de dados
description: Descreve como executar comandos ou procedimentos armazenados que modificam dados em um banco de dados.
ms.date: 11/25/2020
dev_langs:
- csharp
ms.assetid: 55c545e5-dcd5-4323-a5b9-3825c2157462
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: aca7b1adb8ce91a12832bccfd6cbd27b07229d22
ms.sourcegitcommit: c938c12cf157962a5541347fcfae57588b90d929
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2020
ms.locfileid: "97771475"
---
# <a name="updating-data-in-a-data-source"></a>Atualizar dados em uma fonte de dados

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

As instruções SQL que modificam dados (como UPDATE, INSERT ou DELETE) não retornam linhas. Da mesma forma, muitos procedimentos armazenados executam uma ação, mas não retornam linhas. Para executar comandos que não retornam linhas, crie um objeto **Command** com o comando SQL apropriado e um **Connection**, incluindo os **Parâmetros** necessários. Execute o comando com o método <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQuery%2A> do objeto <xref:Microsoft.Data.SqlClient.SqlCommand>.

> [!NOTE]
> O método **ExecuteNonQuery** retorna um número inteiro que representa o número de linhas afetadas pela instrução ou pelo procedimento armazenado que foi executado. Se várias instruções tiverem sido executadas, o valor retornado é a soma dos registros afetados por todas as instruções executadas.

## <a name="example"></a>Exemplo

O exemplo de código a seguir executa uma instrução INSERT para inserir um registro em um banco de dados usando **ExecuteNonQuery**.
  
[!code-csharp[DataWorks SqlCommand.ExecuteNonQuery#1](~/../sqlclient/doc/samples/SqlCommand_ExecuteNonQuery_SP_DML.cs#1)]

O exemplo de código a seguir executa o procedimento armazenado criado pelo exemplo de código em [Executar operações de catálogo](perform-catalog-operations.md). Nenhuma linha é retornada pelo procedimento armazenado, portanto, o método **ExecuteNonQuery** é usado, mas o procedimento armazenado recebe um parâmetro de entrada e retorna um parâmetro de saída e um valor.

[!code-csharp[DataWorks SqlCommand.ExecuteNonQuery#2](~/../sqlclient/doc/samples/SqlCommand_ExecuteNonQuery_SP_DML.cs#2)]

## <a name="see-also"></a>Confira também

- [Usar comandos para modificar dados](use-commands-to-modify-data.md)
- [Atualizar fontes de dados com DataAdapters](update-data-sources-with-dataadapters.md)
- [Comandos e parâmetros](commands-parameters.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
