---
title: Analisar no Excel (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 2f17b4df-eea2-48c7-a1f2-a3fb7748c15f
author: minewiskan
ms.author: owend
ms.openlocfilehash: 429245f875ce6d13ef3818cf7bae874f72c500ed
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939927"
---
# <a name="analyze-in-excel-ssas-tabular"></a>Analisar no Excel (SSAS tabular)
  O recurso Analisar no Excel, no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], fornece a autores de modelos de tabela um modo de analisar projetos de modelo rapidamente durante o desenvolvimento. O recurso Analisar no Excel abre o Microsoft Excel, cria uma conexão da fonte de dados para o banco de dados de workspace modelo e automaticamente adiciona uma Tabela Dinâmica à planilha. Os objetos de banco de dados de workspace (tabelas, colunas e medidas) são incluídos como campos na Lista de campos da Tabela Dinâmica. Os objetos e os dados podem então ser exibidos dentro do contexto do usuário efetivo ou função e perspectiva.  
  
 Este tópico pressupõe que você já esteja familiarizado com o Microsoft Excel, Tabelas Dinâmicas e Gráficos Dinâmicos. Para saber mais sobre o uso do Excel, consulte a Ajuda do Excel.  
  
 Seções neste tópico:  
  
-   [Benefícios](#bkmk_benefits)  
  
-   [Tarefas relacionadas](#bkmk_rt)  
  
##  <a name="benefits"></a><a name="bkmk_benefits"></a> Benefícios  
 O recurso Analisar no Excel fornece aos autores de modelo a capacidade para testar a eficácia de um projeto de modelo usando o aplicativo comum de análise de dados, Microsoft Excel. Para usar o recurso Analisar no Excel, você deve ter o Microsoft Office 2003 ou superior instalado no mesmo computador que o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
> [!NOTE]  
>  Se o Office não estiver instalado no mesmo computador como [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], você poderá usar o Excel em outro computador para conectar-se ao banco de dados de workspace como uma fonte de dados. Você pode então adicionar manualmente uma Tabela Dinâmica à planilha.  
  
 O recurso Analisar no Excel abre o Excel e cria uma nova pasta de trabalho do Excel (.xls). Uma conexão de dados da pasta de trabalho para o banco de dados de workspace modelo é criada. Uma Tabela Dinâmica em branco é adicionada à planilha e os metadados de objeto modelo são populados na lista de Campo de Tabela Dinâmica. Você pode então adicionar dados visíveis e segmentações de dados à Tabela Dinâmica.  
  
 Ao usar o recurso Analisar no Excel, por padrão, a conta de usuário atualmente conectada é o usuário efetivo. Esta conta é geralmente um Administrador sem restrições de exibição para objetos modelo ou dados. Porém, você pode especificar um nome de usuário ou função efetivo diferente. Isto permite que você navegue em um projeto de modelo no Excel dentro do contexto de um usuário ou função específico. Especificar o usuário efetivo inclui as opções a seguir:  
  
 **Usuário do Windows atual**  
 Usa a conta de usuário com a qual você está conectado atualmente.  
  
 **Outro usuário do Windows**  
 Usa um nome de usuário do Windows especificado em vez do usuário conectado atualmente. Usar um usuário do Windows diferente não exige uma senha. Os objetos e os dados podem somente ser exibidos no Excel dentro do contexto do nome do usuário efetivo. Nenhuma alteração a objetos modelo ou dados pode ser feita no Excel.  
  
 **Função**  
 Uma função é usada para definir permissões de usuário nos metadados de objeto e nos dados. As funções são normalmente definidas para um usuário ou grupo de usuário do Windows específico. Determinadas funções podem incluir filtros em nível de linha adicionais definidos em uma fórmula DAX. Ao usar o recurso Analisar no Excel, você pode opcionalmente selecionar uma função a ser usada. Os metadados de objeto e as exibições de dados serão restringidas pela permissão e pelos filtros definidos para a função. Para obter mais informações, consulte [Criar e gerenciar funções &#40;SSAS de Tabela&#41;](roles-ssas-tabular.md).  
  
 Além do usuário efetivo ou função, você pode especificar uma perspectiva. As perspectivas permitem que os autores do modelo definam exibições de cenário comerciais específicas de objetos modelo e dados. Por padrão, nenhuma perspectiva é usada. Para usar uma perspectiva com o Analisar no Excel, as perspectivas já devem ser definidas usando a caixa de diálogo Perspectivas no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Se uma perspectiva for especificada, a Lista de campos da Tabela Dinâmica conterá somente esses objetos selecionados na perspectiva. Para obter mais informações, consulte [criar e gerenciar perspectivas &#40;SSAS&#41;de tabela ](perspectives-ssas-tabular.md).  
  
##  <a name="related-tasks"></a><a name="bkmk_rt"></a> Tarefas relacionadas  
  
|**Tópico**|**Descrição**|  
|---------------|---------------------|  
|[Analisar um modelo de tabela no Excel &#40;SSAS de Tabela&#41;](analyze-a-tabular-model-in-excel-ssas-tabular.md)|Esse tópico descreve como usar o recurso Analisar no Excel no designer de modelo para abrir o Excel, criar uma conexão da fonte de dados para o banco de dados de workspace modelo e adicionar uma Tabela Dinâmica à planilha.|  
  
## <a name="see-also"></a>Consulte Também  
 [Analisar um modelo de tabela no Excel &#40;SSAS de tabela&#41;](analyze-a-tabular-model-in-excel-ssas-tabular.md)   
 [Funções &#40;SSAS de tabela&#41;](roles-ssas-tabular.md)   
 [Perspectivas &#40;SSAS de Tabela&#41;](perspectives-ssas-tabular.md)  
  
  
