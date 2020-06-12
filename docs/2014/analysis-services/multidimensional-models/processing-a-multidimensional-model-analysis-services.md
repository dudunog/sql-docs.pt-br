---
title: Processamento de objeto de modelo multidimensional | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- online mode [Analysis Services]
- processing objects [Analysis Services]
- partitions [Analysis Services], processing
- jobs [Analysis Services]
- objects [Analysis Services], processing
- reprocessing objects
- impact analysis [Analysis Services]
- dimensions [Analysis Services], processing
- project mode [Analysis Services]
- cubes [Analysis Services], processing
ms.assetid: 625aa5a6-aa09-4bac-be8a-778fa81c5a61
author: minewiskan
ms.author: owend
ms.openlocfilehash: caf111b2d78032b0a127f978562b2e0138df0109
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545789"
---
# <a name="multidimensional-model-object-processing"></a>Processamento de objetos de modelo multidimensional
  O processamento é a etapa ou uma série de etapas nas quais o Analysis Services carrega dados de uma fonte de dados relacional para um modelo multidimensional. Para objetos que usam o armazenamento MOLAP, os dados são salvos em disco na pasta do arquivo de banco de dados. No armazenamento ROLAP, o processamento ocorre sob demanda, em resposta a uma consulta MDX sobre um objeto. Para objetos que usam armazenamento ROLAP, o processamento refere-se à atualização do cache antes de retornar os resultados da consulta.  
  
 Por padrão, o processamento ocorre quando você implanta uma solução no servidor. Você também pode processar toda a solução ou parte dela, usando ferramentas ad hoc como o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ou [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], ou em um agendamento usando o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e o SQL Server Agent. Ao fazer uma alteração estrutural no modelo, como remover uma dimensão ou alterar seu nível de compatibilidade, você precisará processar novamente para sincronizar os aspectos físicos e lógicos do modelo.  
  
 Este tópico inclui as seções a seguir:  
  
 [Pré-requisitos](#bkmk_prereq)  
  
 [Escolhendo uma ferramenta ou abordagem](#bkmk_tool)  
  
 [Processando objetos](#bkmk_proc)  
  
 [Reprocessando objetos](#bkmk_reproc)  
  
##  <a name="prerequisites"></a><a name="bkmk_prereq"></a> Pré-requisitos  
  
-   O processamento exige permissões administrativas na instância do Analysis Services. Se você estiver processando interativamente do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ou [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], deverá ser um membro da função de administrador do servidor na instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Para processamento que é executado de modo autônomo, por exemplo, usando um pacote de SSIS que você agenda por meio do SQL Server Agent, a conta usada para executar o pacote deverá ser um membro da função de administrador do servidor. Para obter mais informações sobre como definir permissões de administrador, consulte [permissões de administrador do servidor de concessão &#40;Analysis Services&#41;](../instances/grant-server-admin-rights-to-an-analysis-services-instance.md).  
  
-   A conta usada para recuperar dados é especificada no objeto de fonte de dados, como uma opção de representação se você estiver usando a autenticação do Windows, ou como o nome de usuário na cadeia de conexão se estiver usando a autenticação de banco de dados. A conta deve ter permissões de leitura nas fontes de dados relacionais usadas pelo modelo.  
  
-   O projeto ou a solução devem ser implantados antes de você poder processar objetos.  
  
     Inicialmente, durante as fases iniciais do desenvolvimento do modelo, a implantação e o processamento ocorrem juntos. Porém, você pode definir opções para processar o modelo posteriormente, depois que implantar a solução. Para obter mais informações sobre a implantação, consulte [Implantar projetos do Analysis Services &#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md).  
  
##  <a name="choosing-a-tool-or-approach"></a><a name="bkmk_tool"></a>Escolhendo uma ferramenta ou abordagem  
 Você pode processar objetos usando um aplicativo cliente, como o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] ou o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], interativamente ou uma operação de script executada como um trabalho do SQL Server Agent ou um pacote do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 O modo de processamento de um banco de dados varia consideravelmente dependendo se o modelo está em desenvolvimento ativo ou em produção. Quando um modelo é implantado em um servidor de produção, o processamento deve ser controlado atentamente para assegurar a integridade e a disponibilidade de dados multidimensionais. Como os objetos são interdependentes, o processamento normalmente tem um efeito em cascata no modelo já que outros objetos também são processados ou não processados em tandem. Se alguns objetos permanecerem em estado não processado, as consultas desses dados não serão resolvidas, corrompendo os relatórios ou aplicativos que os usam. Para desenvolver uma estratégia de processamento de um banco de dados de produção, considere usar script ou pacotes do [!INCLUDE[ssIS](../../includes/ssis-md.md)] depurados e testados para evitar erro de operador ou etapas ignoradas.  
  
 Para obter mais informações, consulte [Ferramentas e abordagens para processamento &#40;Analysis Services&#41;](tools-and-approaches-for-processing-analysis-services.md).  
  
##  <a name="processing-objects"></a><a name="bkmk_proc"></a>Processando objetos  
 O processamento afeta os seguintes objetos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] : grupos de medidas, partições, dimensões, cubos, modelos de mineração, estruturas de mineração e bancos de dados. Quando um objeto contém um ou mais objetos, processar o objeto de nível mais elevado causa uma cascata de processamento de todos os objetos de nível inferior. Por exemplo, um cubo contém normalmente um ou mais grupos de medidas (cada um dos quais contém uma ou mais partições) e dimensões. O processamento de um cubo causa o processamento de todos os grupos de medidas dentro do cubo e das dimensões constituintes que estão atualmente em estado não processado. Para obter mais informações sobre o processamento de objetos [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , consulte [Processamento de objetos do Analysis Services](processing-analysis-services-objects.md).  
  
 Enquanto a tarefa de processamento estiver funcionando, os objetos afetados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] podem ser acessados para consulta. A tarefa de processamento trabalha dentro de uma transação e a transação pode ser confirmada ou revertida. Se a tarefa de processamento falhar, a transação será revertida. Se a tarefa de processamento tiver êxito, um bloqueio exclusivo será colocado no objeto quando as mudanças estiverem sendo confirmadas, significando que o objeto estará temporariamente indisponível para consulta ou processamento. Durante a fase de confirmação da transação, as consultas ainda podem ser enviadas ao objeto, mas elas serão enfileiradas até que a confirmação esteja concluída.  
  
 Durante uma tarefa de processamento, se um objeto é processado e como ele será processado, depende da opção de processamento definida para esse objeto. Para obter mais informações sobre as opções de processamento específicas que podem ser aplicadas a cada objeto, consulte [Processamento de opções e configurações &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md).  
  
##  <a name="reprocessing-objects"></a><a name="bkmk_reproc"></a>Reprocessando objetos  
 Cubos que contêm elementos não processados têm que ser reprocessados antes de poderem ser navegados. Cubos no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] contêm grupos de medidas e partições que devem ser processados antes de o cubo ser consultado. O processamento de um cubo fará com que o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] processe dimensões constituintes do cubo se essas dimensões estiverem em estado não processado. Depois do primeiro processamento de um objeto, ele deverá ser reprocessado parcialmente ou por completo sempre que ocorrer uma das seguintes situações:  
  
-   A estrutura do objeto é alterada, como descartar uma coluna em uma tabela de fato.  
  
-   O design de agregação para o objeto é alterado.  
  
-   Os dados do objeto precisam ser atualizados.  
  
 Quando você processar objetos no [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], você pode selecionar uma opção de processamento ou pode habilitar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para determinar o tipo apropriado de processamento. Os métodos de processamento disponibilizados diferem de um objeto para outro e são baseados no tipo de objeto. Adicionalmente, os métodos disponíveis são baseados nas alterações que ocorreram no objeto desde o último processamento. Se você habilitar o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para selecionar automaticamente um método de processamento, ele usará o método que retornar o objeto a um estado inteiramente processado no menor tempo. Para obter mais informações, consulte [Opções e configurações de processamento &#40;Analysis Services&#41;](processing-options-and-settings-analysis-services.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Arquitetura lógica &#40;Analysis Services de dados multidimensionais&#41;](olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [Objetos de banco de dados &#40;Analysis Services – Dados Multidimensionais&#41;](olap-logical/database-objects-analysis-services-multidimensional-data.md)  
  
  
