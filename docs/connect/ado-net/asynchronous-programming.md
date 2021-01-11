---
title: Programação assíncrona
description: Saiba mais sobre a programação assíncrona no Provedor de Dados do Microsoft SqlClient para o SQL Server.
ms.date: 12/04/2020
ms.assetid: 85da7447-7125-426e-aa5f-438a290d1f77
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 6eec681974499219a1ca649f9a47449a27ff4002
ms.sourcegitcommit: 5b2c47ce88f7e56552fd415c32b319009d043b56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/29/2020
ms.locfileid: "97804301"
---
# <a name="asynchronous-programming"></a>Programação assíncrona

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Este tópico aborda o suporte à programação assíncrona no Provedor de Dados do Microsoft SqlClient para o SQL Server (SqlClient).

## <a name="legacy-asynchronous-programming"></a>Programação assíncrona herdada

O Provedor de Dados do Microsoft SqlClient para o SQL Server inclui métodos de **System.Data.SqlClient** para manter a compatibilidade com versões anteriores em aplicativos que migram para o <xref:Microsoft.Data.SqlClient>. Não é recomendável usar os seguintes métodos herdados de programação assíncrona para um novo desenvolvimento:

- <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteNonQuery%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteReader%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlCommand.BeginExecuteXmlReader%2A?displayProperty=nameWithType>

> [!TIP]
> No Provedor de Dados do Microsoft SqlClient para o SQL Server, esses métodos herdados não exigem mais `Asynchronous Processing=true` na cadeia de conexão.

## <a name="asynchronous-programming-features"></a>Recursos de programação assíncrona

Esses recursos de programação assíncrona fornecem uma técnica simples para tornar o código assíncrono.

Para obter mais informações sobre a programação assíncrona no .NET, confira:

