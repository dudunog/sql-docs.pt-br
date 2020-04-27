---
title: MSSQLSERVER_10001 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10001 (Database Engine error)
ms.assetid: f8fd2d8d-a4af-4b6a-ba51-9123b7e4c9bf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 022b1ca3c1ab4c0e1921cbac86c3059f10087f21
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62916357"
---
# <a name="mssqlserver_10001"></a>MSSQLSERVER_10001
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|10001|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|HR_E_UNEXPECTED|  
|Texto da mensagem|O provedor reportou uma falha catastrófica inesperada.|  
  
## <a name="explanation"></a>Explicação  
 O processamento de consulta distribuído encontrou um erro genérico ao chamar no provedor OLE DB.  
  
## <a name="user-action"></a>Ação do usuário  
 Colete eventos de rastreamento OLE DB usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e forneça esses dados ao suporte ao produto do provedor OLE DB.  
  
## <a name="see-also"></a>Consulte Também  
 [Modelos e permissões de SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
