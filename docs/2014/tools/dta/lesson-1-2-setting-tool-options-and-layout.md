---
title: Definindo opções de ferramentas e layout | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Database Engine [SQL Server], tutorials
ms.assetid: 43e97ce0-97bc-4a27-9485-5bbeb7190b85
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: de7918c382187fe4af361146bd182eecd7e30b80
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66110197"
---
# <a name="setting-tool-options-and-layout"></a>Definindo o layout e opções de ferramentas
  É possível definir as opções que configuram o que a GUI (interface gráfica do usuário) do Orientador de Otimização do Mecanismo de Banco de Dados exibe na inicialização, quais fontes ela usa e outra ferramenta de funcionalidade para oferecer o melhor suporte na hora de usá-la. As práticas nesta página irão familiarizá-lo com as opções de definição e como defini-las.  
  
### <a name="set-the-tool-options"></a>Definir as opções de ferramenta  
  
1.  Inicie o Orientador de Otimização do Mecanismo de Banco de Dados. No menu **Iniciar** do Windows, aponte para **Todos os Programas**, aponte para [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], aponte para **Ferramentas de Desempenho**e clique em **Orientador de Otimização do Mecanismo de Banco de Dados**.  
  
2.  No menu **Ferramentas** , clique em **Opções**.  
  
3.  Na caixa de diálogo **Opções** , exiba as seguintes opções:  
  
    -   Expanda a lista **Na inicialização** para exibir o que o Orientador de Otimização do Mecanismo de Banco de Dados pode exibir ao ser iniciado. Por padrão, está selecionado **Mostrar uma nova sessão** .  
  
    -   Clique em **Alterar fonte** para ver quais fontes você pode escolher para as listas de bancos de dados e tabelas na guia **geral** . As fontes escolhidas para essa opção também são usadas em Orientador de Otimização do Mecanismo de Banco de Dados grades de recomendação e relatórios depois que você tiver executado o ajuste. Por padrão, o Orientador de Otimização do Mecanismo de Banco de Dados usa fontes de sistema.  
  
    -   O **Número de itens nas listas usadas mais recentemente** pode ser definido entre **1** e **10**. Isso define o número máximo de itens nas listas exibidas ao se clicar em **Sessões Recentes** ou **Arquivos Recentes** no menu **Arquivo** . Por padrão, essa opção está definida como **4**.  
  
    -   Quando **Lembrar minhas últimas opções de ajuste** está marcada, por padrão, o Orientador de Otimização do Mecanismo de Banco de Dados usa as opções de ajuste especificadas em sua última sessão de ajuste para a próxima sessão. Desmarque essa caixa de seleção para usar as opções de ajuste padrão do Orientador de Otimização do Mecanismo de Banco de Dados. Por padrão, essa opção é selecionada.  
  
    -   Por padrão, **Perguntar antes de excluir permanentemente as sessões** está marcada para evitar excluir sessões de ajuste acidentalmente.  
  
    -   Por padrão, **Perguntar antes de parar a análise da sessão** está marcada para evitar parar uma sessão de ajuste acidentalmente antes que o Orientador de Otimização do Mecanismo de Banco de Dados termine de analisar uma carga de trabalho.  
  
## <a name="next-lesson"></a>Próxima lição  
 [Lição 2: uso do Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/database-engine-tuning-advisor.md)  
  
  
