---
title: Exibir o plano de execução estimado | Microsoft Docs
description: Saiba como gerar planos de execução gráfica estimados usando o SQL Server Management Studio. Um plano de execução estimado não contém informações sobre o runtime.
ms.custom: ''
ms.date: 11/21/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- zoom [SQL Server]
- estimated execution plan [SQL Server]
- displaying execution plans
- viewing execution plans
- execution plans [SQL Server], displaying
- customizing execution plan display [SQL Server]
- modifying execution plan display
- custom zoom [SQL Server]
ms.assetid: e94aa576-4c0c-4c54-ad05-6c3432cc615b
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 90b7074b12a3c3a49588a9c791cde1386212192b
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/17/2020
ms.locfileid: "86457278"
---
# <a name="display-the-estimated-execution-plan"></a>Exibir o plano de execução estimado
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Este tópico descreve como gerar planos de execução gráfica estimados usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Quando são gerados planos de execução estimados, as consultas ou lotes [!INCLUDE[tsql](../../includes/tsql-md.md)] não são executadas. Por isso, um plano de execução estimado não contém informações de runtime, como avisos de runtime ou métricas de uso real do recurso. Em vez disso, o plano de execução gerado exibirá o plano de execução de consulta que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] teria maior probabilidade de usar se as consultas fossem executadas, e exibirá a estimativa de linhas que passam por vários operadores no plano.  
  
 Para usar esse recurso, os usuários devem ter as permissões apropriadas para executar a consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] para as quais está sendo gerado um plano de execução gráfica e devem ter permissão SHOWPLAN para todos os bancos de dados incluídos na consulta.  
  
## <a name="to-display-the-estimated-execution-plan-for-a-query"></a>Para exibir o plano de execução estimado para uma consulta  
  
1.  Na barra de ferramentas, clique em **Consulta do Mecanismo de Banco de Dados**. Você também pode abrir uma consulta existente e exibir o plano de execução estimado clicando no botão de barra de ferramentas **Abrir Arquivo** e localizando a consulta existente.  
  
2.  Insira a consulta para a qual você deseja exibir o plano de execução estimado.  
  
3.  No menu **Consulta** , clique em **Exibir Plano de Execução Estimado** ou clique no botão de barra de ferramentas **Exibir Plano de Execução Estimado** . O plano de execução estimado é exibido na guia **Plano de execução** no painel de resultados. 

    ![Botão Plano de Execução Estimado na barra de ferramentas](../../relational-databases/performance/media/estimatedexecplantoolbar.png "Botão Plano de Execução Estimado na barra de ferramentas")    

    Para exibir mais informações, mantenha o mouse sobre os ícones dos operadores lógicos e físicos e exiba a dica de tela com a descrição e as propriedades do operador. Você também pode exibir propriedades do operador na janela Propriedades. Se a janela Propriedades não estiver visível, clique com o botão direito do mouse em um operador e clique em **Propriedades**. Selecione um operador cujas propriedades exibir.  

    ![Clicar com o botão direito do mouse em Propriedades no operador de plano](../../relational-databases/performance/media/planproperties.png "Clicar com o botão direito do mouse em Propriedades no operador de plano")    
  
4.  Para alterar a exibição do plano de execução, clique com o botão direito do mouse no plano de execução e selecione **Ampliar**, **Reduzir**, **Zoom Personalizado**ou **Ajustar Nível de Zoom**. **Ampliar** e **Reduzir** permitem ampliar ou reduzir o plano de execução com valores fixos. **Zoom personalizado** permite que você defina sua própria ampliação da exibição, como ampliar em 80 por cento. **Ajustar Nível de Zoom** aumenta o plano de execução para se ajustar ao painel de resultados. Como alternativa, use a tecla CTRL e o botão de rolagem do mouse para ativar o **zoom dinâmico**.  

5.  Para navegar na exibição do plano de execução, use as barras de rolagem vertical e horizontal ou **clique e segure em qualquer área em branco** do plano de execução e **arraste o mouse**. Como alternativa, clique e segure o sinal de adição (+) no canto inferior direito da janela de plano de execução para exibir um mapa em miniatura de todo o plano de execução.
 
> [!NOTE] 
> Como alternativa, use [SET SHOWPLAN_XML](../../t-sql/statements/set-showplan-xml-transact-sql.md) para retornar informações do plano de execução para cada instrução sem executá-las. Se usada em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], a guia *Resultados* terá um link para abrir o plano de execução em formato gráfico.   
  
## <a name="see-also"></a>Consulte Também  
 [Planos de execução](../../relational-databases/performance/execution-plans.md)    
 [Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md)  
