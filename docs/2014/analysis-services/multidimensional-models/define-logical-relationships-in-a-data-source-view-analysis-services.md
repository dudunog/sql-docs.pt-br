---
title: Definir relações lógicas em uma exibição da fonte de dados (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- adding relationships
- relationships [Analysis Services], data source views
- data source views [Analysis Services], relationships
ms.assetid: a20d6dae-e769-4131-8a59-7ef56f174220
author: minewiskan
ms.author: owend
ms.openlocfilehash: a356fa721f6e95289ab92579bbc580900f32f507
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546968"
---
# <a name="define-logical-relationships-in-a-data-source-view-analysis-services"></a>Definir relações lógicas em uma exibição da fonte de dados (Analysis Services)
  O Assistente de Exibição da Fonte de Dados e o Designer de Exibição da Fonte de Dados definem relações entre as tabelas adicionadas a uma DSV (exibição da fonte de dados) com base nas relações do banco de dados subjacente ou nos critérios de correspondência de nomes que você especificar.  
  
 Nos casos em que você está trabalhando com dados de diversas fontes de dados, pode ser necessário definir manualmente relações lógicas na DSV (exibição da fonte de dados) para complementar essas relações que são definidas automaticamente. O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] precisa de relações para identificar tabelas de fatos e dimensões, construir consultas para recuperar dados e metadados de fontes de dados subjacentes e aproveitar os recursos avançados de business intelligence.  
  
 Você pode definir os tipos de relações a seguir no Designer de Exibição da Fonte de Dados:  
  
-   Uma relação de uma tabela para outra na mesma fonte de dados.  
  
-   Uma relação de uma tabela para ela mesma, como em uma relação pai-filho.  
  
-   Uma relação de uma tabela de uma fonte de dados para outra tabela de outra fonte de dados.  
  
> [!NOTE]  
>  As relações definidas em uma DSV são lógicas e não podem refletir as relações atuais definidas na fonte de dados subjacente. É possível criar relações no Designer de Exibição da Fonte de Dados que não existem na fonte de dados subjacente e remover relações criadas pelo Designer da Exibição da Fonte de Dados a partir de relações de chave estrangeira existentes na fonte de dados subjacente.  
  
 As relações são direcionadas. Para cada valor da coluna de origem, existe um valor correspondente na coluna de destino. Em um diagrama da exibição da fonte de dados, como os diagramas exibidos no painel **Diagrama** , uma seta na linha entre duas tabelas indica a direção da relação.  
  
 Este tópico inclui as seções a seguir:  
  
 [Adicionar uma relação entre tabelas, consultas nomeadas ou exibições](#bkmk_addRel)  
  
 [Para exibir ou modificar uma relação no painel diagrama](#bkmk_diagrampane)  
  
 [Para exibir ou modificar uma relação no painel tabelas](#bkmk_tablespane)  
  
##  <a name="to-add-a-relationship-between-tables-named-queries-or-views"></a><a name="bkmk_addRel"></a>Para adicionar uma relação entre tabelas, consultas nomeadas ou exibições  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto ou conecte-se ao banco de dados que contém a exibição da fonte de dados à qual você deseja adicionar uma relação lógica.  
  
2.  No Gerenciador de Soluções, expanda a pasta **Exibições da Fonte de Dados** e clique duas vezes na exibição da fonte de dados para abri-la no **Designer de Exibição da Fonte de Dados**.  
  
3.  Clique com o botão direito do mouse na tabela, consulta nomeada ou exibição a que você deseja adicionar uma relação no painel **Tabelas** e, em seguida, clique em **Nova Relação**.  
  
    > [!NOTE]  
    >  Para localizar uma tabela, exibição ou consulta nomeada, use a opção **Localizar Tabela** clicando no menu **Exibição da Fonte de Dados** ou clicando com o botão direito do mouse em uma área livre do painel **Tabelas** ou de **Diagrama** .  
  
4.  Na caixa de diálogo **Especificar Relação** , faça o seguinte:  
  
    1.  Selecione a tabela, consulta nomeada ou exibição apropriada na lista **Tabela de origem (chave estrangeira)** .  
  
    2.  Selecione a tabela, consulta nomeada ou exibição apropriada na lista **Tabela de destino (chave primária)** .  
  
    3.  Selecione as colunas nas listas **Colunas de Origem** e **Colunas de Destino** para criar uma relação entre as duas tabelas.  
  
         Se o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] detectar, pela amostragem dos dados da tabela, exibição ou consulta nomeada subjacente, que você definiu a relação na direção errada (da chave primária para a chave estrangeira em vez do contrário), será solicitada a inversão da ordem. Para invertê-la rapidamente, clique em **Inverter**.  
  
         Se o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] detectar que já existe uma relação entre as colunas selecionadas, você será avisado. Não é possível definir relações duplicadas.  
  
    4.  Opcionalmente, na caixa **Descrição** , digite uma descrição para a relação.  
  
##  <a name="to-view-or-modify-a-relationship-in-the-diagram-pane"></a><a name="bkmk_diagrampane"></a> Para exibir ou modificar uma relação no painel de Diagrama  
  
-   No painel **Diagrama** no **Designer de Exibição da Fonte de Dados**, clique com o botão direito do mouse na relação que você deseja exibir e clique em **Editar Relação** (ou simplesmente clique duas vezes na seta da relação).  Use a caixa de diálogo **Editar Relação** para modificar a relação.  
  
##  <a name="to-view-or-modify-a-relationship-in-the-tables-pane"></a><a name="bkmk_tablespane"></a> Para exibir ou modificar uma relação no painel de Tabelas  
  
1.  No painel **Tabelas** no **Designer de Exibição da Fonte de Dados**, localize e expanda a tabela, exibição ou consulta nomeada que contém a relação que você deseja exibir ou modificar.  
  
2.  Expanda a pasta **Relações** .  As relações entre a tabela, exibição ou consulta nomeada selecionada e outras tabelas, exibições ou consultas nomeadas aparecem com a coluna de relações listada.  
  
3.  Clique com o botão direito do mouse na relação que você deseja modificar e, em seguida, clique em **Editar Relação**.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de fontes de dados em modelos multidimensionais](data-source-views-in-multidimensional-models.md)  
  
  
