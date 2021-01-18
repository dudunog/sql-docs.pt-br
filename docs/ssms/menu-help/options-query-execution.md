---
title: Página de opções de SQL Server – Execução de consulta
description: Opções (Execução de consulta)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Query_Execution.Sql_Server.General
dev_langs:
- TSQL
author: markingmyname
ms.author: maghan
ms.date: 01/13/2021
ms.openlocfilehash: 25ac37cdb9095151c90fdf81314d4c32044e6159
ms.sourcegitcommit: af64e2b8d498af26b973e86db5c00f8d72991295
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98193123"
---
# <a name="query-options-execution-general-page"></a>Execução de Opções de Consultas (página Geral)

Use esta página para especificar as opções para executar consultas do Microsoft SQL Server. Para acessar essa caixa de diálogo, clique com o botão direito do mouse no corpo de uma janela do Editor de Consultas e, então, clique em Opções de Consultas.

- **SET ROWCOUNT** O valor padrão de 0 indica que o SQL Server esperará os resultados até que todos os resultados sejam recebidos. Forneça um valor maior que 0 se você quiser que o SQL Server interrompa a consulta depois de obter o número especificado de linhas. Para desligar essa opção (de forma que todas as linhas sejam retornadas), especifique SET ROWCOUNT 0.

- **SET TEXTSIZE** O valor padrão de 2.147.483.647 bytes indica que o SQL Server fornecerá um campo de dados completo até o limite dos campos de dados text, ntext, nvarchar(max) e varchar(max). Não afeta o tipo de dados XML. Forneça um número menor para limitar os resultados no caso de valores grandes. Colunas maiores que o número fornecido serão truncadas.

- **Tempo limite de execução** Indica o número de segundos de espera antes de cancelar a consulta. Um valor 0 indica uma espera infinita ou nenhum tempo limite.

- **Separador de lote** Digite uma palavra que você usa para separar instruções Transact-SQL em lotes. O padrão é GO.

- **Por padrão, abra consultas novas no Modo SQLCMD** Marque esta caixa de seleção para abrir novas consultas no modo SQLCMD. Essa caixa de seleção só é visível quando a caixa de diálogo é aberta pelo menu Ferramentas.

    Ao selecionar essa opção, esteja atento às seguintes limitações:

    - O IntelliSense no Editor de Consulta do Mecanismo de Banco de Dados está desativado.

    - Como o Editor de Consultas não é executado na linha de comando, você não pode passar parâmetros de linha de comando, como variáveis.

    - Como o Editor de Consultas não pode responder a prompts do sistema operacional, você deve ter cuidado para não executar instruções interativas.

- **Restaurar Padrões** Redefine todos os valores dessa página com os valores padrão originais.