---
title: Integração de System.Transactions com SQL Server
description: Descreve a integração de System.Transactions ao SQL Server para trabalhar com transações distribuídas.
ms.date: 11/25/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: af0ba2865719a5388314a4ca695e09191cb56173
ms.sourcegitcommit: 2add15a99df7b85d271adb261523689984dfd134
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97051242"
---
# <a name="systemtransactions-integration-with-sql-server"></a>Integração de System.Transactions com SQL Server

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

O .NET inclui uma estrutura de transação que pode ser acessada por meio do namespace <xref:System.Transactions>. Essa estrutura expõe transações de uma forma totalmente integrada no .NET, incluindo o ADO.NET.  
  
Além dos aprimoramentos de programação, o <xref:System.Transactions> e o ADO.NET podem trabalhar em conjunto para coordenar otimizações quando você trabalha com transações. Uma transação passível de promoção é uma transação leve (local) que pode ser promovida automaticamente a uma transação totalmente distribuída, conforme necessário.

O Provedor de Dados Microsoft SqlClient para SQL Server dá suporte a transações passíveis de promoção quando você trabalha com o SQL Server. Uma transação passível de promoção não chama a sobrecarga adicional de uma transação distribuída a menos que a sobrecarga adicional seja necessária. As transações passíveis de promoção são automáticas e não exigem nenhuma intervenção do desenvolvedor.

## <a name="creating-promotable-transactions"></a>Como criar transações passíveis de promoção

O Provedor de Dados Microsoft SqlClient para SQL Server fornece suporte para transações passíveis de promoção, que são tratadas por meio das classes no namespace <xref:System.Transactions>. As transações passíveis de promoção otimizam as transações distribuídas por meio da criação de uma transação distribuída até que seja necessária. Se apenas um gerenciador de recursos for necessário, não ocorrerá nenhuma transação distribuída.

> [!NOTE]
> Em um cenário parcialmente confiável, a <xref:System.Transactions.DistributedTransactionPermission> é necessária quando uma transação é promovida para uma transação distribuída.

## <a name="promotable-transaction-scenarios"></a>Cenários de transações passíveis de promoção

As transações distribuídas normalmente consomem recursos significativos do sistema, sendo gerenciadas pelo MS DTC (Coordenador de Transações Distribuídas da Microsoft), que integra todos os gerenciadores de recursos acessados na transação. Uma transação passível de promoção é uma forma especial de uma transação <xref:System.Transactions> que delega efetivamente o trabalho para uma simples transação do SQL Server. O <xref:System.Transactions>, o <xref:Microsoft.Data.SqlClient> e o SQL Server coordenam o trabalho envolvido no tratamento da transação, promovendo-a para uma transação distribuída completa, conforme necessário.

A vantagem de usar transações passíveis de promoção é que, quando uma conexão é aberta com uma transação <xref:System.Transactions.TransactionScope> ativa e não há nenhuma outra conexão aberta, a transação é confirmada como uma transação leve, em vez de gerar a sobrecarga adicional de uma transação distribuída completa.

### <a name="connection-string-keywords"></a>Palavras-chave de cadeia de conexão

A propriedade <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A> dá suporte a uma palavra-chave, `Enlist`, que indica se <xref:Microsoft.Data.SqlClient> detectará contextos transacionais e inscreverá automaticamente a conexão em uma transação distribuída. Se `Enlist=true`, a conexão será inscrita automaticamente no contexto de transação atual do thread de abertura. Se `Enlist=false`, a conexão `SqlClient` não interagirá com uma transação distribuída. O valor padrão de `Enlist` é true. Se `Enlist` não estiver especificado na cadeia de conexão, a conexão será inscrita automaticamente em uma transação distribuída, caso uma seja detectada no momento em que a conexão é aberta.

As palavras-chave `Transaction Binding` em uma cadeia de conexão <xref:Microsoft.Data.SqlClient.SqlConnection> controlam a associação da conexão com uma transação `System.Transactions` inscrita. Ela também está disponível por meio da propriedade <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder.TransactionBinding%2A> de um <xref:Microsoft.Data.SqlClient.SqlConnectionStringBuilder>.

A tabela a seguir descreve os valores possíveis.
  
|Palavra-chave|Descrição|  
|-------------|-----------------|  
|Desassociação implícita|O padrão. A conexão é desanexada da transação quando ela é encerrada, voltando para o modo de confirmação automática.|
|Desassociação explícita|A conexão permanece anexada à transação até que a transação seja fechada. A conexão falhará se a transação associada não estiver ativa ou não corresponder a <xref:System.Transactions.Transaction.Current%2A>.|

