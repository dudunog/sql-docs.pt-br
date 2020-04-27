---
title: Projeto de scripts de Analysis Services no SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- scripts [Analysis Services]
- scripts [Analysis Services], projects
- projects [Analysis Services], Analysis Server Scripts project
- projects [Analysis Services], creating
- Analysis Server Scripts project
- items [Analysis Services]
ms.assetid: c4f5a06b-e2e4-4660-a3a8-6fd356742c02
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c0bcc06655333dfef073757218d9a740c1dfb0dd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66080363"
---
# <a name="analysis-services-scripts-project-in-sql-server-management-studio"></a>Projeto de scripts do Analysis Services no SQL Server Management Studio
  No [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você pode criar um projeto do Analysis Server Scripts no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para agrupar scripts relacionados para uso em desenvolvimento, gerenciamento e controle do código-fonte. Se não houver uma solução carregada no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], a criação de um novo projeto do Analysis Server Scripts criará automaticamente uma nova solução. Caso contrário, o novo projeto do Analysis Server Scripts pode ser adicionado à solução existente ou criado em uma solução nova.  
  
 Siga estas etapas básicas para criar um projeto do Analysis Server Scripts no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:  
  
1.  No menu Arquivo , aponte para **Novo**e clique em **Projeto**.  
  
     Selecione o modelo de projeto **Scripts do Analysis Server** e especifique um nome e um local para o novo projeto.  
  
2.  Clique com o botão direito do mouse em **Conexões** para criar uma nova conexão na pasta Conexões do projeto do Analysis Server Scripts no Gerenciador de Soluções.  
  
     Esta pasta contém cadeias de conexão com instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , nas quais os scripts contidos no projeto do Analysis Server Scripts podem ser executados. Podem existir várias conexões em um projeto do Analysis Server Scripts e você pode escolher uma delas para executar um script contido no projeto no momento da execução.  
  
3.  Clique com o botão direito do mouse em **Consultas** para criar scripts MDX (expressão MDX), DMX (extensões DMX) e XMLA (XML for Analysis) na pasta Scripts do projeto do Analysis Server Scripts no Gerenciador de Soluções. Para obter mais informações, consulte [Script de tarefas administrativas no Analysis Services](../script-administrative-tasks-in-analysis-services.md).  
  
4.  Clique com o botão direito do mouse no projeto, aponte para **Adicionar**e selecione **Item Existente** para adicionar arquivos diversos, como arquivos de texto com observações sobre o projeto, na pasta **Diversos** do Analysis Server Scripts no Gerenciador de Soluções. Esses arquivos são ignorados pelo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="file-types"></a>Tipos de arquivo  
 A solução do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] pode conter vários tipos de arquivo, dependendo dos projetos incluídos nela e de seus itens. Para obter mais informações sobre tipos de arquivo para soluções em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], consulte [Arquivos que gerenciam soluções e projetos](../../ssms/solution/files-that-manage-solutions-and-projects.md). Em geral, os arquivos de cada projeto de uma solução do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] são armazenados na pasta da solução, em uma pasta separada para cada projeto.  
  
 A pasta de um projeto do Analysis Server Scripts pode conter os tipos de arquivo listados na tabela a seguir.  
  
|Tipo de arquivo|Descrição|  
|---------------|-----------------|  
|Arquivo de definição do projeto do Analysis Server Scripts (.ssmsasproj)|Contém metadados sobre as pastas mostradas no Gerenciador de Soluções, além de informações que indicam quais pastas devem exibir os arquivos incluídos no projeto.<br /><br /> O arquivo de definição do projeto também contém os metadados das conexões do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contidas no projeto, além dos metadados que associam conexões aos arquivos de script incluídos no projeto.|  
|Arquivo de script DMX (.dmx)|Contém um script DMX incluído no projeto.|  
|Arquivo de script MDX (.mdx)|Contém um script MDX incluído no projeto.|  
|Arquivo de script XMLA (.xmla)|Contém um script XMLA incluído no projeto.|  
  
## <a name="analysis-services-templates"></a>Modelos do Analysis Services  
 Ao adicionar novos scripts MDX, DMX ou XMLA a um projeto do Analysis Server Scripts, você tem a opção de usar o Explorador de Modelos para localizar os modelos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , uma coleção de scripts ou instruções predefinidos(as) que demonstram como executar a ação especificada. O Gerenciador de modelos está disponível no menu **Exibir** e inclui modelos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]o, [!INCLUDE[ssEW](../../includes/ssew-md.md)]o e o. Para obter mais informações, consulte [Usar modelos do Analysis Services no SQL Server Management Studio](use-analysis-services-templates-in-sql-server-management-studio.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criando modelos multidimensionais usando o SQL Server Data Tools &#40;SSDT&#41;](../multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)   
 [Expressões multidimensionais &#40;referência de&#41; MDX](/sql/mdx/multidimensional-expressions-mdx-reference)   
 [Referência de&#41; &#40;DMX de extensões de mineração de dados](/sql/dmx/data-mining-extensions-dmx-reference)   
 [Analysis Services linguagem de script &#40;referência de&#41; do ASSL](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [Analysis Services linguagem de script &#40;referência de&#41; do ASSL](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)  
  
  
