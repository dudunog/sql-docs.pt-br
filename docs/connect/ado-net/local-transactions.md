---
title: Transações locais
description: Demonstra como executar transações em um banco de dados com o Provedor de Dados Microsoft SqlClient para SQL Server.
ms.date: 11/24/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: a310ab409c2300eb31d1e3c0e58b7ebe32096bfd
ms.sourcegitcommit: 2add15a99df7b85d271adb261523689984dfd134
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97051239"
---
# <a name="local-transactions"></a>Transações locais

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

As transações do ADO.NET são usadas quando você deseja associar várias tarefas para que elas sejam executadas como uma só unidade de trabalho. Por exemplo, imagine que um aplicativo executa duas tarefas. Primeiro, ele atualiza uma tabela com informações sobre pedidos. Em seguida, ele atualiza uma tabela que contém informações de inventário, debitando os itens pedidos. Se uma das tarefas falhar, as duas atualizações serão revertidas.  

## <a name="determining-the-transaction-type"></a>Como determinar o tipo de transação

Uma transação é considerada local quando é monofásica e é tratada diretamente pelo banco de dados. Uma transação é considerada distribuída quando é coordenada por um monitor de transação e usa mecanismos à prova de falhas (como o protocolo 2PC) na resolução das transações.

O Provedor de Dados Microsoft SqlClient para SQL Server tem seu objeto <xref:Microsoft.Data.SqlClient.SqlTransaction> para executar transações locais em bancos de dados do SQL Server. Outros provedores de dados .NET também fornecem os objetos `Transaction`. Além disso, há uma classe <xref:System.Data.Common.DbTransaction> que está disponível para a criação de um código independente de provedor que exige transações.

> [!NOTE]
> As transações são mais eficientes quando são executadas no servidor. Se você estiver trabalhando com um banco de dados do SQL Server que faz uso extensivo de transações explícitas, considere criá-las como procedimentos armazenados usando a instrução Transact-SQL BEGIN TRANSACTION.

## <a name="performing-a-transaction-using-a-single-connection"></a>Como executar uma transação usando uma só conexão 

No ADO.NET, você controla as transações com o objeto `Connection`. É possível iniciar uma transação local com o método `BeginTransaction`. Depois de iniciar uma transação, você pode inscrever um comando nessa transação com a propriedade `Transaction` de um objeto `Command`. Em seguida, você poderá confirmar ou reverter todas as modificações feitas na fonte de dados com base no êxito ou na falha dos componentes de transação.

> [!NOTE]
> O método `EnlistDistributedTransaction` não deve ser usado para uma transação local.

O escopo da transação é limitado à conexão. O exemplo a seguir executa uma transação explícita que consiste em dois comandos separados no bloco `try`. Os comandos executam as instruções INSERT na tabela `Production.ScrapReason` do banco de dados de exemplo AdventureWorks do SQL Server, as quais são confirmadas se nenhuma exceção é gerada. O código no bloco `catch` reverterá a transação se uma exceção for lançada. Se a transação for anulada ou a conexão for fechada antes de a transação ser concluída, a transação será automaticamente revertida.

## <a name="example"></a>Exemplo  

 Siga estas etapas para executar uma transação.

1. Chame o método <xref:Microsoft.Data.SqlClient.SqlConnection.BeginTransaction%2A> do objeto <xref:Microsoft.Data.SqlClient.SqlConnection> para marcar o início da transação. O método <xref:Microsoft.Data.SqlClient.SqlConnection.BeginTransaction%2A> retorna uma referência à transação. Essa referência é atribuída aos objetos <xref:Microsoft.Data.SqlClient.SqlCommand> inscritos na transação.

2. Atribua o objeto `Transaction` à propriedade <xref:Microsoft.Data.SqlClient.SqlCommand.Transaction%2A> de <xref:Microsoft.Data.SqlClient.SqlCommand> a ser executado. Se um comando for executado em uma conexão com uma transação ativa, e o objeto `Transaction` não tiver sido atribuído à propriedade `Transaction` do objeto `Command`, uma exceção será gerada.

3. Execute os comandos necessários.

4. Chame o método <xref:Microsoft.Data.SqlClient.SqlTransaction.Commit%2A> do objeto <xref:Microsoft.Data.SqlClient.SqlTransaction> para concluir a transação, ou chame o método <xref:Microsoft.Data.SqlClient.SqlTransaction.Rollback%2A> para finalizar a transação. Se a conexão for fechada ou descartada antes do método <xref:Microsoft.Data.SqlClient.SqlTransaction.Commit%2A> ou <xref:Microsoft.Data.SqlClient.SqlTransaction.Rollback%2A> ser executado, a transação será revertida.

O exemplo de código a seguir demonstra a lógica transacional usando o Provedor de Dados Microsoft SqlClient para SQL Server.  

[!code-csharp[SqlTransactionLocal#1](~/../sqlclient/doc/samples/SqlTransactionLocal.cs#1)]

## <a name="see-also"></a>Confira também

- [Transações e simultaneidade](transactions-and-concurrency.md)
- [Transações distribuídas](distributed-transactions.md)
- [Integração de System.Transactions com SQL Server](system-transactions-integration-with-sql-server.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
