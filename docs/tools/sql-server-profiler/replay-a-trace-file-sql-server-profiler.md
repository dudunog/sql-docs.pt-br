---
title: Reproduzir um arquivo de rastreamento
titleSuffix: SQL Server Profiler
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
ms.assetid: 9e361275-c8fd-4499-8389-242cf8e27415
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 0c658f692fcc1e58275c98e6cfd958dd8c73020f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75307526"
---
# <a name="replay-a-trace-file-sql-server-profiler"></a>Repetir um arquivo de rastreamento (SQL Server Profiler)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Repetição é a capacidade de abrir um rastreamento salvo e repeti-lo novamente. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] apresenta um mecanismo de repetição multi-threaded que consegue simular as conexões de usuário e a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A repetição é útil para solucionar problemas de aplicativos ou processos. Ao identificar o problema e implementar correções, execute o rastreamento que encontrou o problema potencial no aplicativo ou processo corrigido. Em seguida, repita o rastreamento original e compare os resultados.  
  
 Além de quaisquer outras classes de evento que desejar monitorar, devem ser capturadas classes de evento específicas para habilitar a repetição. Esses eventos serão capturados por padrão se você usar o modelo de rastreamento **TSQL_Replay** . Para obter mais informações, consulte [Replay Requirements](../../tools/sql-server-profiler/replay-requirements.md).  
  
### <a name="to-replay-a-trace-file"></a>Para repetir um arquivo de rastreamento  
  
1.  No menu **Arquivo** , aponte para **Abrir**e clique em **Arquivo de Rastreamento**. Selecione um arquivo de rastreamento que contenha as classes de evento necessárias para a repetição.  
  
2.  No menu **Repetir** , clique em **Iniciar**e conecte à instância de servidor em que deseja repetir o rastreamento.  
  
3.  Na caixa de diálogo **Configuração de Reprodução** , na guia **Opções de Reprodução Básicas** , especifique o **Servidor de reprodução**. Clique em **Alterar** para alterar o servidor exibido na caixa **Servidor de reprodução** .  
  
4.  Opcionalmente, selecione um dos seguintes destinos nos quais salvar a repetição:  
  
    -   **Salvar em arquivo**, que especifica um arquivo no qual a reprodução será salva.  
  
    -   **Salvar em tabela**, que especifica uma tabela de banco de dados na qual salvar a repetição.  
  
5.  Escolha **Reproduzir eventos na oudem em que fouam rastreados**ou **Reproduzir eventos usando vários threads**. A tabela a seguir explica a diferença entre essas configurações.  
  
    |Opção|DESCRIÇÃO|  
    |------------|-----------------|  
    |**Repetir eventos na ordem em que foram rastreados**|Repete os eventos na ordem em que foram registrados. Essa opção habilita a depuração.|  
    |**Reproduzir eventos usando vários threads**|Essa opção usa vários threads para repetir cada evento, não importando a sequência. Essa opção otimiza o desempenho.|  
  
6.  Selecione **Exibir resultados da repetição** para visualizar a repetição enquanto ela ocorre.  
  
7.  Como alternativa, clique na guia **Opções de Reprodução Avançadas**para configurar as seguintes opções:  
  
    -   Para reproduzir todas as SPIDs (IDs de processo do servidor), selecione **Reproduzir SPIDs do sistema**.  
  
    -   Para limitar a repetição aos processos pertencentes a um SPID específico, selecione **Repetir somente um SPID**. Na caixa **SPID a serem reproduzidas** , digite a SPID.  
  
    -   Para reproduzir eventos ocorridos durante um intervalo de tempo específico, selecione **Limitar reprodução por data e hora**. Selecione uma data e hora para **Hora de início**e **Hora de término**para especificar o intervalo de tempo a incluir na reprodução.  
  
    -   Para controlar o modo como o SQL Server gerencia os processos durante a reprodução, configure as **Opções do Health Monitor**.  
  
## <a name="see-also"></a>Consulte Também  
 [Permissões necessárias para executar o SQL Server Profiler](../../tools/sql-server-profiler/permissions-required-to-run-sql-server-profiler.md)   
 [Repetir rastreamentos](../../tools/sql-server-profiler/replay-traces.md)   
 [Abrir um arquivo de rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/open-a-trace-file-sql-server-profiler.md)   
 [SQL Server Profiler](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
