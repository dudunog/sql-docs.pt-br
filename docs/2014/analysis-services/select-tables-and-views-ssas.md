---
title: Selecionar tabelas e exibições (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.seltablesviews.f1
ms.assetid: 5e8121cc-03f0-4168-98cf-63c5c032bb0b
author: minewiskan
ms.author: owend
ms.openlocfilehash: 354883f2bb57de348d6449dd969470483d3c5e50
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940817"
---
# <a name="select-tables-and-views-ssas"></a>Selecionar tabelas e exibições (SSAS)
  Esta página do **Assistente de Importação de Tabela** o habilita a selecionar as tabelas e exibições das quais você deseja importar dados. Para acessar o assistente do [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no menu **Modelo** , clique em **Importar de Fonte de Dados**.  
  
 A aparência de tabelas e exibições nesta página não garante que essa importação terá êxito. Se o usuário especificado na página Informações sobre Representação não tiver privilégios suficientes para ler do banco de dados selecionado, a importação falhará.  
  
 Para fontes de dados que usam a autenticação do Windows, as credenciais do usuário atual são usadas para buscar as tabelas e exibições na caixa de diálogo Selecionar Tabelas e Exibições. Para outras fontes de dados, as credenciais fornecidas na cadeia de conexão são usadas para buscar os dados.  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
 **Servidor**  
 Exibe o servidor ao qual você está conectado.  
  
 **Backup de banco de dados**  
 Exibe o banco de dados que você selecionou.  
  
 **Tabelas e Exibições**  
 Lista as tabelas e exibições no banco de dados. Marque a caixa de seleção ao lado de cada tabela e exibição que você deseja importar.  
  
 **Tabela de origem**  
 Especifica o nome da tabela de origem com base no tipo de fonte de dados.  
  
 **Esquema**  
 Especifica o esquema no qual a tabela de origem está contida. Dependendo do tipo de banco de dados, um esquema funciona como um contêiner para outros objetos, como tabelas, além de também se rpossível indicar a propriedade desses objetos.  
  
 **Nome amigável**  
 Especifica o nome amigável da tabela de origem. Por padrão, a coluna exibe o nome da tabela de origem que aparece na coluna **Tabela de Origem** . Altere o nome se você quiser usar um nome diferente do nome usado no banco de dados de origem.  
  
 **Detalhes do Filtro**  
 Quando um filtro é aplicado aos dados que estão sendo importados, exibe o filtro de importação de dados na caixa de diálogo **Detalhes do Filtro**. Para obter mais informações, consulte [Detalhes do filtro &#40;SSAS&#41;](filter-details-ssas.md).  
  
 **Visualização e Filtro**  
 Exibe a caixa de diálogo **Visualizar Tabela Selecionada**, que é usada para aplicar um filtro aos dados que estão sendo importados. Para obter mais informações, consulte [Visualizar Tabela Selecionada &#40;SSAS&#41;](preview-selected-table-ssas.md).  
  
 **Selecionar Tabelas Relacionadas**  
 Seleciona essas tabelas e exibições relacionadas a tabelas e exibições já selecionadas para importação.  
  
  
