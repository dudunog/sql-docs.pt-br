---
title: Reproduzir para um cursor (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- replaying cursors
- traces [SQL Server], replaying
- replaying traces
ms.assetid: 89eadc41-4424-4a1c-ba61-0b52c851cdb1
author: stevestein
ms.author: sstein
ms.openlocfilehash: b1bfba95925d041c61939947efe7d8f4432cba42
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85007413"
---
# <a name="replay-to-a-cursor-sql-server-profiler"></a>Repetir até um cursor (SQL Server Profiler)
  Este tópico descreve como repetir arquivos ou tabelas de rastreamento e pausar quando um cursor for atingido, usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Pausar rastreamentos mediante cursores dá suporte à depuração, pois é possível dividir a repetição de scripts de rastreamento longos em segmentos curtos que podem ser analisados incrementalmente.  
  
### <a name="to-replay-to-the-cursor"></a>Para repetir até o cursor  
  
1.  Abra o arquivo ou tabela de rastreamento que deseja repetir. Para obter mais informações, consulte [Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](open-a-trace-file-sql-server-profiler.md) ou do [Abrir uma tabela de rastreamento &#40;SQL Server Profiler&#41;](open-a-trace-table-sql-server-profiler.md).  
  
     Certifique-se de que o arquivo ou tabela de rastreamento aberto contém as classes de evento necessárias para a repetição. Para obter mais informações, consulte [Replay Requirements](replay-requirements.md).  
  
2.  Na janela do rastreamento, clique em um evento.  
  
3.  No menu **Reprodução** , clique em **Executar até Cursor**e conecte-se ao servidor em que deseja reproduzir o rastreamento.  
  
4.  Na caixa de diálogo **Configuração de Repetição** , verifique as definições e clique em **OK**.  
  
     A repetição é iniciada, sendo pausada quando o primeiro cursor é atingido.  
  
5.  Pressione F5 para retomar o rastreamento.  
  
6.  Repita a Etapa 5 até o término do rastreamento.  
  
## <a name="see-also"></a>Consulte Também  
 [Reproduzir em um ponto de interrupção &#40;SQL Server Profiler&#41;](replay-to-a-breakpoint-sql-server-profiler.md)   
 [Repetir rastreamentos](replay-traces.md)   
 [SQL Server Profiler](sql-server-profiler.md)  
  
  
