---
title: Como localizar e exibir relatórios no portal da Web (Construtor de Relatórios) | Microsoft Docs
description: O Gerenciador de Relatórios é uma ferramenta com base na Web que inclui recursos para exibir e gerenciar relatórios. Faz parte de uma instalação do servidor de relatórios.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 8556807e-f2e2-4a7b-bb1b-ac5ea1872e51
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d3bd5691a31ebaaaf49bb5c2f8eb1357b60f6551
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "80342812"
---
# <a name="finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs"></a>Localizando e exibindo relatórios no Portal da Web (Construtor de Relatórios e SSRS)
  O Gerenciador de Relatórios é uma ferramenta com base na Web que inclui recursos para exibir e gerenciar relatórios. Faz parte de uma instalação do servidor de relatórios. Para abrir o Gerenciador de Relatórios, digite uma URL do Gerenciador de Relatórios em uma janela do navegador. Para obter mais informações sobre os requisitos de navegador, veja [Suporte ao navegador para Reporting Services e Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md). Para obter mais informações sobre como uma URL do Gerenciador de Relatórios deve ser configurada no servidor de relatório, contate o administrador de sistema. Para obter mais informações, consulte [Configurar o Gerenciador de Relatórios &#40;Modo Nativo&#41;](../../reporting-services/report-server/configure-report-manager-native-mode.md).  
  
 As permissões que administrador do sistema define no servidor de relatório determinam o que você pode ver quando usa o Gerenciador de Relatórios. São concedidas permissões por uma atribuição de função. Para localizar e exibir relatórios, sua atribuição de função deve incluir a tarefa Exibir Relatórios. Para localizar um relatório em um servidor de relatórios, procure-o por nome ou descrição ou procure as pastas do servidor de relatórios. Você só pode pesquisar ou procurar por relatórios que foram publicados ou carregados no servidor de relatórios.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="navigating-the-folder-hierarchy-in-report-manager"></a>Navegando na hierarquia de pasta no Gerenciador de Relatórios  
 Para procurar os relatórios que deseja executar, você poderá usar a página inicial, que é exibida automaticamente quando você inicia o Gerenciador de Relatórios e quando abre qualquer pasta na hierarquia de pastas. A página inicial só mostra os itens que você tem permissão de exibir. O caminho da pasta é exibido como uma linha de links na parte superior da página inicial. Os nomes de pasta são listados em sequência, começando com a pasta raiz (Base). A medida que você abre cada pasta adicional, o nome da pasta é adicionado ao caminho da pasta na parte superior da página. **(1)** na imagem abaixo. Quando você abre um relatório, o nome dele também é adicionado ao caminho da pasta.  
  
 ![Faixa de opções e navegação no Gerenciador de Relatórios](../../reporting-services/report-builder/media/rs-reportmanager-ribbon.gif "Faixa de opções e navegação no Gerenciador de Relatórios")  
Faixa de Opções do Gerenciador de Relatórios  
  
 Use as seguintes técnicas para navegar por uma hierarquia de pasta:  
  
-   Para exibir o conteúdo de uma pasta, clique no nome da pasta na página inicial. Uma página de pasta é aberta, exibindo o conteúdo da pasta.  
  
-   Para navegar pela hierarquia de pastas, abra uma subpasta da pasta atual. As pastas contêm relatórios, recursos, itens de fonte de dados compartilhados e outras pastas. Clicar em um ícone de pasta abre a pasta, mostrando o conteúdo da hierarquia um nível para baixo.  
  
-   Para navegar na hierarquia de pastas, na linha de links na parte superior da página, clique no nome da pasta cujo conteúdo deseja ver. **(1)** na imagem anterior.  
  
## <a name="opening-a-report"></a>Abrindo um relatório  
 Depois que localizar um relatório, clique no nome de relatório para abri-lo. O relatório é renderizado em HTML e é exibido na página Conteúdo no Gerenciador de Relatórios. Os relatórios são sempre armazenados em cache pela sessão do navegador para que você possa geralmente retornar a ele, clicando no botão **Voltar** . Isso é verdade mesmo que você tenha que fornecer um nome de usuário e uma senha para executar o relatório. Você não pode totalmente fechar um relatório renderizado até fechar navegador.  
  
 Nem todos os relatórios visíveis na hierarquia de pasta estão imediatamente acessíveis. Alguns relatórios podem solicitar seu nome de usuário e sua senha para determinar se você pode acessar a fonte de dados do relatório. 

 Você pode navegar até um relatório e abri-lo diretamente do servidor de relatório do Construtor de Relatórios. 
  
## <a name="to-search-for-items"></a>Para pesquisar itens  
  
-   Para procurar por itens no Gerenciador de Relatórios, digite uma cadeia de caracteres de pesquisa na caixa de texto **Pesquisar** na parte superior da página. **(2)** na imagem anterior. As pesquisas começam no nó superior na hierarquia da pasta e continua até cada ramificação. Se você não tiver permissão para acessar uma ramificação específica, essa ramificação será ignorada. Isso se aplica às pastas Meus Relatórios que pertencem a outros usuários e a outras pastas que geralmente não estão disponíveis. Somente os relatórios e itens para os quais você tem permissão para exibir são incluídos nos resultados da pesquisa.  
  
-   Para procurar por um item por nome ou descrição, especifique toda ou parte do texto que deseja coincidir. A cadeia de caracteres de pesquisa não faz distinção entre maiúsculas e minúsculas. Você não pode usar os operadores de pesquisa, como símbolos de mais (+) ou menos (-), para exigir ou excluir critérios de pesquisa.  
  
-   Para procurar um texto específico em um relatório, use a barra de ferramentas na parte superior do relatório.  
  
## <a name="see-also"></a>Consulte Também  
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
