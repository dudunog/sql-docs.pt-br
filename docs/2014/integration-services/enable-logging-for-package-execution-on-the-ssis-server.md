---
title: Habilitar o log para a execução do pacote no servidor SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8930c63c-bc6f-46c2-b428-b3c29ee89a7d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 47f74d4510b46b984eb58706ff4ac159cb8b1352
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66059367"
---
# <a name="enable-logging-for-package-execution-on-the-ssis-server"></a>Habilitar o log para a execução do pacote no servidor SSIS
  Este procedimento descreve como definir ou alterar o nível de log para um pacote quando você executa um pacote implantado no servidor [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . O nível de log que você define ao executar o pacote anula o log do pacote configurado usando o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Consulte [Habilitar o log de pacote no SQL Server Data Tools](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md) para obter mais informações.  
  
 Você pode especificar o nível de log usando um dos métodos a seguir. Este tópico aborda o primeiro método.  
  
-   Configuração de uma instância de uma execução de pacote usando a caixa de diálogo Executar Pacote  
  
-   Configuração de parâmetros para uma instância de uma execução usando o [catalog.set_execution_parameter_value &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database)  
  
-   Configuração de um trabalho do SQL Server Agent para uma execução de pacote usando a caixa de diálogo Nova Etapa de Trabalho.  
  
### <a name="to-set-the-logging-level-for-a-package-by-using-the-execute-package-dialog-box"></a>Para definir o nível de log para um pacote usando a caixa de diálogo Executar Pacote  
  
1.  No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], navegue até o pacote no Pesquisador de Objetos.  
  
2.  Clique com o botão direito do mouse no pacote e selecione **Executar**.  
  
3.  Selecione a guia **Avançado** na caixa de diálogo **Executar Pacote** .  
  
4.  Em **Nível de log**, selecione o nível de log. Consulte a tabela abaixo para obter uma descrição de valores disponíveis.  
  
5.  Conclua qualquer outra configuração de pacote e clique em **OK** para executar o pacote.  
  
 Os níveis de log a seguir estão disponíveis.  
  
|Nível de log|Descrição|  
|-------------------|-----------------|  
|Nenhum|O log está desativado. Apenas o status da execução do pacote é registrado em log.|  
|Basic|Todos os eventos são registrados em log, menos personalizados e de diagnóstico. Este é o valor padrão.|  
|Desempenho|Apenas estatísticas de desempenho e eventos OnError e OnWarning são registrados em log.<br /><br /> O relatório **Desempenho de Execução** mostra a hora ativa e o tempo total para os componentes de fluxo de dados do pacote. Estas informações estão disponíveis quando o nível de log da última execução do pacote foi definido como **desempenho** ou **detalhado**. Para saber mais, confira [Reports for the Integration Services Server](../../2014/integration-services/reports-for-the-integration-services-server.md).<br /><br /> A exibição [catalog.execution_component_phases](/sql/integration-services/system-views/catalog-execution-component-phases) mostra as horas de início e de término para os componentes de fluxo de dados, para cada fase de uma execução. Esta exibição mostra essas informações para esses componentes apenas quando o nível de log da execução do pacote é definido como **Desempenho** ou **Detalhado**.|  
|Detalhado|Todos os eventos são registrados em log, inclusive eventos personalizados e de diagnóstico.<br /><br /> Um exemplo de um evento de diagnóstico é o evento DiagnosticEx. Sempre que uma tarefa Executar Pacote executa um pacote filho, ela registra esse evento. A mensagem de evento consiste nos valores de parâmetros passados para pacotes filho<br /><br /> O valor da coluna de mensagem para DiagnosticEx é texto XML. . Para exibir o texto da mensagem para uma execução de pacote, consulte a exibição [catalog.operation_messages &#40;Banco de Dados SSISDB&#41;](/sql/integration-services/system-views/catalog-operation-messages-ssisdb-database).<br /><br /> Observação: os eventos personalizados incluem os eventos que são registrados [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] por tarefas. Para obter mais informações, consulte [mensagens personalizadas para registro em log](../../2014/integration-services/custom-messages-for-logging.md).<br /><br /> A exibição [catalog.execution_data_statistics](../relational-databases/statistics/statistics.md) mostra uma linha cada vez que um componente de fluxo de dados envia dados a um componente downstream, para determinada execução do pacote. O nível de log deve ser definido como **Detalhado** para capturar essas informações na exibição.|  
  
## <a name="see-also"></a>Consulte Também  
 [Log de&#41; Integration Services &#40;SSIS](performance/integration-services-ssis-logging.md)   
 [Habilitar o log de pacote no SQL Server Data Tools](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md)  
  
  
