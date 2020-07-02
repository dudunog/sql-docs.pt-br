---
title: Usando System. Transactions | Microsoft Docs
description: O namespace System. Transactions fornece uma estrutura de transação totalmente integrada ao ADO.NET e SQL Server integração CLR.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- TransactionScope class
- Dispose method
- System.Transactions namespace
ms.assetid: 79656ce5-ce46-4c5e-9540-cf9869bd774b
author: rothja
ms.author: jroth
ms.openlocfilehash: 1fed4e8106fc5348c94a3c7afda0ec903f570eff
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765365"
---
# <a name="using-systemtransactions"></a>Usando System.Transactions
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  O **System.Transactions** fornece uma estrutura de transação que é totalmente integrada com o ADO.NET e a integração CLR (Common Language Runtime) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Uma classe **System.Transactions.TransactionScope** torna um bloco de código transacional inscrevendo implicitamente conexões em uma transação distribuída. Chame o método **Complete** no final do bloco de código marcado pelo **TransactionScope**. O método **Dispose** será invocado quando a execução do programa deixar um bloco de código, fazendo a transação ser descontinuada se o método **Complete** não for chamado. Se tiver sido lançada uma exceção que faz o código deixar o escopo, a transação será considerada descontinuada.  
  
 É recomendável utilizar um bloco **using** para assegurar que o método **Dispose** seja chamado no objeto **TransactionScope** ao sair do bloco **using** . Uma falha ao confirmar ou reverter transações pendentes pode diminuir muito o desempenho, pois o tempo limite padrão para o **TransactionScope** é de um minuto. Se você não usar uma instrução **using** , deverá executar todo o trabalho em um bloco **Try** e chamar explicitamente o método **Dispose** no bloco **Finally** .  
  
 Se ocorrer uma exceção no **TransactionScope**, a transação será marcada como inconsistente e abandonada. Ela será revertida quando o **TransactionScope** for descartado. Se nenhuma exceção ocorrer, as transações participantes serão confirmadas.  
  
 **TransactionScope** deve ser usado somente quando são acessados gerenciadores de recursos externos ou fontes de dados locais e remotas. Isso porque **TransactionScope** sempre causa a elevação de transações, mesmo que esteja sendo usado apenas em uma conexão de contexto.  
  
> [!NOTE]  
>  Por padrão, a classe **TransactionScope** cria uma transação com um **System.Transactions.Transaction.IsolationLevel** de **Serializable** . Dependendo do seu aplicativo, talvez você queira considerar abaixar o nível de isolamento para evitar uma contenção elevada em seu aplicativo.  
  
> [!NOTE]  
>  É recomendável executar apenas atualizações, inserções e exclusões em transações distribuídas em servidores remotos, pois isso consume recursos de banco de dados significativos. Caso a operação seja executada no servidor local, uma transação distribuída não será necessária e uma transação local será suficiente. Instruções SELECT podem bloquear recursos do banco de dados desnecessariamente e, em alguns cenários, pode ser necessário usar transações para seleções. Qualquer trabalho que não seja do banco de dados deve ser executado fora do escopo da transação, a menos que envolva outros gerenciadores de recursos transacionados. Apesar de uma exceção no escopo da transação evitar que a transação seja confirmada, a classe **TransactionScope** não tem provisão para reverter as alterações que seu código tenha feito fora do escopo da própria transação. Se precisar executar alguma ação ao reverter a ação, será necessário escrever sua própria implementação da interface **System.Transactions.IEnlistmentNotification** e inscrevê-la na transação explicitamente.  
  
## <a name="example"></a>Exemplo  
 Para trabalhar com **System.Transactions**, é necessário ter uma referência para o arquivo System.Transactions.dll.  
  
 O código a seguir demonstra como criar uma transação que pode ser elevada em duas instâncias diferentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essas instâncias são representadas por dois objetos **System.Data.SqlClient.SqlConnection** diferentes, que são quebrados em um bloco **TransactionScope** . O código cria o bloco **TransactionScope** com uma instrução **using** e abre a primeira conexão, que o inscreve automaticamente no **TransactionScope**. A transação é inscrita inicialmente como uma transação lightweight, não uma transação distribuída completa. O código presume a existência de uma lógica condicional (que foi omitida para ser breve). Ele abrirá a segunda conexão somente se for necessário, inscrevendo-o no **TransactionScope**. Quando a conexão é aberta, a transação é automaticamente elevada a uma transação distribuída completa. Então, o código invoca **TransactionScope.Complete**, que confirma a transação. O código dispõe das duas conexões ao sair das instruções **using** para as conexões. O método **TransactionScope.Dispose** para o **TransactionScope** é chamado automaticamente no encerramento do bloco **using** para o **TransactionScope**. Se uma exceção tiver sido lançada em qualquer ponto no bloco **TransactionScope** , **Complete** não será chamado e a transação distribuída será revertida quando o **TransactionScope** for descartado.  
  
 Visual Basic  
  
```  
Using transScope As New TransactionScope()  
    Using connection1 As New SqlConnection(connectString1)  
        ' Opening connection1 automatically enlists it in the   
        ' TransactionScope as a lightweight transaction.  
        connection1.Open()  
  
        ' Do work in the first connection.  
  
        ' Assumes conditional logic in place where the second  
        ' connection will only be opened as needed.  
        Using connection2 As New SqlConnection(connectString2)  
            ' Open the second connection, which enlists the   
            ' second connection and promotes the transaction to  
            ' a full distributed transaction.  
            connection2.Open()  
  
            ' Do work in the second connection.  
  
        End Using  
    End Using  
  
    ' Commit the transaction.  
    transScope.Complete()  
End Using  
```  
  
 C#  
  
```  
using (TransactionScope transScope = new TransactionScope())  
{  
    using (SqlConnection connection1 = new   
       SqlConnection(connectString1))  
    {  
        // Opening connection1 automatically enlists it in the   
        // TransactionScope as a lightweight transaction.  
        connection1.Open();  
  
        // Do work in the first connection.  
  
        // Assumes conditional logic in place where the second  
        // connection will only be opened as needed.  
        using (SqlConnection connection2 = new   
            SqlConnection(connectString2))  
        {  
            // Open the second connection, which enlists the   
            // second connection and promotes the transaction to  
            // a full distributed transaction.   
            connection2.Open();  
  
            // Do work in the second connection.  
        }  
    }  
    //  The Complete method commits the transaction.  
    transScope.Complete();  
}  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Integração CLR e transações](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
