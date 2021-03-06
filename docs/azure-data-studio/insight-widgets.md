---
title: Usar widgets de Insight para monitorar servidores e bancos de dados
description: Saiba como usar os widgets de insights do Azure Data Studio para transformar consultas que monitoram servidores e bancos de dados em visualizações avançadas.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, sstein
ms.custom: seodec18, sqlfreshmay19, seo-lt-2019
ms.date: 05/14/2019
ms.openlocfilehash: c93cd3ea16b87a23dac96c1f21f3720d169e8c19
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364009"
---
# <a name="manage-servers-and-databases-with-insight-widgets-in-azure-data-studio"></a>Gerenciar servidores e bancos de dados com widgets de insight no Azure Data Studio

Os widgets de insight usam as consultas Transact-SQL (T-SQL) que você usa para monitorar servidores e bancos de dados e as transforma em visualizações repletas de insights.

Os insights são quadros e gráficos personalizáveis que você adiciona aos painéis de monitoramento de servidor e de banco de dados. Veja insights rápidos sobre seus servidores e bancos de dados e, em seguida, aprofunde-se em mais detalhes e inicie as ações de gerenciamento que você definir.

Você pode criar painéis de gerenciamento de servidor e de banco de dados incríveis semelhantes ao exemplo a seguir:

![painel de banco de dados](media/insight-widgets/database-dashboard.png)

Para começar a criar diferentes tipos de widgets de insights, confira os seguintes tutoriais:

- [Criar um widget de insight personalizado](tutorial-build-custom-insight-sql-server.md)
- *Habilitar widgets de insights internos*
  - [Habilitar o insight de monitoramento de desempenho](tutorial-qds-sql-server.md)
  - [Habilitar o insight de uso de espaço de tabela](tutorial-table-space-sql-server.md)

## <a name="sql-queries"></a>Consultas SQL

O Azure Data Studio tenta evitar a introdução de mais um idioma ou uma interface do usuário pesada, assim, ele tenta usar o T-SQL o máximo possível com a configuração de JSON mínima. A configuração de widgets de insight com o T-SQL aproveita as incontáveis fontes existentes de consultas T-SQL úteis que podem ser transformadas em widgets mais sofisticados.

Os widgets de insight são compostos por uma ou duas consultas T-SQL:
* A *consulta do widget de insight* é obrigatória e é a consulta que retorna os dados que aparecem no widget.
* A *consulta de detalhes do insight* só será necessária se você estiver criando uma página de detalhes de insight.

Uma consulta do widget de insight define um conjunto de dados que renderiza uma conta, um quadro ou um gráfico. A consulta de detalhes de insights é usada para listar informações relevantes de detalhes de insight em um formato tabular no painel de detalhes do insight. 

O Azure Data Studio executa consultas do widget de insight e mapeia o conjunto de resultados da consulta para o conjunto de dados do gráfico e então o renderiza. Quando os usuários abrem os detalhes de um insight, ele executa a consulta de detalhes do insight e imprime o resultado em um modo de exibição de grade dentro da caixa de diálogo.

A ideia básica é escrever uma consulta T-SQL de forma que possa ser usada como um conjunto de dados de um widget de contagem, quadro e gráfico. 

## <a name="summary"></a>Resumo

A consulta T-SQL e seu conjunto de resultados determina o comportamento do widget do insight. Escrever uma consulta para um tipo de gráfico ou mapear um tipo de gráfico correto para a consulta existente é a principal consideração para criar um widget de insight eficaz.



## <a name="additional-resources"></a>Recursos adicionais
- [Editor de Consultas](tutorial-sql-editor.md)

