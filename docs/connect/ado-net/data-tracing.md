---
title: Rastreamento de dados no SqlClient
description: Descreve como o Provedor de Dados do Microsoft SqlClient para o SQL Server fornece a funcionalidade interna de rastreamento de dados.
ms.date: 12/04/2020
ms.assetid: a6a752a5-d2a9-4335-a382-b58690ccb79f
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: fc8b5a7ca06af3c3e3ea83fcb747f79517e5ef7a
ms.sourcegitcommit: 4419e99d77ee2c73f9da1559c7944f7702f2de30
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/23/2020
ms.locfileid: "97744339"
---
# <a name="data-tracing-in-sqlclient"></a>Rastreamento de dados no SqlClient

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

O .NET apresenta a funcionalidade de rastreamento de dados interna, que é compatível com o Provedor de Dados do Microsoft SqlClient para o SQL Server e os protocolos de rede do SQL Server.

O rastreamento de chamadas à API de acesso a dados pode ajudar a diagnosticar os seguintes problemas:

- Incompatibilidade de esquema entre o programa cliente e o banco de dados.

- Problemas de biblioteca de rede ou de indisponibilidade de banco de dados.

- SQL incorreto, seja embutido em código ou gerado por um aplicativo.

- Lógica de programação incorreta.

- Problemas resultantes da interação entre o Provedor de Dados do Microsoft SqlClient para o SQL Server e componentes próprios.

Para dar suporte a diferentes tecnologias de rastreamento, o rastreamento é extensível. Portanto, um desenvolvedor pode rastrear um problema em qualquer nível da pilha de aplicativos. O Provedor de Dados do Microsoft SqlClient para o SQL Server aproveita as APIs generalizadas de rastreamento e instrumentação.

Para obter mais informações sobre como definir e configurar o rastreamento gerenciado no .NET, confira [Rastreamento de acesso a dados](/previous-versions/sql/sql-server-2012/hh880086(v=msdn.10)).

## <a name="access-diagnostic-information-in-the-extended-events-log"></a>Acessar informações de diagnóstico no log de eventos estendidos

No Provedor de Dados do Microsoft SqlClient para o SQL Server, o [Rastreamento de Acesso a Dados](/previous-versions/sql/sql-server-2012/hh880086(v=msdn.10)) facilita a correlação de eventos do cliente com informações de diagnóstico, como falhas de conexão, do buffer de anéis de conectividade do servidor e das informações de desempenho do aplicativo no log de eventos estendidos. Para obter mais informações sobre como ler o log de eventos estendidos, consulte [View Event Session Data](/previous-versions/sql/sql-server-2012/hh710068(v=sql.110)).

Para operações de conexão, o Provedor de Dados do Microsoft SqlClient para o SQL Server enviará uma ID de conexão do cliente. Se houver falha na conexão, você poderá acessar o buffer de anéis de conectividade ([Solução de problemas de conectividade no SQL Server 2008 com o buffer de anéis de conectividade](/archive/blogs/sql_protocols/connectivity-troubleshooting-in-sql-server-2008-with-the-connectivity-ring-buffer)), localizar o campo `ClientConnectionID` e obter informações de diagnóstico sobre a falha na conexão. As IDs de conexão de cliente estarão registradas no buffer de anéis se um erro ocorrer. Se uma conexão falhar antes do envio do pacote anterior ao logon, uma ID de conexão de cliente não será gerada. A ID de conexão de cliente é um GUID de 16 bytes. Você também poderá encontrar a ID de conexão do cliente na saída de destino dos eventos estendidos se a ação `client_connection_id` for adicionada aos eventos em uma sessão de eventos estendidos. Você pode habilitar o rastreamento de acesso a dados e executar novamente o comando de conexão, além de observar o campo `ClientConnectionID` no rastreamento de acesso a dados, caso precise obter assistência adicional com o diagnóstico de driver do cliente.

Você pode obter a ID de conexão do cliente de modo programático usando a propriedade `SqlConnection.ClientConnectionID`.

> [!NOTE]
> O Provedor de Dados do Microsoft SqlClient para o SQL Server dá suporte à ID de processo do servidor desde a versão 2.1.0. Você pode obtê-la de modo programático usando a propriedade `SqlConnection.ServerProcessId`.

As `ClientConnectionID` e `ServerProcessId` estão disponíveis para um objeto <xref:Microsoft.Data.SqlClient.SqlConnection> que estabelece com êxito uma conexão. Se uma tentativa de conexão falhar, a `ClientConnectionID` poderá estar disponível por meio de `SqlException.ToString`.

O Provedor de Dados do Microsoft SqlClient para o SQL Server também envia uma ID de atividade específica do thread. A ID de atividade é capturada nas sessões de eventos estendidas se as sessões são iniciadas com a opção de TRACK_CAUSALITY habilitada. Para problemas de desempenho com uma conexão ativa, você poderá obter a ID de atividade do rastreamento de acesso a dados do cliente (campo `ActivityID`) e, em seguida, localizar a ID de atividade nas saídas dos eventos estendidos. A ID de atividade nos eventos estendidos é um GUID de 16 bytes (não é o mesmo que o GUID da ID de conexão do cliente) com o acréscimo de um número de sequência de 4 bytes. O número de sequência representa a ordem de uma solicitação dentro de um thread e indica a ordenação relativa de lote e as instruções RPC para o thread. No momento, a `ActivityID` é enviada opcionalmente para instruções em lote do SQL e solicitações do RPC quando o rastreamento de acesso a dados está habilitado e o 18º bit na palavra de configuração de rastreamento de acesso a dados está ativado (ON).

A instrução SQL a seguir é um exemplo que usa o Transact-SQL para iniciar uma sessão de eventos estendidos que será armazenada em um buffer de anéis e gravará a ID de atividade enviada de um cliente no RPC e de operações de lote.

```sql
create event session MySession on server
add event connectivity_ring_buffer_recorded,
add event sql_statement_starting (action (client_connection_id)),
add event sql_statement_completed (action (client_connection_id)),
add event rpc_starting (action (client_connection_id)),
add event rpc_completed (action (client_connection_id))
add target ring_buffer with (track_causality=on)
```

## <a name="see-also"></a>Confira também
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
