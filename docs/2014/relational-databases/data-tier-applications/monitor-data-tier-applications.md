---
title: Monitorar aplicativos da camada de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- monitoring [SQL Server], data-tier applications
- monitoring server performance [SQL Server], DACs
- data-tier application [SQL Server], monitor
ms.assetid: d2765828-2385-4019-aef2-1de3ab7d1b26
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8fe96b7d84a2e363166238c3e840cac383f443dc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62918060"
---
# <a name="monitor-data-tier-applications"></a>Monitorar aplicativos da camada de dados
  Um DAC (aplicativo da camada de dados) pode ser monitorado no **Gerenciador do Utilitário** e no **Pesquisador de Objetos** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] (SSMS), junto com exibições e tabelas do sistema. Além disso, todos os objetos no banco de dados contidos no DAC podem ser monitorados usando técnicas padrão de monitoração de banco de dados e [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## <a name="before-you-begin"></a>Antes de começar  
 Se você implantar um DAC em uma instância gerenciada do [!INCLUDE[ssDE](../../includes/ssde-md.md)], as informações sobre o DAC implantado serão incorporadas no Utilitário do SQL Server na próxima vez que o conjunto de coleta do utilitário for enviado da instância para o ponto de controle de utilitário. Você pode exibir informações de integridade básicas sobre o DAC usando o Gerenciador do Utilitário [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]Gerenciador do Utilitário**do**.  
  
 O **Pesquisador de Objetos** do SSMS exibe informações básicas de configuração sobre cada DAC implantado em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)], independentemente de a instância ser ou não gerenciada no Utilitário do SQL Server. Além disso, o banco de dados associado a um DAC implantado pode ser monitorado usando os mesmos procedimentos de monitoramento de qualquer banco de dados.  
  
## <a name="using-the-sql-server-utility"></a>Usando o Utilitário do SQL Server  
 A página de detalhes **Aplicativos da Camada de Dados Implantados** no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **Utility Explorer** displays a dashboard that reports the resource utilization of all DACs that have been deployed to managed instances of the [!INCLUDE[ssDE](../../includes/ssde-md.md)]. O painel da parte superior da página de detalhes lista cada DAC implantado com indicadores visuais que mostram se a sua utilização de CPU e recursos de arquivo está fora das políticas definidas para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility. Se você selecionar qualquer DAC na exibição de lista, serão exibidos detalhes adicionais em guias no painel inferior da página. Para obter mais informações sobre as informações apresentadas na página de detalhes, veja [Detalhes do aplicativo da camada de dados implantado &#40;Utilitário do SQL Server&#41;](../../database-engine/deployed-data-tier-application-details-sql-server-utility.md).  
  
 Depois de usar a página de detalhes **Aplicativos da Camada de Dados Implantados** para identificar rapidamente os DACs que estão subutilizados ou exigindo recursos de hardware demais, você poderá fazer planos para resolver qualquer problema. Vários DACs que não estão utilizando os recursos de hardware atuais completamente poderiam ser consolidados em um único servidor, liberando alguns servidores para outros usos. Se um DAC estiver exigindo recursos demais do servidor atual, o DAC pode ser movido para um servidor maior ou é possível acrescentar recursos ao servidor atual.  
  
 Os limites mínimos e máximos para uso de recurso são definidos por políticas de monitoração de aplicativo definidas na página de detalhes **Administração do Utilitário** . Os administradores de banco de dados podem personalizar as políticas para corresponder aos limites estabelecidos por suas organizações. Por exemplo, uma empresa pode definir 75% como a utilização de CPU máxima para um DAC, enquanto outra pode definir o máximo como 80%. Para obter mais informações sobre como definir políticas de monitoramento de aplicativo, veja [Administração do Utilitário &#40;Utilitário do SQL Server&#41;](../../database-engine/utility-administration-sql-server-utility.md).  
  
 Para exibir a página de detalhes **Aplicativos da Camada de Dados Implantados** :  
  
1.  Selecione o menu **Exibir/Gerenciador do Utilitário** .  
  
2.  Conecte o **Gerenciador do Utilitário** ao UCP (ponto de controle do utilitário).  
  
3.  Selecione o menu **Exibir/Detalhes do Gerenciador do Utilitário** .  
  
4.  Selecione o nó **Aplicativos da Camada de Dados Implantados** no **Gerenciador do Utilitário**.  
  
 As informações na página de detalhes **Aplicativos da Camada de Dados Implantados** é resultado dos dados no data warehouse de gerenciamento do utilitário, cujo padrão é coletar dados a cada 15 minutos. O intervalo também pode ser personalizado usando a página de detalhes **Administração do Utilitário** .  
  
## <a name="using-object-explorer"></a>Usando o Pesquisador de Objetos  
 O **Pesquisador de Objetos** do SSMS exibe informações básicas de configuração sobre cada DAC implantado em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Isto inclui tanto as instâncias gerenciadas que foram inscritas no Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quanto as instâncias autônomas que não podem ser exibidas no **Gerenciador do Utilitário**.  
  
 Para exibir os detalhes de um DAC implantado em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]:  
  
1.  Selecione o menu **Exibir/Pesquisador de Objetos** .  
  
2.  Conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]no painel Pesquisador de Objetos.  
  
3.  Selecione o menu **Exibir/Detalhes do Pesquisador de Objetos** .  
  
4.  Selecione o nó de servidor em **Pesquisador de Objetos** que é mapeado para a instância e navegue até o nó **Gerenciamento\Aplicativos da Camada de Dados** .  
  
5.  A exibição de lista no painel da parte superior da página de detalhes lista cada DAC implantado na instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Selecione um DAC para o qual exibir as informações no painel de detalhes na parte inferior da página.  
  
 O menu de atalho do nó **Aplicativos da camada de Dados** também é usado para implantar um novo DAC ou excluir um existente.  
  
## <a name="using-the-dac-system-views-and-tables"></a>Usando as exibições e as tabelas do sistema de DAC  
 A tabela do sistema msdb.dbo.sysdac_history_internal registra o êxito ou a falha de todas as ações de gerenciamento do DAC realizadas em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. A tabela registra a hora em que cada ação ocorreu e qual logon iniciou a ação. Para obter mais informações, veja [sysdac_history_internal &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/data-tier-application-tables-sysdac-history-internal).  
  
 As exibições do sistema do DAC relatam informações básicas de catálogo. Para obter mais informações, veja [Exibições de aplicativo da camada de dados &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/data-tier-application-views-dbo-sysdac-instances).  
  
## <a name="monitoring-dac-databases"></a>Monitorando bancos de dados DAC  
 Depois que um DAC foi implantado com êxito, o banco de dados contido no DAC funciona igual a qualquer outro banco de dados. Use técnicas e ferramentas padrão do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para monitorar desempenho, log, eventos e utilização de recursos do banco de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Aplicativos da Camada de Dados](data-tier-applications.md)   
 [Implantar um aplicativo da camada de dados](deploy-a-data-tier-application.md)  
  
  
