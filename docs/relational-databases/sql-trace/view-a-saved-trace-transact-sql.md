---
description: Exibir um rastreamento salvo (Transact-SQL)
title: Exibir um rastreamento salvo (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], viewing
- displaying traces
- viewing traces
ms.assetid: 3a95a816-aa89-4d5f-858c-968a9cb3ee87
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: c2d709b76d5039560f3f55a720f7f96891aea548
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88324899"
---
# <a name="view-a-saved-trace-transact-sql"></a>Exibir um rastreamento salvo (Transact-SQL)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como usar funções internas para exibir um rastreamento salvo.  
  
### <a name="to-view-a-specific-trace"></a>Exibir um rastreamento específico  
  
1.  Execute **fn_trace_getinfo** especificando a identificação do rastreamento sobre o qual informações são necessárias. Esta função retorna uma tabela que lista o rastreamento, a propriedade de rastreamento e as informações sobre a propriedade.  

     Invoque a função deste modo:  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(trace_id)  
    ```  
  
### <a name="to-view-all-existing-traces"></a>Exibir todos os rastreamentos existentes  
  
1.  Execute **fn_trace_getinfo** especificando `0` ou `default`. Esta função retorna uma tabela que lista todos os rastreamentos, suas propriedades e as informações sobre essas propriedades.  
  
     Chame a função como segue:  
  
    ```  
    SELECT *  
    FROM ::fn_trace_getinfo(default)  
    ```  
  
## <a name="net-framework-security"></a>Segurança do .NET Framework  
 Para executar a função interna **fn_trace_getinfo**, o usuário precisa da seguinte permissão:  
  
 ALTER TRACE no servidor.  
  
## <a name="see-also"></a>Consulte Também  
 [sys.fn_trace_getinfo &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)   
 [Exibir e analisar rastreamentos com o SQL Server Profiler](../../tools/sql-server-profiler/view-and-analyze-traces-with-sql-server-profiler.md)  
  
  
