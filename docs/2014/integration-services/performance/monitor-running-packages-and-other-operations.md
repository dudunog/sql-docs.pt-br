---
title: Monitoramento de execuções de pacote e outras operações | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: cbbcd79f-ab9b-46ec-84cb-4821c1d16b99
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 628b62d9c8e01d0dc0bf641551de67c3838a4504
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85423243"
---
# <a name="monitoring-for-package-executions-and-other-operations"></a>Monitorando execuções de pacotes e outras operações
  Você pode monitorar execuções de pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , validações de projeto e outras operações usando uma ou mais das ferramentas a seguir. Algumas ferramentas, como toques de dados, estão disponíveis somente para os projetos que são implantados no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
-   Logs  
  
     Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](integration-services-ssis-logging.md).  
  
-   Relatórios  
  
     Para saber mais, confira [Reports for the Integration Services Server](../reports-for-the-integration-services-server.md).  
  
-   Exibições  
  
     Para obter mais informações, consulte [Exibições &#40;Catálogo do Integration Services&#41;](/sql/integration-services/system-views/views-integration-services-catalog).  
  
-   Contadores de desempenho  
  
     Para obter mais informações, consulte [Performance Counters](performance-counters.md).  
  
-   Toques de dados  
  
## <a name="operation-types"></a>Tipos de operação  
 São monitorados vários tipos diferentes de operações no catálogo `SSISDB`, no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Cada operação pode ter várias mensagens associadas a ela. Cada mensagem pode ser classificada em um de vários tipos diferentes. Por exemplo, uma mensagem pode ser de tipo Informações, Aviso ou Erro. Para obter a lista completa dos tipos de mensagem, consulte a documentação da exibição [catalog.operation_messages &#40;Banco de Dados do SSISDB&#41;](/sql/integration-services/system-views/catalog-operation-messages-ssisdb-database) do Transact-SQL. Para ver uma lista completa dos tipos de operação, consulte [catalog.operations &#40;Banco de Dados do SSISDB&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database).  
  
 São usados nove tipos de status diferentes para indicar o status de uma operação. Para ver uma lista completa dos tipos de status, consulte a exibição [catalog.operations &#40;Banco de Dados do SSISDB&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database).  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Entrada de blog, [Visão geral da API do T-SQL SSIS](https://go.microsoft.com/fwlink/?LinkId=249051), em blogs.msdn.com.  
  
  