- [Programação assíncrona em C#](/dotnet/csharp/async)

- [Programação assíncrona com Async e Await (Visual Basic)](/dotnet/visual-basic/programming-guide/concepts/async/index)

Quando sua interface de usuário não tem resposta ou o servidor não escala, é provável que você precise que seu código seja mais assíncrono. Escrever código assíncrono tradicionalmente envolve instalar um retorno de chamada (também chamado de continuação) para expressar a lógica que ocorre depois que a operação assíncrona é concluída. Isso complica a estrutura de código assíncrona em comparação com o código síncrono.

Você pode chamar métodos assíncronos sem usar retornos de chamada e sem dividir o código em vários métodos ou expressões lambda.

O modificador `async` especifica que um método é assíncrono. Ao chamar um método `async`, uma tarefa é retornada. Quando o operador `await` é aplicado a uma tarefa, o método atual é encerrado imediatamente. Quando a tarefa é concluída, a execução é retomada no mesmo método.

> [!TIP]
> No Provedor de Dados do Microsoft SqlClient para o SQL Server, as chamadas assíncronas não são necessárias para definir a palavra-chave da cadeia de conexão `Context Connection`.

Chamar um método de `async` não atribui nenhum thread adicional. Ele pode usar o thread de E/S de conclusão existente brevemente na extremidade.

Os seguintes métodos do Provedor de Dados do Microsoft SqlClient para o SQL Server dão suporte à programação assíncrona:

- <xref:System.Data.Common.DbConnection.OpenAsync%2A?displayProperty=nameWithType>

- <xref:System.Data.Common.DbCommand.ExecuteDbDataReaderAsync%2A?displayProperty=nameWithType>

- <xref:System.Data.Common.DbCommand.ExecuteNonQueryAsync%2A?displayProperty=nameWithType>

- <xref:System.Data.Common.DbCommand.ExecuteReaderAsync%2A?displayProperty=nameWithType>

- <xref:System.Data.Common.DbCommand.ExecuteScalarAsync%2A?displayProperty=nameWithType>

- <xref:System.Data.Common.DbDataReader.GetFieldValueAsync%2A>

- <xref:System.Data.Common.DbDataReader.IsDBNullAsync%2A>

- <xref:System.Data.Common.DbDataReader.NextResultAsync%2A?displayProperty=nameWithType>

- <xref:System.Data.Common.DbDataReader.ReadAsync%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlConnection.OpenAsync%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteNonQueryAsync%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteReaderAsync%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteScalarAsync%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlCommand.ExecuteXmlReaderAsync%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlDataReader.NextResultAsync%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlDataReader.ReadAsync%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlBulkCopy.WriteToServerAsync%2A?displayProperty=nameWithType>

Outros membros assíncronos dão suporte ao [suporte a streaming do SqlClient](sqlclient-streaming-support.md).

> [!TIP]
> Os métodos assíncronos não exigem `Asynchronous Processing=true` na cadeia de conexão. Além disso, essa propriedade é obsoleta no Provedor de Dados do Microsoft SqlClient para o SQL Server.

### <a name="synchronous-to-asynchronous-connection-open"></a>Conexão síncrona para assíncrona aberta

Você pode atualizar um aplicativo existente para usar o recurso assíncrono. Por exemplo, suponha que um aplicativo tenha um algoritmo síncrono de conexão e bloqueie o thread de interface de usuário sempre que se conecta ao banco de dados e, uma vez conectado, o aplicativo chama um procedimento armazenado que sinaliza outros usuários da pessoa que acabou de se conectar.

[!code-csharp[SqlCommand_ExecuteNonQuery#1](~/../sqlclient/doc/samples/SqlCommand_ExecuteNonQuery.cs#1)]

Quando convertido para usar a funcionalidade assíncrona, o programa terá a seguinte aparência:

[!code-csharp[SqlCommand_ExecuteNonQueryAsync#1](~/../sqlclient/doc/samples/SqlCommand_ExecuteNonQueryAsync.cs#1)]

### <a name="add-the-asynchronous-feature-in-an-existing-application-mixing-old-and-new-patterns"></a>Adicionar o recurso assíncrono em um aplicativo existente (combinando padrões antigos e novos)

Também é possível adicionar a funcionalidade assíncrona (SqlConnection::OpenAsync) sem alterar a lógica assíncrona existente. Por exemplo, se um aplicativo no momento usa:

[!code-csharp[SqlConnection_OpenAsync_ContinueWith#1](~/../sqlclient/doc/samples/SqlConnection_OpenAsync_ContinueWith.cs#1)]

Você pode começar a usar o padrão assíncrono sem alterar substancialmente o algoritmo existente.

[!code-csharp[SqlConnection_OpenAsync_ContinueWith#2](~/../sqlclient/doc/samples/SqlConnection_OpenAsync_ContinueWith.cs#2)]

### <a name="use-the-base-provider-model-and-the-asynchronous-feature"></a>Usar o modelo de provedor base e o recurso assíncrono

Você pode precisar criar uma ferramenta que seja capaz de se conectar a bancos de dados diferentes e executar consultas. Use o modelo de provedor base e o recurso assíncrono.

O controlador MSDTC deve ser habilitado no servidor para usar transações distribuídas. Para obter informações sobre como habilitar o MSDTC, confira [Como habilitar o MSDTC em um servidor Web](/previous-versions/commerce-server/dd327979(v=cs.90)).

[!code-csharp[SqlClient_AsyncProgramming_ProviderModel#1](~/../sqlclient/doc/samples/SqlClient_AsyncProgramming_ProviderModel.cs#1)]

### <a name="use-sql-transactions-and-the-new-asynchronous-feature"></a>Usar transações SQL e o novo recurso assíncrono

[!code-csharp[SqlClient_AsyncProgramming_SqlTransaction#1](~/../sqlclient/doc/samples/SqlClient_AsyncProgramming_SqlTransaction.cs#1)]

### <a name="use-distributed-transactions-and-the-new-asynchronous-feature"></a>Usar transações distribuídas e o novo recurso assíncrono

Em um aplicativo empresarial, talvez seja necessário adicionar **transações distribuídas** em alguns cenários, a fim de habilitar transações entre vários servidores de banco de dados. Você pode usar o namespace System.Transactions e inscrever uma transação distribuída, da seguinte maneira:

[!code-csharp[SqlClient_AsyncProgramming_DistributedTransaction#1](~/../sqlclient/doc/samples/SqlClient_AsyncProgramming_DistributedTransaction.cs#1)]

### <a name="cancel-an-asynchronous-operation"></a>Cancelar uma operação assíncrona

Você pode cancelar uma solicitação assíncrona usando o <xref:System.Threading.CancellationToken>.

[!code-csharp[SqlClient_AsyncProgramming_Cancellation#1](~/../sqlclient/doc/samples/SqlClient_AsyncProgramming_Cancellation.cs#1)]

### <a name="asynchronous-operations-with-sqlbulkcopy"></a>Operações assíncronas com SqlBulkCopy

As funcionalidades assíncronas também estão em <xref:Microsoft.Data.SqlClient.SqlBulkCopy?displayProperty=nameWithType> com <xref:Microsoft.Data.SqlClient.SqlBulkCopy.WriteToServerAsync%2A?displayProperty=nameWithType>.

[!code-csharp[SqlClient_AsyncProgramming_SqlBulkCopy#1](~/../sqlclient/doc/samples/SqlClient_AsyncProgramming_SqlBulkCopy.cs#1)]

## <a name="asynchronously-use-multiple-commands-with-mars"></a>Usar vários comandos de modo assíncrono com o MARS

O exemplo abre uma conexão com o banco de dados **AdventureWorks**. Usando um objeto <xref:Microsoft.Data.SqlClient.SqlCommand>, um <xref:Microsoft.Data.SqlClient.SqlDataReader> é criado. Conforme o leitor é usado, um segundo <xref:Microsoft.Data.SqlClient.SqlDataReader> é aberto, usando dados do primeiro <xref:Microsoft.Data.SqlClient.SqlDataReader> como entrada para a cláusula WHERE para o segundo leitor.

> [!NOTE]
> O exemplo a seguir usa o [banco de dados de exemplo **AdventureWorks**](../../samples/adventureworks-install-configure.md). A cadeia de conexão fornecida no código de exemplo pressupõe que o banco de dados está instalado e disponível no computador local. Modifique a cadeia de conexão conforme necessário para o seu ambiente.

[!code-csharp[SqlClient_AsyncProgramming_MultipleCommands#1](~/../sqlclient/doc/samples/SqlClient_AsyncProgramming_MultipleCommands.cs#1)]

## <a name="asynchronously-read-and-update-data-with-mars"></a>Ler e atualizar dados de modo assíncrono com o MARS

O MARS permite que uma conexão seja usada para operações de leitura e de DML (linguagem de manipulação de dados) com mais de uma operação pendente. Esse recurso elimina a necessidade de um aplicativo lidar com erros de conexão ocupada. Além disso, o MARS pode substituir o uso de cursores do servidor, que geralmente consomem mais recursos. Finalmente, como as várias operações podem funcionar em uma única conexão, elas podem compartilhar o mesmo contexto de transação, eliminando a necessidade de usar procedimentos armazenados do sistema **sp_getbindtoken** e **sp_bindsession**.

O aplicativo de console a seguir demonstra como usar dois objetos <xref:Microsoft.Data.SqlClient.SqlDataReader> com três objetos <xref:Microsoft.Data.SqlClient.SqlCommand> e um objeto <xref:Microsoft.Data.SqlClient.SqlConnection> com o MARS habilitado. O primeiro objeto de comando recupera uma lista de fornecedores cuja classificação de crédito é 5. O segundo objeto de comando usa a ID do fornecedor especificada de um <xref:Microsoft.Data.SqlClient.SqlDataReader> para carregar o segundo <xref:Microsoft.Data.SqlClient.SqlDataReader> com todos os produtos para o fornecedor específico. Cada registro de produto é visitado pelo segundo <xref:Microsoft.Data.SqlClient.SqlDataReader>. Um cálculo é executado para determinar o que o novo **OnOrderQty** deve ser. O terceiro objeto de comando é usado para atualizar a tabela **ProductVendor** com o novo valor. Todo esse processo ocorre em uma transação, que é revertida no final.

> [!NOTE]
> O exemplo a seguir usa o [banco de dados de exemplo **AdventureWorks**](../../samples/adventureworks-install-configure.md). A cadeia de conexão fornecida no código de exemplo pressupõe que o banco de dados está instalado e disponível no computador local. Modifique a cadeia de conexão conforme necessário para o seu ambiente.

[!code-csharp[SqlClient_AsyncProgramming_MultipleCommandsEx#1](~/../sqlclient/doc/samples/SqlClient_AsyncProgramming_MultipleCommandsEx.cs#1)]

## <a name="see-also"></a>Confira também

- [Recuperar e modificar dados no ADO.NET](retrieving-modifying-data.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
