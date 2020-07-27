---
title: Analisar um plano de execução real | Microsoft Docs
description: Saiba como analisar planos de execução gráfica reais, que contêm informações sobre o runtime, usando o recurso de Análise de Plano do SQL Server Management Studio.
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- analyzing execution plans
- analyzing actual execution plans
- execution plans [SQL Server], analyzing
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: 1424558566e544acd1a65aeb39c9a83747bbbb64
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458581"
---
# <a name="analyze-an-actual-execution-plan"></a>Analisar um plano de execução real

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este tópico descreve como você pode analisar planos de execução gráficos reais usando o recurso de Análise de Plano [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Este recurso está disponível a partir do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v17.4. Geralmente, recomendamos que você [instale a versão mais recente do SSMS](../../ssms/download-sql-server-management-studio-ssms.md).

> [!NOTE]
> Os planos de execução reais são gerados depois que as consultas ou lotes [!INCLUDE[tsql](../../includes/tsql-md.md)] são executados. Por isso, um plano de execução real contém informações de runtime, como número real de linhas, métricas de uso de recursos e avisos de runtime (se houver). Para obter mais informações, confira [Exibir um plano de execução real](../../relational-databases/performance/display-an-actual-execution-plan.md).
  
Solução de problemas de desempenho de consulta requer conhecimento significativo sobre as noções básicas de processamento e execução de planos de consulta para poder de fato encontrar e consertar as causas raiz.

[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] inclui a funcionalidade que implementa um certo grau de automação na tarefa de análise de plano de execução real, especialmente para planos grandes e complexos. A meta é tornar mais fácil encontrar os cenários de [Estimativa de Cardinalidade](../../relational-databases/performance/cardinality-estimation-sql-server.md) imprecisa e obter recomendações sobre quais mitigações possíveis podem estar disponíveis.

> [!IMPORTANT]
> Realize o teste adequado das mitigações propostas antes de aplicá-las em ambientes de produção.
  
## <a name="to-analyze-an-execution-plan-for-a-query"></a>Para analisar um plano de execução para uma consulta  
  
1.  Abra um arquivo de plano de execução de consulta salvo anteriormente (.sqlplan) usando o menu **Arquivo** e clicando em **Abrir Arquivo** ou arraste um arquivo de plano para a janela [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]. Como alternativa, se você tiver acabado de executar uma consulta e optar por exibir seu plano de execução, vá para a guia **Plano de Execução** guia no painel de resultados. 

2.  Clique com o botão direito do mouse em uma área em branco do plano de execução e clique em **Analisar Plano de Execução Real**. 

    ![Clique com o botão direito do mouse em Analisar Plano de Execução Real](../../relational-databases/performance/media/plananalysismenuoption.png "Clique com o botão direito do mouse em Analisar Plano de Execução Real")   

3.  A janela **Análise de Plano de execução** é aberta na parte inferior. A guia **Várias Instruções** é útil ao analisar planos com várias instruções, permitindo que a instrução certa seja analisada.

4.  Selecione a guia Cenários para ver detalhes sobre os problemas encontrados para o plano de execução real. Para cada operador listado no painel esquerdo, o painel direito mostra detalhes sobre o cenário no link *Clique aqui para obter mais informações sobre esse cenário* e possíveis razões para explicar esse cenário são listadas.

    ![Resultados da Análise do Plano de Execução](../../relational-databases/performance/media/plananalysis-scenarios.png "Resultados da Análise do Plano de Execução") 
