---
title: Relatório de avaliação (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 5525d989-024c-402d-9e84-faa4721cc5b9
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: fb6d01bf9c02d0a7b96adf8e46eb354cd426db4d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68139187"
---
# <a name="assessment-report-mysqltosql"></a>Relatório de avaliação (MySQLToSQL)
A janela relatório de avaliação mostra os resultados da conversão de objetos de banco [!INCLUDE[tsql](../../includes/tsql-md.md)] de dados em sintaxe e também pode ajudá-lo a estimar a complexidade e o custo de seus projetos de migração.  
  
Para acessar o relatório de avaliação, selecione objetos a serem convertidos no Gerenciador de metadados de origem, clique com o botão direito do mouse em **esquemas**e selecione **criar relatório**.  
  
## <a name="options"></a>Opções  
  
|||  
|-|-|  
|**Termo**|**Definição**|  
|**Estatísticas de conversão**|Mostra as estatísticas de conversão por tipo de instrução. Esse painel fica visível quando um objeto de grupo, como um esquema, ou um objeto sem código é selecionado no painel esquerdo.|  
|**Objetos por categorias**|Mostra o número de objetos por categoria. Esse painel só é visível quando um objeto de grupo, como um esquema, ou um objeto sem código é selecionado no painel esquerdo.|  
|**Estatísticas**|Mostra as estatísticas de conversão para o objeto selecionado. Esse painel só é visível quando um objeto individual com código é selecionado no painel esquerdo. Talvez seja necessário expandir as **estatísticas**, que estão imediatamente acima do painel de **origem** , para exibir esse painel.|  
|**Fonte**|Mostra o código do MySQL para o objeto selecionado e realça o código que não foi convertido [!INCLUDE[tsql](../../includes/tsql-md.md)]em. Esse painel só é visível quando um objeto individual com código é selecionado no painel esquerdo.<br /><br />Clique nos números de linha para definir ou limpar os indicadores. Use os botões na parte superior do painel para navegar pelo código.|  
|**Destino**|Mostra o código resultante [!INCLUDE[tsql](../../includes/tsql-md.md)] da conversão para o objeto selecionado e mensagens de erro para o código que não foi convertido. Esse painel só é visível quando um objeto individual com código é selecionado no painel esquerdo.<br /><br />Clique nos números de linha para definir ou limpar os indicadores. Use os botões na parte superior do painel para navegar pelo código.|  
|**painel Mensagens**|Mostra os erros, avisos e mensagens informativas que foram geradas durante a criação do relatório de avaliação. As mensagens são agrupadas por número. Para exibir o código que causou o erro, clique em **erros**, **avisos**ou **informações**, expanda a categoria de mensagens e clique em uma mensagem.|  
  
