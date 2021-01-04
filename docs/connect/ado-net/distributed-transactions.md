---
title: Transações distribuídas
description: Descreve como executar transações distribuídas no ADO.NET
ms.date: 11/25/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 77ed8486f8b059f12fe7178826d81a743a97bbc4
ms.sourcegitcommit: 866554663ca3191748b6e4eb4d8d82fa58c4e426
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97559228"
---
# <a name="distributed-transactions"></a>Transações distribuídas

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Uma transação é um conjunto de tarefas relacionadas que é bem-sucedida (confirmação) ou falha (anulação) como uma unidade, entre outras coisas. Uma *transação distribuída* é uma transação que afeta vários recursos. Para que uma transação distribuída seja confirmada, todos os participantes devem garantir que qualquer alteração nos dados será permanente. As alterações devem persistir mesmo que haja falhas do sistema ou outros eventos imprevisíveis. Mesmo se um único participante não fizer essa garantia, a transação inteira falhará e todas as alterações aos dados dentro do escopo da transação serão revertidas. 

> [!NOTE]
> Uma exceção será gerada se você tentar confirmar ou reverter uma transação se um `DataReader` for iniciado enquanto a transação estiver ativa.

## <a name="working-with-systemtransactions"></a>Trabalhando com System.Transactions

No .NET, as transações distribuídas são gerenciadas por meio da API no namespace <xref:System.Transactions>. A API <xref:System.Transactions> delegará a manipulação da transação distribuída para um monitor de transação como o Coordenador de transações distribuídas da Microsoft (DTC) quando vários gerentes de recurso persistentes estão envolvidos. Para obter mais informações, confira os [Conceitos básicos da transação](/dotnet/framework/data/transactions/transaction-fundamentals).

O ADO.NET 2.0 introduziu o suporte para inscrição em uma transação distribuída usando o método `EnlistTransaction`, que inscreve uma conexão em uma instância <xref:System.Transactions.Transaction>. Em versões anteriores do ADO.NET, a inscrição explícita em transações distribuídas foi realizada usando o método `EnlistDistributedTransaction` de uma conexão para inscrever uma conexão em uma instância <xref:System.EnterpriseServices.ITransaction>, que não tem suporte para compatibilidade com versões anteriores. Para obter mais informações sobre as transações de serviços corporativos, confira [Interoperabilidade com os serviços corporativos e as transações COM+](/dotnet/framework/data/transactions/interoperability-with-enterprise-services-and-com-transactions).

Ao usar uma transação <xref:System.Transactions> com o Provedor de Dados Microsoft SqlClient para SQL Server em um banco de dados do SQL Server, um <xref:System.Transactions.Transaction> leve será usado automaticamente. A transação pode então ser promovida a uma transação distribuída completa conforme o necessário. Para obter mais informações, confira [Integração de System.Transactions ao SQL Server](system-transactions-integration-with-sql-server.md).

## <a name="automatically-enlisting-in-a-distributed-transaction"></a>Como se inscrever automaticamente em uma transação distribuída

A inscrição automática é a maneira padrão (e preferida) de integrar conexões ADO.NET com `System.Transactions`. Um objeto de conexão será inscrito automaticamente em uma transação distribuída existente se ele determinar que uma transação está ativa, o que, nos termos do `System.Transaction`, significa que `Transaction.Current` não é nulo. A inscrição automática de transação ocorre quando a conexão é aberta. Isso não ocorrerá depois disso, mesmo que um comando seja executado dentro de um escopo de transação. Você pode desabilitar a inscrição automática em transações existentes especificando `Enlist=false` como um parâmetro de cadeia de conexão para um <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=nameWithType>.

## <a name="manually-enlisting-in-a-distributed-transaction"></a>Como se inscrever manualmente em uma transação distribuída

Se a inscrição automática estiver desabilitada ou você precisar inscrever uma transação iniciada após a abertura da conexão, você poderá inscrevê-la em uma transação distribuída existente usando o método `EnlistTransaction` do objeto <xref:Microsoft.Data.SqlClient.SqlConnection> para o Provedor de Dados Microsoft SqlClient para SQL Server. A inscrição em uma transação atribuída existente garante que, se a transação for confirmada ou revertida, as alterações feitas pelo código na fonte de dados também serão confirmadas ou revertidas.

Inscrever-se em transações distribuídas é aplicável principalmente ao agrupar objetos de negócios. Se um objeto de negócios é agrupado com uma conexão aberta, a inscrição automática da transação ocorre somente quando essa conexão está aberta. Se várias transações são executadas usando o objeto comercial agrupado, a conexão aberta para esse objeto não se inscreverá automaticamente em transações iniciadas recentemente. Nesse caso, você pode desabilitar a inscrição automática de transação para a conexão e inscrever a conexão nas transações usando `EnlistTransaction`.

`EnlistTransaction` usa um só argumento do tipo <xref:System.Transactions.Transaction> que é uma referência para a transação existente. Após chamar o método `EnlistTransaction` da conexão, as modificações feitas na fonte de dados usando a conexão serão incluídas na transação. Passar um valor nulo cancela a inscrição da conexão de sua inscrição de transação distribuída atual. Observe que a conexão deve ser aberta antes de chamar `EnlistTransaction`.

> [!NOTE]
> Assim que uma conexão é inscrita explicitamente em uma transação, ela não pode ter a inscrição cancelada nem ser inscrita em outra transação até a primeira transação terminar.

> [!CAUTION]
> `EnlistTransaction` gera uma exceção se a conexão já tiver começado uma transação usando o método <xref:Microsoft.Data.SqlClient.SqlConnection.BeginTransaction%2A> da conexão. No entanto, se a transação for uma transação local iniciada na fonte de dados (por exemplo, executando a instrução BEGIN TRANSACTION explicitamente usando uma <xref:Microsoft.Data.SqlClient.SqlCommand>), o `EnlistTransaction` reverterá a transação local e se inscreverá na transação distribuída existente conforme o solicitado. Você não receberá o aviso de que a transação local foi revertida e deverá gerenciar as transações locais não iniciadas usando <xref:Microsoft.Data.SqlClient.SqlConnection.BeginTransaction%2A>. Se você estiver usando o Provedor de Dados Microsoft SqlClient para SQL Server com o SQL Server, uma tentativa de inscrição vai gerar uma exceção. Todos os outros casos permanecerão despercebidos.  

## <a name="promotable-transactions-in-sql-server"></a>Transações passíveis de promoção no SQL Server

O SQL Server oferece suporte a transações passíveis de promoção nas quais uma transação leve local pode ser automaticamente promovida para uma transação distribuída somente se isso for necessário. Uma transação passível de promoção não chama a sobrecarga adicional de uma transação distribuída a menos que a sobrecarga adicional seja necessária. Para obter mais informações e um exemplo de código, confira [Integração de System.Transactions ao SQL Server](system-transactions-integration-with-sql-server.md).

## <a name="configuring-distributed-transactions"></a>Configurando transações distribuídas

 Você talvez precise habilitar o MS DTC na rede para usar transações distribuídas. Se tiver o Firewall do Windows habilitado, você deverá permitir que o serviço do MS DTC use a rede ou abra a porta do MS DTC.  
  
## <a name="see-also"></a>Veja também

- [Transações e simultaneidade](transactions-and-concurrency.md)
- [Integração de System.Transactions com SQL Server](system-transactions-integration-with-sql-server.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
