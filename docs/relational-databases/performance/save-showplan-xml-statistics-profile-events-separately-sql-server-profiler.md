---
title: Salvar eventos de perfil de estatísticas do Plano de Execução XML separadamente
description: Saiba como salvar eventos do Perfil de Estatísticas XML do Plano de Execução capturados em rastreamentos em arquivos com o SQL Server Profiler. Abra os arquivos no SQL Server Management Studio.
titleSuffix: SQL Server Profiler
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Showplan XML events
- saving Showplan XML events
- events [SQL Server], Showplan XML
ms.assetid: df393f13-d538-4d94-8155-9c2fdf5f755d
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 6c15e6ffae81724aebced968f1031ed4b7713451
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/02/2020
ms.locfileid: "96504991"
---
# <a name="save-showplan-xml-statistics-profile-events-separately-sql-server-profiler"></a>Salvar eventos de perfil de estatísticas do Plano de Execução XML separadamente (SQL Server Profiler)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Esse tópico descreve como salvar eventos **Showplan XML Statistics Profile** que são capturados nos rastreamentos em arquivos .SQLPlan separados, por meio do [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]. Você pode abrir os arquivos de eventos de **perfil de estatísticas do Plano de Execução XML** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], o que permite exibir o plano de execução gráfico de cada evento.  
  
## <a name="save-showplan-xml-statistics-profile-events-separately"></a>Salvar eventos de perfil de estatísticas do Plano de Execução XML separadamente  
  
1. No menu **Arquivo**, selecione **Novo Rastreamento** e conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     É exibida a caixa de diálogo **Propriedades do Rastreamento** .  
  
    > [!NOTE]  
    >  Se você selecionar **Iniciar rastreamento imediatamente após estabelecer a conexão**, a caixa de diálogo **Propriedades do Rastreamento** não será exibida e, em vez disso, o rastreamento será iniciado. Para desligar essa configuração, no menu **Ferramentas**, selecione **Opções** e desmarque a caixa de seleção **Iniciar rastreamento imediatamente após estabelecer a conexão**.  
  
2. Na caixa de diálogo **Propriedades do Rastreamento** , digite um nome para o rastreamento na caixa **Nome do rastreamento** .  
  
3. Na lista **Usar o modelo**, selecione um modelo de rastreamento no qual esse rastreamento deve ser baseado. Se você não quiser usar um modelo, selecione **Em branco**.  
  
4. Realize um dos seguintes procedimentos:  
  
    -   Selecione a caixa de seleção **Salvar em arquivo** para capturar o rastreamento em um arquivo. Especifique um valor para **Definir tamanho máximo do arquivo**.  
  
         Opcionalmente, marque as caixas de seleção **Habilitar substituição de arquivo** e **Dados de rastreamento de processos do servidor** . 
  
    -   Marque a caixa de seleção **Salvar em tabela** para capturar o rastreamento em uma tabela de banco de dados.  
  
         Opcionalmente, selecione **Definir máximo de linhas** e especifique um valor.  
  
5. Opcionalmente, marque a caixa de seleção **Habilitar horário de parada do rastreamento** e especifique uma data e hora de parada. 
  
6. Selecione a guia **Seleção de Eventos**.  
  
7. Na coluna de dados **Eventos**, expanda a categoria de evento **Desempenho** e marque a caixa de seleção **Perfil de estatísticas do Plano de Execução XML**. Se a categoria de evento **Performance** não estiver disponível, marque **Mostrar todos os eventos** para exibi-la.  
  
     A guia **Configurações de Extração de Eventos** é adicionada à caixa de diálogo **Propriedades do Rastreamento**.  
  
8. Na guia **Configurações de Extração de Eventos**, clique em **Salvar eventos de Plano de Execução XML separadamente**.  
  
9. Na caixa de diálogo **alvar como** , digite o nome do arquivo para armazenar os eventos **Showplan XML Statistics Profile** .  
  
10. Selecione **Todos os lotes em um único arquivo** para salvar todos os eventos de **perfil de estatísticas do Plano de Execução XML** em um único arquivo XML. Ou selecione **Cada lote de Plano de Execução XML em um arquivo distinto** para criar um novo arquivo XML para cada evento de **perfil de estatísticas do Plano de Execução XML**.  
  
11. Para exibir o arquivo do evento de **perfil de estatísticas do Plano de Execução XML** no SQL Server Management Studio, no menu **Arquivo**, aponte para **Abrir** e clique em **Arquivo**. Navegue até o diretório em que você salvou o arquivo (ou arquivos) de evento de **perfil de estatísticas do Plano de Execução XML** para selecioná-lo e abri-lo. Arquivos de evento **Showplan XML Statistics Profile** têm a extensão .SQLPlan.  
  
## <a name="see-also"></a>Confira também  
 [Analisar consultas com resultados do Plano de Execução no SQL Server Profiler](../../tools/sql-server-profiler/analyze-queries-with-showplan-results-in-sql-server-profiler.md)  
  
  
