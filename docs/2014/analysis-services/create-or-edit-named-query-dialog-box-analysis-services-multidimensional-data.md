---
title: Caixa de diálogo criar ou editar consulta nomeada (Analysis Services-dados multidimensionais) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dsvdesigner.createnamedquery.f1
helpviewer_keywords:
- Create Named Query dialog box
ms.assetid: 8e192ad6-a0b1-4e21-bb3f-087c93e62941
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97f01b0bbf3d1ddc54ea4db2b771723e12d168d7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66086806"
---
# <a name="create-or-edit-named-query-dialog-box-analysis-services---multidimensional-data"></a>Caixa de diálogo Criar/Editar Consulta Nomeada (Analysis Services - Dados Multidimensionais)
  Use a caixa de diálogo **Criar/Editar Consulta Nomeada** no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para criar ou editar uma consulta nomeada no **Designer de Exibição da Fonte de Dados**. Uma consulta nomeada pode ser tratada como uma tabela, na qual você pode basear outros objetos do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . É possível exibir a caixa de diálogo **Criar/Editar Consulta Nomeada** :  
  
-   Clicando em **Nova Consulta Nomeada** no painel **Barra de Ferramentas** do **Designer de Exibição da Fonte de Dados**.  
  
-   Clicando com o botão direito do mouse no painel **Diagrama** do **Designer de Exibição da Fonte de Dados** e selecionando **Nova Consulta Nomeada**.  
  
-   Clicando com o botão direito do mouse no nome de uma consulta nomeada no painel **Diagrama** ou **Tabelas** do **Designer de Exibição da Fonte de Dados** e selecionando **Editar Consulta Nomeada**.  
  
 A consulta digitada deve ser um comando de consulta válido para o provedor subjacente. A consulta é preparada com o provedor subjacente para validação e para identificar as colunas retornadas. A caixa de diálogo pode apresentar duas exibições:  
  
-   Construtor de Consultas VDT (Visual Database Tools)  
  
     Para todos os usuários, a exibição Construtor de Consultas VDT fornece um conjunto de ferramentas de interface do usuário para construir e testar uma consulta SQL visualmente.  
  
-   Construtor de Consultas Genérico  
  
     Para usuários avançados, a exibição Construtor de Consultas Genérico fornece uma interface do usuário mais simples e direta para construir e testar uma consulta SQL.  
  
## <a name="options"></a>Opções  
 **Nome**  
 Digite o nome da consulta.  
  
 **Descrição**  
 Digite a descrição opcional da consulta.  
  
 **Fonte de Dados**  
 Especifica a fonte de dados para a consulta.  
  
 **Definição da consulta**  
 A definição da consulta fornece uma barra de ferramentas e painéis onde definir e testar a consulta, dependendo da exibição selecionada.  
  
 **Barra**  
 Use a barra de ferramentas para gerenciar conjuntos de dados, selecionar painéis para exibição e controlar várias funções de consulta.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Alternar para Construtor de Consultas Genérico**|Selecione para exibir apenas as opções disponíveis para a exibição Construtor de Consultas Genérico. Apenas as seguintes opções são exibidas:<br />**Painel SQL**<br />**Painel de resultados**<br />**Barra de Ferramentas**, contendo apenas **Alternar para o Construtor de Consultas VDT** e **Executar**<br /><br /> <br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
|**Alternar para o Construtor de Consultas VDT**|Selecione para exibir todas as opções disponíveis para a exibição Construtor de Consultas VDT (Visual Database Tools).<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas Genérico** estiver selecionado.|  
|**Painel Mostrar/Ocultar Diagrama**|Mostra ou oculta o **painel de diagrama**.<br /><br /> **Observação** Essa opção só será exibida se **a opção Alternar para VDT Construtor de consultas** estiver selecionada.|  
|**Mostrar/Ocultar Painel Grade**|Mostra ou oculta o **painel de grade**.<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
|**Painel Mostrar/Ocultar SQL**|Mostra ou oculta o painel **SQL**.<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
|**Mostrar/Ocultar Painel Resultado**|Mostra ou oculta o painel **Resultado**.<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
|**Funcionam**|Executa a consulta. Os resultados são exibidos no **painel de resultados**.|  
|**Verificar SQL**|Verifica a instrução SQL na consulta.<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
|**Classificação crescente**|Classifica as linhas de saída na coluna selecionada no painel **Grade**, em ordem crescente.<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
|**Classificação decrescente**|Classifica as linhas de saída na coluna selecionada no painel **Grade**, em ordem decrescente.<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
|**Remover filtro**|Remove critérios de classificação, se aplicável, para a linha selecionada no painel **Grade**.<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
|**Usar Agrupar Por**|Adiciona a funcionalidade de agrupamento à consulta.<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
|**Adicionar Tabela**|Exibe a caixa de diálogo **Adicionar Tabela** para adicionar uma nova tabela ou exibição à consulta. Para obter mais informações sobre a caixa de diálogo **Adicionar Tabela**, consulte [Caixa de diálogo Adicionar Tabela &#40;Analysis Services – Dados Multidimensionais&#41;](add-table-dialog-box-analysis-services-multidimensional-data.md).<br /><br /> Observação: essa opção apenas será exibida se **Alternar para Construtor de Consultas VDT** estiver selecionado.|  
  
 **Painel de diagrama**  
 Exibe os objetos referenciados pela consulta como um diagrama. O diagrama mostra as tabelas incluídas na consulta e como elas estão unidas. Marque ou desmarque a caixa de seleção próxima a uma coluna em uma tabela para adicioná-la ou removê-la da saída da consulta.  
  
 Quando você adiciona tabelas à consulta, a caixa de diálogo cria junções entre tabelas com base nas chaves da tabela. Para adicionar uma junção, arraste um campo de uma tabela sobre um campo em outra tabela. Para gerenciar uma junção, clique com o botão direito do mouse na junção.  
  
 Clique com o botão direito do mouse no **painel Diagrama** para adicionar ou remover tabelas, selecionar todas as tabelas e mostrar ou ocultar painéis.  
  
> [!NOTE]  
>   O conteúdo do **Painel Diagrama**, **Painel Grade**e **Painel SQL** é sincronizado, de forma que as alterações feitas em um painel são refletidas nos outros dois.  
  
> [!IMPORTANT]  
>  A caixa de diálogo não oferece suporte para alteração de tipos de consulta.  
  
 **Painel Grade**  
 Exibe os objetos referenciados pela consulta em uma grade. Você pode usar este painel para adicionar e remover colunas da consulta e alterar as configurações de cada coluna.  
  
> [!NOTE]  
>   O conteúdo do **Painel Diagrama**, **Painel Grade**e **Painel SQL** é sincronizado, de forma que as alterações feitas em um painel são refletidas nos outros dois.  
  
 **Painel SQL**  
 Exibe a consulta como uma instrução SQL. Digite para alterar a instrução SQL da consulta.  
  
> [!NOTE]  
>   O conteúdo do **Painel Diagrama**, **Painel Grade**e **Painel SQL** é sincronizado, de forma que as alterações feitas em um painel são refletidas nos outros dois.  
  
 **Painel de resultados**  
 Exibe os resultados da consulta quando você clica em **Executar** no painel **Barra de Ferramentas** .  
  
## <a name="see-also"></a>Consulte Também  
 [Analysis Services designers e caixas de diálogo &#40;dados multidimensionais&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Definir consultas nomeadas em uma exibição da fonte de dados &#40;Analysis Services&#41;](multidimensional-models/define-named-queries-in-a-data-source-view-analysis-services.md)  
  
  
