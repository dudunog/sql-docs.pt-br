---
title: ISSAsynchStatus::Abort (Driver do OLE DB) | Microsoft Docs
description: Saiba como o método ISSAsynchStatus::Abort cancela uma operação de execução assíncrona no Driver do OLE DB para SQL Server.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apiname:
- ISSAsynchStatus::Abort (OLE DB)
apitype: COM
helpviewer_keywords:
- Abort method
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cbbef11ae17029500a6910e5b28c121f6312dce2
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862201"
---
# <a name="issasynchstatusabort-ole-db"></a>ISSAsynchStatus::Abort (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Cancela uma operação que está sendo executada de forma assíncrona.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
HRESULT Abort(  
        HCHAPTER hChapter,  
        DBASYNCHOP eOperation);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hChapter*[in]  
 O identificador do capítulo que contém a operação a ser anulada. Se o objeto que está sendo chamado não for um objeto de conjunto de linhas ou se a operação não se aplicar a um capítulo, o chamador precisará definir *hChapter* como DB_NULL_HCHAPTER.  
  
 *eOperation*[in]  
 A operação a ser anulada. O seguinte valor deveria ser usado:  
  
 DBASYNCHOP_OPEN – a solicitação de cancelamento se aplica à abertura ou população assíncrona de um conjunto de linhas ou à inicialização assíncrona de um objeto de fonte de dados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 S_OK  
 A solicitação para cancelar a operação assíncrona foi processada. Isso não garante que a operação propriamente dita foi cancelada. Para determinar se a operação foi cancelada, o consumidor deve chamar [ISSAsynchStatus::GetStatus](../../oledb/ole-db-interfaces/issasynchstatus-getstatus-ole-db.md) e verificar DB_E_CANCELED; no entanto, esse valor pode não ser retornado na chamada seguinte.  
  
 DB_E_CANTCANCEL  
 A operação assíncrona não pode ser cancelada.  
  
 DB_E_CANCELED  
 A solicitação para anular a operação assíncrona foi cancelada durante notificações. A operação ainda está sendo executada de forma assíncrona.  
  
 E_FAIL  
 Ocorreu um erro específico de provedor.  
  
 E_INVALIDARG  
 O parâmetro *hChapter* não é DB_NULL_HCHAPTER ou *eOperation* não é DBASYNCH_OPEN.  
  
 E_UNEXPECTED  
 `ISSAsynchStatus::Abort` foi chamado em um objeto de fonte de dados no qual `IDBInitialize::Initialize` não foi chamado ou não foi concluído.  
  
 `ISSAsynchStatus::Abort` foi chamado em um objeto de fonte de dados no qual `IDBInitialize::Initialize` foi chamado, mas foi cancelado antes da inicialização ou atingiu o tempo limite. O objeto de fonte de dados permanece não inicializado.  
  
 `ISSAsynchStatus::Abort` foi chamado em um conjunto de linhas no qual `ITransaction::Commit` ou `ITransaction::Abort` foi chamado anteriormente, e o conjunto de linhas não sobreviveu à operação de confirmação ou anulação e está em um estado zumbi.  
  
 `ISSAsynchStatus::Abort` foi chamado em um conjunto de linhas cancelado de forma assíncrona em sua fase de inicialização. O conjunto de linhas está em um estado zumbi.  
  
## <a name="remarks"></a>Comentários  
 Anular a inicialização de um conjunto de linhas ou objeto de fonte de dados pode deixar o conjunto de linhas ou o objeto de fonte de dados em um estado zumbi, de modo que todos os métodos diferentes de `IUnknown` retornam E_UNEXPECTED. Quando isso acontece, a única ação possível para o consumidor é liberar o conjunto de linhas ou objeto de fonte de dados.  
  
 Chamar `ISSAsynchStatus::Abort` e atribuir um valor a *eOperation* diferente de DBASYNCHOP_OPEN retorna S_OK. Esse valor não significa que a operação tenha sido concluída ou cancelada.  
  
## <a name="see-also"></a>Consulte Também  
 [Executando operações assíncronas](../../oledb/features/performing-asynchronous-operations.md)  
  
  
