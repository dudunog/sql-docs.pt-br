---
title: Opções de reprodução (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- traces [SQL Server], replaying
- replaying traces
- health monitor [SQL Server]
- Replay Configuration dialog box
ms.assetid: 58761a25-a84f-4a90-9c61-97700bc5ad9c
author: stevestein
ms.author: sstein
ms.openlocfilehash: 068a6aaeba1af8c456c77fd45ecdc2a52719b0f2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063986"
---
# <a name="replay-options-sql-server-profiler"></a>Opções de repetição (SQL Server Profiler)
  Antes de repetir um rastreamento capturado com [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], especifique as seguintes opções de repetição na caixa de diálogo **Configuração de Repetição** . Para inicializar essa caixa de diálogo, abra o arquivo ou tabela de rastreamento a repetir no [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]e, no menu **Repetir** , clique em **Iniciar**. Para obter informações sobre quais permissões são necessárias para reproduzir um rastreamento, veja [Permissões necessárias para executar o SQL Server Profiler](sql-server-profiler.md).  
  
 Este tópico descreve as opções especificadas com a caixa de diálogo **Configuração de Repetição** .  
  
> [!NOTE]  
>  É recomendável usar o Distributed Replay Utility para reproduzir um aplicativo OLTP intensivo (com muitas conexões simultâneas ativas ou alta taxa de transferência). O Distributed Replay Utility pode reproduzir dados de rastreamento de vários computadores, com uma simulação melhor de uma carga de trabalho de missão crítica. Para obter mais informações, consulte [SQL Server Distributed Replay](../distributed-replay/sql-server-distributed-replay.md).  
  
## <a name="basic-replay-options"></a>Opções de repetição básicas  
 **Servidor de repetição**  
 O servidor é o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em relação ao qual se deseja repetir o rastreamento. O servidor deve cumprir os requisitos de repetição descritos em [Replay Requirements](replay-requirements.md)".  
  
 **Salvar no arquivo**  
 O arquivo de saída em que é gravado o resultado da repetição do rastreamento para posterior análise. Por padrão, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] exibe os resultados da repetição do rastreamento apenas na tela.  
  
 **Salvar na tabela**  
 O tabela de banco de dados em que é gravado o resultado da repetição do rastreamento para posterior análise.  
  
 **Número de threads de repetição**  
 Especifica o número de threads de repetição a usar simultaneamente. Um número mais alto consome mais recursos durante a repetição, porém ela é mais rápida. A ordenação de eventos não é completamente mantida quando são usados vários threads.  
  
 **Repetir eventos na ordem em que foram rastreados**  
 Permite-lhe usar métodos de depuração, como cada etapa de cada rastreamento. Se esta opção não estiver selecionada, a repetição não garantirá que os eventos sejam repetidos em uma ordem consistente com a que foram capturados originalmente.  
  
 **Reproduzir eventos usando vários threads**  
 Otimiza o desempenho e desabilita a depuração. Os eventos são repetidos na ordem em que foram registrados para uma ID de processo do servidor (SPID) específica, mas não se garante a ordem dos SPIDs.  
  
 **Exibir resultados da repetição**  
 Exibe os resultados da repetição. Essa é a opção padrão. Se o rastreamento que está sendo repetido for muito grande, pode ser conveniente desabilitar essa opção para economizar espaço em disco.  
  
> [!NOTE]  
>  Para um melhor desempenho da repetição, recomendamos selecionar eventos a repetir usando vários threads e não selecionar a exibição dos resultados da repetição.  
  
## <a name="advanced-replay-options"></a>Opções de repetição avançadas  
 **Repetir SPIDs do sistema**  
 Repetir todos os SPIDs. Essa é a opção padrão.  
  
 **Repetir somente um SPID**  
 Repetir o número de SPID selecionado na lista.  
  
 **Limitar repetição por data e hora**  
 Repete o rastreamento para a **Hora de início** e **Hora de término**especificadas.  
  
 **Intervalo de espera do Health Monitor**  
 Define o tempo de execução permitido a um processo até que o Health Monitor o encerre.  
  
 **Intervalo de sondagem do Health Monitor**  
 Define a frequência com que o Health Monitor sonda candidatos a encerramento.  
  
 **Habilitar monitor de processos bloqueados do SQL Server**  
 Define a frequência com que o monitor de processos bloqueados procura processos bloqueados ou que estejam causando bloqueios.  
  
## <a name="about-the-health-monitor"></a>Sobre o Health Monitor  
 O Health Monitor é um thread de aplicativo que monitora os processos simulados envolvidos na repetição de um rastreamento e encerra os processos que se encontram bloqueados na repetição. Na guia **Opções de Repetição Avançadas** da caixa de diálogo **Configuração de Repetição** , é possível especificar o tempo, em segundos, que o Health Monitor deve esperar antes de encerrar um processo bloqueado (**Intervalo de espera do Health Monitor**). Se você definir esse intervalo como 0, o Health Monitor nunca encerrará os processos que causam bloqueios no rastreamento de repetição.  
  
## <a name="see-also"></a>Consulte Também  
 [Repetir rastreamentos](replay-traces.md)   
 [Requisitos para reprodução](replay-requirements.md)   
 [Considerações para reproduzir rastreamentos &#40;SQL Server Profiler&#41;](considerations-for-replaying-traces-sql-server-profiler.md)  
  
  
