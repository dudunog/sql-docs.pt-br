---
title: Contadores de desempenho do SqlClient
description: Use os contadores de desempenho do Provedor de Dados do Microsoft SqlClient para o SQL Server a fim de monitorar o status do seu aplicativo e os respectivos recursos de conexão usando o Monitor de Desempenho do Windows ou de modo programático.
ms.date: 12/04/2020
dev_langs:
- csharp
ms.assetid: 0b121b71-78f8-4ae2-9aa1-0b2e15778e57
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: e9d8c2edb88a9ed50b47c761d3af8aec8016065a
ms.sourcegitcommit: 5b2c47ce88f7e56552fd415c32b319009d043b56
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/29/2020
ms.locfileid: "97804296"
---
# <a name="performance-counters-in-sqlclient"></a>Contadores de desempenho do SqlClient

[!INCLUDE[appliesto-netfx-xxxx-xxxx-md](../../includes/appliesto-netfx-xxxx-xxxx-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

Use os contadores de desempenho do <xref:Microsoft.Data.SqlClient> para monitorar o status do seu aplicativo e os recursos de conexão usados por ele. Os contadores de desempenho podem ser monitorados por meio do Monitor de Desempenho do Windows ou acessados de modo programático pela classe <xref:System.Diagnostics.PerformanceCounter> no namespace <xref:System.Diagnostics>.

## <a name="available-performance-counters"></a>Contadores de desempenho disponíveis

Atualmente, há 14 contadores de desempenho diferentes disponíveis para o <xref:Microsoft.Data.SqlClient>, conforme descrito na tabela a seguir.

|Contador de desempenho|Descrição|  
|-------------------------|-----------------|  
|`HardConnectsPerSecond`|O número de conexões por segundo que estão sendo feitas com um servidor de banco de dados.|  
|`HardDisconnectsPerSecond`|O número de desconexões por segundo que estão sendo feitas com um servidor de banco de dados.|  
|`NumberOfActiveConnectionPoolGroups`|O número de grupos de pools de conexão exclusivos que estão ativos. Esse contador é controlado pelo número de cadeias de conexão exclusivas encontradas no AppDomain.|  
|`NumberOfActiveConnectionPools`|O número total de pools de conexão.|  
|`NumberOfActiveConnections`|O número de conexões ativas que estão atualmente em uso. **Observação:**  esse contador de desempenho não está habilitado por padrão. Para habilitá-lo, confira [Ativar contadores desativados por padrão](#ActivatingOffByDefault).|  
|`NumberOfFreeConnections`|O número de conexões disponíveis para uso nos pools de conexão. **Observação:**  esse contador de desempenho não está habilitado por padrão. Para habilitá-lo, confira [Ativar contadores desativados por padrão](#ActivatingOffByDefault).|  
|`NumberOfInactiveConnectionPoolGroups`|O número de grupos de pools de conexão exclusivos que estão marcados para remoção. Esse contador é controlado pelo número de cadeias de conexão exclusivas encontradas no AppDomain.|  
|`NumberOfInactiveConnectionPools`|O número de pools de conexão inativos que não tiveram nenhuma atividade recente e que estão aguardando para serem descartados.|  
|`NumberOfNonPooledConnections`|O número de conexões ativas que não estão em pool.|  
|`NumberOfPooledConnections`|O número de conexões ativas que estão sendo gerenciadas pela infraestrutura de pooling de conexão.|  
|`NumberOfReclaimedConnections`|O número de conexões que foram recuperadas por meio da coleta de lixo, em que `Close` ou `Dispose` não foi chamado pelo aplicativo. **Observação** O não fechamento ou o não descarte explícitos das conexões afeta o desempenho.|  
|`NumberOfStasisConnections`|O número de conexões que estão aguardando a conclusão de uma ação e que, portanto, não estão disponíveis para uso pelo seu aplicativo.|  
|`SoftConnectsPerSecond`|O número de conexões ativas extraídas do pool de conexão. **Observação:**  esse contador de desempenho não está habilitado por padrão. Para habilitá-lo, confira [Ativar contadores desativados por padrão](#ActivatingOffByDefault).|  
|`SoftDisconnectsPerSecond`|O número de conexões ativas que estão sendo retornadas para o pool de conexão. **Observação:**  esse contador de desempenho não está habilitado por padrão. Para habilitá-lo, confira [Ativar contadores desativados por padrão](#ActivatingOffByDefault).|  

### <a name="connection-pool-groups-and-connection-pools"></a>Grupos de pools de conexão e pools de conexão

Ao usar a Autenticação do Windows (segurança integrada), você precisará monitorar os contadores de desempenho `NumberOfActiveConnectionPoolGroups` e `NumberOfActiveConnectionPools`. O motivo é que os grupos do pool de conexão são mapeados para cadeias de conexão exclusivas. Quando a segurança integrada é usada, os pools de conexão são mapeados para cadeias de conexão e criam pools separados para identidades individuais do Windows. Por exemplo, se Mateus e Marina, cada um dentro do mesmo AppDomain, usarem a cadeia de conexão `"Data Source=MySqlServer;Integrated Security=true"`, um grupo de pools de conexão será criado para a cadeia de conexão e dois pools adicionais serão criados, um para Mateus e outro para Marina. Se Pedro e Beatriz usarem uma cadeia de conexão com um logon idêntico do SQL Server, `"Data Source=MySqlServer;User Id=<myUserID>;Password=<myPassword>"`, apenas um pool será criado para a identidade **<myUserID>** .

<a name="ActivatingOffByDefault"></a>

### <a name="activate-off-by-default-counters"></a>Ativar contadores desativados por padrão

Os contadores de desempenho `NumberOfFreeConnections`, `NumberOfActiveConnections`, `SoftDisconnectsPerSecond` e `SoftConnectsPerSecond` estão desativados por padrão. Adicione as seguintes informações ao arquivo de configuração do aplicativo para habilitá-las:

```xml  
<system.diagnostics>  
  <switches>  
    <add name="ConnectionPoolPerformanceCounterDetail"  
         value="4"/>  
  </switches>  
</system.diagnostics>  
```  

## <a name="retrieve-performance-counter-values"></a>Recuperar valores de contador de desempenho

O aplicativo de console a seguir mostra como recuperar valores de contador de desempenho no seu aplicativo. As conexões precisam estar abertas e ativas de modo que as informações sejam retornadas para todos os contadores de desempenho do Provedor de Dados do Microsoft SqlClient para o SQL Server.

> [!NOTE]
> Este exemplo usa o [banco de dados de exemplo **AdventureWorks**](../../samples/adventureworks-install-configure.md). As cadeias de conexão fornecidas no código de exemplo pressupõem que o banco de dados esteja instalado e disponível no computador local e que você tenha criado logons que correspondam àqueles fornecidos nas cadeias de conexão. Talvez seja necessário habilitar os logons do SQL Server se o servidor está definido por meio das configurações de segurança padrão que permitem apenas a Autenticação do Windows. Modifique as cadeias de conexão, conforme necessário, de acordo com o seu ambiente.

### <a name="example"></a>Exemplo

[!code-csharp[SqlClient_PerformanceCounter#1](~/../sqlclient/doc/samples/SqlClient_PerformanceCounter.cs#1)]

## <a name="see-also"></a>Confira também

- [Conectar-se a fontes de dados](connecting-to-data-source.md)
- [Criação de perfil de runtime](/dotnet/framework/debug-trace-profile/runtime-profiling)
- [Introdução ao monitoramento de limites de desempenho](/previous-versions/visualstudio/visual-studio-2008/bd20x32d(v=vs.90))
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
