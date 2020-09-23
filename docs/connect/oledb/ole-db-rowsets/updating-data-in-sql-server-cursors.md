---
title: Atualizar dados em cursores (Driver do OLE DB)
description: Saiba como um aplicativo de consumidor do Driver do OLE DB para SQL Server funciona com solicitações em um conjunto de linhas modificável usando cursores do SQL Server.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- isolation levels [SQL Server]
- delayed update mode [OLE DB]
- immediate update mode [OLE DB]
- cursors [OLE DB]
- data updates [SQL Server], OLE DB
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eae7b9119803615a2d18fe4710ff1eda2b91ac5b
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88859923"
---
# <a name="updating-data-in-sql-server-cursors"></a>Atualizando dados em cursores do SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Ao buscar e atualizar dados por meio de cursores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], um aplicativo de consumidor do Driver do OLE DB para SQL Server é limitado pelas mesmas considerações e restrições que se aplicam a qualquer outro aplicativo cliente.  
  
 Apenas as linhas em cursores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] participam do controle de acesso a dados simultâneo. Quando o consumidor solicita um conjunto de linhas modificável, o controle de simultaneidade é controlado por DBPROP_LOCKMODE. Para modificar o nível do controle de acesso simultâneo, o consumidor define a propriedade DBPROP_LOCKMODE antes de abrir o conjunto de linhas.  
  
 Os níveis de isolamento da transação podem gerar defasagens significativas no posicionamento de linhas, se o design do aplicativo cliente permitir que as transações permaneçam abertas por longos períodos. Por padrão, o OLE DB Driver for SQL Server usa o nível de isolamento de leitura confirmada especificado por DBPROPVAL_TI_READCOMMITTED. O Driver do OLE DB para SQL Server dá suporte ao isolamento de leitura suja quando a simultaneidade do conjunto de linhas é somente leitura. Assim, o consumidor pode solicitar um nível mais alto de isolamento em um conjunto de linhas modificável, mas não pode solicitar nenhum nível inferior com êxito.  
  
## <a name="immediate-and-delayed-update-modes"></a>Modos de atualização imediatos e atrasados  
 No modo de atualização imediato, cada chamada a **IRowsetChange::SetData** causa uma viagem de ida e volta ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se o consumidor fizer várias alterações em uma única linha, será mais eficiente enviar todas as alterações com uma única chamada de **SetData**.  
  
 No modo de atualização atrasada, uma viagem de ida e volta é feita ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para cada linha indicada nos parâmetros *cRows* e *rghRows* de **IRowsetUpdate::Update**.  
  
 Em qualquer modo, uma viagem de ida e volta representará uma transação distinta quando nenhum objeto de transação estiver aberto para o conjunto de linhas.  
  
 Ao usar **IRowsetUpdate::Update**, o Driver do OLE DB para SQL Server tenta processar cada linha indicada. Um erro que ocorre devido a valores de status, tamanho ou dados inválidos para qualquer linha não interrompe o processamento do OLE DB Driver for SQL Server. É possível modificar todas ou nenhuma das outras linhas que participam da atualização. O consumidor precisa examinar a matriz *prgRowStatus* retornada para determinar a falha de qualquer linha específica quando o OLE DB Driver for SQL Server retorna DB_S_ERRORSOCCURRED.  
  
 Um consumidor não deve presumir que as linhas são processadas em qualquer ordem específica. Se um consumidor solicitar o processamento ordenado da modificação de dados em mais de uma única linha, ele deverá estabelecer essa ordem na lógica do aplicativo e abrir uma transação para conter o processo.  
  
## <a name="see-also"></a>Consulte Também  
 [Atualizando dados em conjuntos de linhas](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
