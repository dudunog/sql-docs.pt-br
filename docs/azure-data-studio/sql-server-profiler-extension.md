---
title: Extensão do SQL Server Profiler
description: Instale e use a extensão do SQL Server Profiler (versão prévia) para o Azure Data Studio
ms.custom: seodec18
ms.date: 09/24/2018
ms.reviewer: alayu, maghan, sstein
ms.prod: azure-data-studio
ms.technology: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: f86257f7d024d36109901e09f11ab910525810e5
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85758312"
---
# <a name="sql-server-profiler-extension-preview"></a>Extensão do SQL Server Profiler (versão prévia)

A extensão do SQL Server Profiler (versão prévia) fornece uma solução de rastreamento de SQL Server simples semelhante ao SSMS (SQL Server Management Studio) Profiler, porém criada usando os Eventos Estendidos. O SQL Server Profiler é muito fácil de usar e tem bons valores padrão para as configurações de rastreamento mais comuns. A experiência do usuário é otimizada para navegar por eventos e exibir o texto de Transact-SQL (T-SQL) associado. O SQL Server Profiler para Azure Data Studio também assume bons valores padrão para coletar atividades de execução de T-SQL com uma experiência do usuário fácil de usar. Esta extensão está em versão prévia.

**Casos de uso comuns do SQL Profiler:**

- Percorrer consultas de problemas para localizar a causa do problema.
- Localizar e diagnosticar consultas de execução lenta.
- Capturar a série de instruções Transact-SQL que resultam em um problema.
- Monitorar o desempenho do SQL Server para ajustar cargas de trabalho.
- Correlacionar contadores de desempenho para diagnosticar problemas.


## <a name="install-the-sql-server-profiler-extension"></a>Instalar a extensão do SQL Server Profiler

1. Para abrir o gerenciador de extensões e acessar as extensões disponíveis, selecione o ícone de extensões ou selecione **Extensões** no menu **Exibir**.
2. Selecione uma extensão disponível para exibir os detalhes.

   ![gerenciador da extensão do profiler](media/extensions/sql-server-profiler-extension/profiler-extension.png)

1. Selecione a extensão que você deseja e **Instale**-a.
2. Selecione **Recarregar** para habilitar a extensão (necessário apenas na primeira vez que você instala uma extensão).

## <a name="start-profiler"></a>Iniciar o Profiler

1. Para iniciar o Profiler, primeiro faça uma conexão com um servidor na guia Servidores.
2. Depois de fazer uma conexão, digite **Alt + P** para iniciar o Profiler.
3. Para iniciar o Profiler, digite **Alt + S**. Agora, você pode começar a ver os Eventos Estendidos.
    ![gerenciador da extensão do profiler](media/extensions/sql-server-profiler-extension/view-profiler.png)    
1. Para interromper o Profiler, digite **Alt + S.** Essa tecla de atalho é de alternância.

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre o Profiler e sobre eventos estendidos, confira [Eventos Estendidos](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events).





