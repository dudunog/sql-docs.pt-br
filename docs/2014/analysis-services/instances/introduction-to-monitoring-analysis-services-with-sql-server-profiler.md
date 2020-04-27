---
title: Introdução ao monitoramento de Analysis Services com SQL Server Profiler | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Profiler, Analysis Services
- monitoring Analysis Services [SQL Server]
- performance [Analysis Services]
- performance [Analysis Services], SQL Server Profiler
- Profiler [SQL Server Profiler], Analysis Services
ms.assetid: 568ec549-5ddc-493a-b9f8-3bdc548b562e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a3146f5a9f3e22753cc86c07b609d997be580b9f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66079803"
---
# <a name="introduction-to-monitoring-analysis-services-with-sql-server-profiler"></a>Introdução ao monitoramento do Analysis Services com o SQL Server Profiler
  Você pode usar [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] o para monitorar eventos gerados por uma instância [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]do. Usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], você pode fazer o seguinte:  
  
-   Monitorar o desempenho de uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
-   Depurar as instruções da linguagem MDX.  
  
-   Identificar as instruções MDX executadas lentamente.  
  
-   Testar as instruções MDX na fase de desenvolvimento de um projeto, percorrendo as instruções para confirmar se o código funciona conforme o esperado.  
  
-   Solucionar problemas no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] capturando eventos em um sistema de produção e repeti-los em um sistema de teste. Essa abordagem é útil para testar ou depurar propósitos e permite que os usuários continuem a usar o sistema de produção sem interferência.  
  
-   Auditar e revisar atividades ocorridas em uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Um administrador de segurança pode revisar qualquer um dos eventos auditados. A revisão inclui o êxito ou a falha de uma tentativa de logon e o êxito ou a falha das permissões ao acessar instruções e objetos.  
  
-   Exibir dados sobre os eventos capturados na tela ou capturar e salvar dados sobre cada evento em um arquivo ou na tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para análise ou reprodução futura. Ao repetir os dados, é possível executar novamente os eventos salvos conforme ocorreram originalmente, seja em tempo real ou passo a passo.  
  
## <a name="using-sql-server-profiler"></a>Usando o SQL Server Profiler  
 Para usar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para criar ou repetir rastreamentos, você deve ser um membro da função de servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Se você for um membro da função de servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , inicie o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] a partir do grupo de programas [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no menu **Iniciar** .  
  
 Ao usar o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], observe o seguinte:  
  
-   As definições de rastreamento são armazenadas no banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usando a instrução CREATE.  
  
-   Vários rastreamentos podem ser executados ao mesmo tempo.  
  
-   Várias conexões podem receber eventos do mesmo rastreamento.  
  
-   Um rastreamento pode continuar quando o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] parar e for reiniciado.  
  
    > [!NOTE]  
    >  As senhas não são reveladas em eventos de rastreamento, \* \* \* \* \* \* mas são substituídas por no evento.  
  
 Para obter o desempenho ideal, use o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para monitorar somente os eventos pelos quais você tem maior interesse. O monitoramento de muitos eventos pode causar sobrecarga e aumentar muito a tabela ou o arquivo de rastreamento, especialmente durante o monitoramento em um longo período de tempo. Além disso, use a filtragem para limitar a quantidade de dados coletados e impedir o aumento em excesso dos rastreamentos.  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos de rastreamento de Analysis Services](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events)   
 [Criar rastreamentos do Profiler para reprodução &#40;Analysis Services&#41;](create-profiler-traces-for-replay-analysis-services.md)  
  
  
