---
title: MSSQLSERVER_2508 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2508 (Database Engine error)
ms.assetid: c37d40e5-c665-4d66-a727-5cb845634fcc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 85859dafcdaf8321adb1211be9bb51d37930331e
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552156"
---
# <a name="mssqlserver_2508"></a>MSSQLSERVER_2508
    
## <a name="details"></a>Detalhes  
  
|Atributo|Valor|  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|2508|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC_OUT_OF_DATE_PAGE_OR_ROW_COUNT|  
|Texto da mensagem|A contagem %.*ls de objetos "%.\*ls", IDs de índice %d, IDs de partição %I64d e IDs de unidade de alocação %I64d (tipo %.\*ls) está incorreta. Execute DBCC UPDATEUSAGE.|  
  
## <a name="explanation"></a>Explicação  
 Em versões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], os valores referentes às contagens de linha de tabela e de índice e as contagens de página podem se tornar incorretas. Os bancos de dados criados em versões anteriores ao [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] podem conter contagens incorretas. O comando DBCC CHECKDB foi aprimorado para detectar esses erros e retorna essa mensagem de aviso quando detecta o erro.  
  
## <a name="user-action"></a>Ação do usuário  
 Execute DBCC UPDATEUSAGE no objeto ou índice especificado ou no banco de dados em que o objeto está contido para corrigir as contagens inválidas.  
  
  
