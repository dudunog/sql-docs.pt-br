---
title: Caixa de diálogo Editar propriedades da tabela (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.edittablepropdb.f1
ms.assetid: 8d913e83-7246-44cc-8fc7-31729023c0d8
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8bb8afc256881c96f70a3dd53a31e75c8fa2b5ce
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528442"
---
# <a name="edit-table-properties-dialog-box-ssas"></a>Caixa de diálogo Editar Propriedades da Tabela (SSAS)
  A caixa de diálogo **Editar Propriedades da Tabela** o habilita a exibir e modificar as propriedades de tabelas que são importadas para o designer de modelo usando o Assistente de Importação de Tabela. Para acessar essa caixa de diálogo, no designer de modelo, selecione uma tabela de dados que foi importada, clique no menu **Tabela** e em **Propriedades da Tabela**.  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
 As opções desta caixa de diálogo são diferentes, dependendo de como você importou os dados: originalmente selecionando tabelas em uma lista ou usando uma consulta SQL.  
  
## <a name="table-preview-mode"></a>Modo de visualização de tabela  
 **Nome da tabela**  
 Exibe o nome da tabela de dados no modelo.  
  
> [!NOTE]  
>  Não é possível editar o nome aqui. No entanto, você pode alterar o nome da tabela clicando com o botão direito do mouse na guia da tabela, na parte inferior do designer do modelo.  
  
 **Nome da conexão**  
 Exibe o nome da conexão que está em uso no momento.  
  
 **Nome de origem**  
 Exiba ou altere a tabela a partir da qual os dados são obtidos.  
  
 Se você alterar a origem para uma tabela que tenha colunas diferentes das da tabela atual, uma mensagem será exibida, avisando que as colunas são diferentes. Em seguida, você deve selecionar as colunas que deseja colocar na tabela atual e clicar em **Salvar**. Você pode substituir toda a tabela marcando a caixa de seleção no lado esquerdo da tabela.  
  
> [!NOTE]  
>  Quando você altera a fonte de dados de uma tabela, basicamente substitui o conteúdo da tabela atual pelo conteúdo da nova tabela de origem.  
  
 **Nomes das colunas de**  
 |||  
|-|-|  
|**Fonte**|Selecione esta opção para substituir os nomes de colunas atuais pelos nomes das colunas da tabela de origem selecionada.|  
|**Deprecia**|Selecione esta opção para usar os nomes de colunas atuais como existem no modelo.|  
  
 **Atualizar visualização**  
 Clique para exibir as colunas de dados na tabela de origem selecionada atualmente.  
  
 **Alternar para**  
 |||  
|-|-|  
|**Visualização de tabela**|Selecione esta opção para visualizar a tabela selecionada e um número limitado de linhas de dados.|  
|**Editor de consultas**|Selecione esta opção para exibir a consulta em relação à fonte de dados selecionada. Esta opção não está disponível para todas as fontes de dados.|  
  
 **Caixa de seleção no cabeçalho da coluna**  
 Marque a caixa de seleção para incluir a coluna na importação de dados. Desmarque a caixa de seleção para remover a coluna da importação de dados.  
  
 **Botão de seta para baixo no cabeçalho da coluna**  
 Filtre dados na coluna.  
  
 **Limpar filtros de linha**  
 Clique para remover os filtros que foram aplicados.  
  
 **OK**  
 Clique para aplicar todas as alterações feitas, incluindo a substituição de colunas.  
  
## <a name="query-design-mode"></a>Modo de design de consulta  
 **Nome da tabela**  
 Exibe o nome da tabela de dados no modelo.  
  
> [!NOTE]  
>  O nome não pode ser editado aqui, mas pode ser alterado clicando com o botão direito do mouse na guia da tabela, na parte inferior do designer.  
  
 **Nome da conexão**  
 Exibe o nome da conexão que está em uso no momento.  
  
 **Alternar para**  
 |||  
|-|-|  
|**Visualização de tabela**|Selecione esta opção para visualizar a tabela selecionada e algumas linhas de dados.|  
|**Editor de consultas**|Selecione esta opção para visualizar a consulta que será emitida em relação à fonte de dados selecionada.|  
  
 **Instrução Sql**  
 Exibe a instrução SQL emitida em relação à fonte de dados atual para recuperar linhas. Por padrão, todas as linhas são recuperadas, mas é possível recuperar um subconjunto de linhas, criando um filtro ou editando manualmente a instrução SQL.  
  
 **Verifica**  
 Clique para verificar se a instrução está sintaticamente correta para a fonte de dados selecionada e o provedor.  
  
 **Design**  
 Clique para abrir um designer de consulta visual e criar uma instrução de consulta. Para obter informações sobre como usar o designer, pressione F1 no designer.  
  
 **OK**  
 Clique para aplicar todas as alterações feitas, incluindo a substituição de colunas.  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas e colunas &#40;SSAS de Tabela&#41;](tabular-models/tables-and-columns-ssas-tabular.md)  
  
  
