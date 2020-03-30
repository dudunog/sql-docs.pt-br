---
title: SQL Server Distributed Replay
titleSuffix: SQL Server Distributed Replay
ms.prod: sql
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 58ef7016-b105-42c2-90a0-364f411849a4
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: c52325045cd21d0eb11edef8b0664d14c292e729
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74993422"
---
# <a name="sql-server-distributed-replay"></a>SQL Server Distributed Replay

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

O recurso [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay ajuda a avaliar o impacto de atualizações futuras do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Também é possível usar esse recurso para ajudar a avaliar o impacto das atualizações de hardware e sistemas operacionais e ajuste do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="benefits-of-distributed-replay"></a>Benefícios do Distributed Replay  
 De modo semelhante ao [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], você pode usar o Distributed Replay para reproduzir um rastreamento capturado em um ambiente de teste atualizado. Diferentemente do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], o Distributed Replay não está limitado à reprodução da carga de trabalho de um único computador.  
  
 O Distributed Replay oferece uma solução mais dimensionável do que o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Com o Distributed Replay, é possível reproduzir uma carga de trabalho de vários computadores e simular melhor uma carga de trabalho de missão crítica.  
  
 O recurso [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay pode usar vários computadores para reproduzir dados de rastreamento e simular uma carga de trabalho de missão crítica. Use o Distributed Replay para teste de compatibilidade de aplicativo, teste de desempenho ou planejamento de capacidade.  
  
## <a name="when-to-use-distributed-replay"></a>Quando usar o Distributed Replay  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] e o Distributed Replay fornecem algumas funções sobrepostas.  
  
 Você pode usar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para repetir um rastreamento capturado em um ambiente de teste atualizado. Também é possível analisar os resultados da repetição para procurar incompatibilidades de função e desempenho. No entanto, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] somente pode repetir uma carga de trabalho de um único computador. Ao repetir um aplicativo OLTP intensivo que tenha muitas conexões simultâneas ativas ou alta taxa de transferência, o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] pode se tornar um gargalo de recurso.  
  
 O Distributed Replay oferece uma solução mais dimensionável do que o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Use o Distributed Replay para reproduzir uma carga de trabalho de vários computadores e simular melhor uma carga de trabalho de missão crítica.  
  
 A tabela a seguir descreve quando usar cada ferramenta.  
  
|Ferramenta|Use quando...|  
|----------|---------------|  
|[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]|Você quiser usar o mecanismo de repetição convencional em um único computador. Em particular, você precisa de recursos de depuração linha a linha, como os comandos **Etapa**, **Executar até o Cursor**e **Ativar/Desativar Pontos de Interrupção** .<br /><br /> Você deseja repetir um rastreamento [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|Distributed Replay|Você quiser avaliar a compatibilidade de aplicativo. Por exemplo, você deseja testar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os cenários de atualização de sistema operacional, atualizações de hardware ou ajuste de índice.<br /><br /> A simultaneidade no rastreamento capturado é tão alta que um único cliente de repetição não pode simular isso suficientemente.|  
  
## <a name="distributed-replay-concepts"></a>Conceitos do Distributed Replay  
 Os seguintes componentes fazem parte do ambiente do Distributed Replay:  
  
-   **ferramenta de administração Distributed Replay**: um aplicativo de console, **DReplay.exe**, usado para se comunicar com o controlador de reprodução distribuída. Use a ferramenta de administração para controlar a reprodução distribuída.  
  
-   **controlador Distributed Replay**: um computador que executa o serviço Windows denominado controlador Distributed Replay do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O controlador Distributed Replay orquestra as ações dos clientes de reprodução distribuída. Cada ambiente de Distributed Replay pode conter apenas uma instância de controlador.  
  
-   **Clientes do Distributed Replay**: um ou mais computadores (físicos ou virtuais) que executam o serviço Windows denominado Cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay. Os clientes do Distributed Replay trabalham juntos para simular cargas de trabalho em uma instância do SQL Server do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Pode haver um ou mais clientes em cada ambiente do Distributed Replay.  
  
-   **Servidor de destino**: uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que clientes do Distributed Replay podem usar para reproduzir dados de rastreamento. Nós recomendamos que o servidor de destino seja localizado em um ambiente de teste.  
  
 A ferramenta de administração Distributed Replay, o controlador e o cliente podem ser instalados em diferentes computadores ou no mesmo computador. Só pode existir uma instância do serviço de cliente ou controlador do Distributed Replay em execução no mesmo computador.  
  
 A seguinte figura mostra para a arquitetura física do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay:  
  
 ![Arquitetura de Distributed Replay](../../tools/distributed-replay/media/distributedreplayarch.gif "Arquitetura de Distributed Replay")  
  
## <a name="distributed-replay-tasks"></a>Tarefas do Distributed Replay  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como configurar o Distributed Replay.|[Configurar o Distributed Replay](../../tools/distributed-replay/configure-distributed-replay.md)|  
|Descreve como preparar os dados de rastreamento de entrada.|[Preparar os dados de rastreamento de entrada](../../tools/distributed-replay/prepare-the-input-trace-data.md)|  
|Descreve como reproduzir dados de rastreamento.|[Reproduzir dados de rastreamento](../../tools/distributed-replay/replay-trace-data.md)|  
|Descreve como revisar os resultados de dados de rastreamento de Distributed Replay.|[Examinar os resultados da reprodução](../../tools/distributed-replay/review-the-replay-results.md)|  
|Descreve como usar a ferramenta de administração para iniciar, monitorar e cancelar operações no controlador.|[Opções de linha de comando da ferramenta de administração &#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [Fórum do SQL Server Distributed Replay](https://social.technet.microsoft.com/Forums/sl/sqldru/)   
 [Uso do Distributed Replay para teste de carga do SQL Server – Parte 2](https://blogs.msdn.com/b/mspfe/archive/2012/11/14/using-distributed-replay-to-load-test-your-sql-server-part-2.aspx)   
 [Usando o Distributed Replay para teste de carga do SQL Server – Parte 1](https://blogs.msdn.com/b/mspfe/archive/2012/11/08/using-distributed-replay-to-load-test-your-sql-server-part-1.aspx)  
  
  