## <a name="using-transactionscope"></a>Como usar TransactionScope

Uma classe <xref:System.Transactions.TransactionScope> torna um bloco de código transacional inscrevendo implicitamente conexões em uma transação distribuída. Você precisará chamar o método <xref:System.Transactions.TransactionScope.Complete%2A> no final do bloco <xref:System.Transactions.TransactionScope> antes de deixá-lo. Deixar o bloco invoca o método <xref:System.Transactions.TransactionScope.Dispose%2A>. Se tiver sido gerada uma exceção que faz o código deixar o escopo, a transação será considerada anulada.

Recomendamos que você use um bloco `using` para garantir que <xref:System.Transactions.TransactionScope.Dispose%2A> seja chamado no objeto <xref:System.Transactions.TransactionScope> quando o bloco using for encerrado. Uma falha ao confirmar ou reverter transações pendentes pode diminuir muito o desempenho, pois o tempo limite padrão para o <xref:System.Transactions.TransactionScope> é de um minuto. Se você não usar uma instrução `using`, deverá executar todo o trabalho em um bloco `Try` e chamar explicitamente o método <xref:System.Transactions.TransactionScope.Dispose%2A> no bloco `Finally`.

Se ocorrer uma exceção no <xref:System.Transactions.TransactionScope>, a transação será marcada como inconsistente e abandonada. Ela será revertida quando o <xref:System.Transactions.TransactionScope> for descartado. Se nenhuma exceção ocorrer, as transações participantes serão confirmadas.

> [!NOTE]
> Por padrão, a classe `TransactionScope` cria uma transação com um <xref:System.Transactions.Transaction.IsolationLevel%2A> de `Serializable`. Dependendo do seu aplicativo, talvez você queira considerar abaixar o nível de isolamento para evitar uma contenção elevada em seu aplicativo.

> [!NOTE]
> Recomendamos executar apenas atualizações, inserções e exclusões em transações distribuídas, pois elas consomem recursos de banco de dados significativos. As instruções SELECT poderão bloquear recursos do banco de dados desnecessariamente e, em alguns cenários, você poderá precisar usar transações para seleções. Qualquer trabalho que não seja do banco de dados deve ser executado fora do escopo da transação, a menos que envolva outros gerenciadores de recursos transacionados.
Apesar de uma exceção no escopo da transação evitar que a transação seja confirmada, a classe <xref:System.Transactions.TransactionScope> não tem provisão para reverter as alterações que o código tenha feito fora do escopo da própria transação. Se você precisar executar alguma ação ao reverter a ação, escreva sua implementação da interface <xref:System.Transactions.IEnlistmentNotification> e inscreva-se na transação explicitamente.

## <a name="example"></a>Exemplo

O uso de <xref:System.Transactions> exige que você tenha uma referência a System.Transactions.dll.

A função a seguir demonstra como criar uma transação passível de promoção em duas instâncias diferentes do SQL Server, representadas por dois objetos <xref:Microsoft.Data.SqlClient.SqlConnection> diferentes, que são encapsulados em um bloco <xref:System.Transactions.TransactionScope>.

O código abaixo cria o bloco <xref:System.Transactions.TransactionScope> com uma instrução `using` e abre a primeira conexão, que o inscreve automaticamente no <xref:System.Transactions.TransactionScope>.

A transação é inscrita inicialmente como uma transação lightweight, não uma transação distribuída completa. A segunda conexão será inscrita no <xref:System.Transactions.TransactionScope> somente se o comando na primeira conexão não gerar uma exceção. Quando a segunda conexão é aberta, a transação é automaticamente promovida para uma transação distribuída completa.

Posteriormente, o método <xref:System.Transactions.TransactionScope.Complete%2A> é invocado, o que confirma a transação somente se nenhuma exceção é gerada. Se uma exceção for gerada em algum ponto no bloco <xref:System.Transactions.TransactionScope>, `Complete` não será chamado, e a transação distribuída será revertida quando o <xref:System.Transactions.TransactionScope> for descartado no final do bloco `using`.

[!code-csharp[SqlTransactionScope#1](~/../sqlclient/doc/samples/SqlTransactionScope.cs#1)]

## <a name="see-also"></a>Confira também

- [Transações e simultaneidade](transactions-and-concurrency.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
