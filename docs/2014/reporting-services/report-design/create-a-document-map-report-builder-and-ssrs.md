---
title: Criar um mapa do documento (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: c200a97b-67f2-499f-8374-3ed1ebe3f33c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 99456151a71e74d0e85baec19cc42d8450c00ae4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106173"
---
# <a name="create-a-document-map-report-builder-and-ssrs"></a>Criar um mapa de documentos (Construtor de Relatórios e SSRS)
  O mapa do documento fornece um conjunto de links de navegação aos itens de relatório em um relatório renderizado. Ao exibir um relatório que inclui um mapa do documento, um painel lateral separado é exibido ao lado do relatório. Um usuário pode clicar nos links do mapa do documento para ir para a página de relatório que exibe esse item. Seções e grupos de relatórios são organizados em uma hierarquia de links. Clicar nos itens do mapa do documento atualiza o relatório e exibe a área do relatório que corresponde ao item no mapa do documento.  
  
 Para adicionar links ao mapa do documento, defina a propriedade `DocumentMapLabel` do item de relatório para o texto que você criar ou para uma expressão que seja avaliada como o texto que você deseja exibir no mapa do documento. Você também pode adicionar valores exclusivos ao grupo de tabelas ou matrizes para o mapa do documento. Por exemplo, para um grupo com base em cores, cada cor exclusiva tem um link que o direciona para a página do relatório que exibe a instância de grupo daquela cor.  
  
 Também é possível criar uma URL para um relatório que substitui a exibição do mapa do documento, portanto, você poderá executar o relatório sem exibir o mapa do documento e clicar no botão **Mostrar/Ocultar Mapa do Documento** na barra de ferramentas do visualizador de relatórios para alternar a exibição.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="document-maps-and-rendering-extensions"></a><a name="DocMapRenderExtensions"></a> Mapas do documento e extensões de renderização  
 O mapa do documento é planejado para uso na extensão de renderização HTML, por exemplo, na Versão prévia e no Visualizador de Relatórios. Outras extensões de renderização têm maneiras diferentes de articular um mapa do documento:  
  
-   O PDF renderiza o mapa do documento como painel de Indicações.  
  
-   O Excel renderiza um mapa do documento como uma planilha nomeada que inclui uma hierarquia de links. As seções de relatórios são renderizadas em planilhas separadas incluídas com o mapa do documento na mesma pasta de trabalho.  
  
-   O Word inclui um mapa do documento como o sumário.  
  
-   Atom, TIFF, XML e CSV ignoram os mapas dos documentos.  
  
 Para obter mais informações, consulte [Funcionalidade interativa para extensões de renderização de relatório diferentes &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/interactive-functionality-different-report-rendering-extensions.md).  
  
##  <a name="AddRptItemToMap"></a>   
#### <a name="to-add-a-report-item-to-a-document-map"></a>Para adicionar um item de relatório a um mapa do documento  
  
1.  No modo de exibição Design, selecione o item de relatório (por exemplo, tabela, matriz ou medidor) que você deseja adicionar ao mapa do documento. As propriedades do item de relatório aparecem no painel Propriedades.  
  
    > [!NOTE]  
    >  Para selecionar uma região de dados tablix, clique em uma célula para exibir as alças de linha e coluna e, em seguida, clique na alça de canto.  
  
2.  No painel Propriedades, digite o texto que você deseja que apareça no mapa do documento na `DocumentMapLabel` propriedade ou insira uma expressão que seja avaliada como um rótulo. Por exemplo, digite **Gráfico de Vendas**.  
  
    > [!NOTE]  
    >  Se você não vir o painel Propriedades, na guia **Exibir** , no grupo **Mostrar/Ocultar** , clique em **Propriedades**.  
  
3.  Repita as etapas 1 e 2 para cada item de relatório que você deseja exibir no mapa do documento.  
  
4.  Clique em **Executar**. O relatório é executado e o mapa do documento exibe os rótulos criados. Clique em qualquer link para ir para a página do relatório relacionada ao item.  
  
 
  
##  <a name="AddUniqueValuesToMap"></a>   
#### <a name="to-add-unique-group-values-to-a-document-map"></a>Para adicionar valores de grupo exclusivos a um mapa do documento  
  
1.  Na exibição Design, selecione a tabela, matriz ou lista que contém o grupo que você deseja exibir no mapa do documento. O painel Agrupamento exibe os grupos de linhas e colunas.  
  
2.  No painel Grupos de Linhas, clique com o botão direito do mouse no grupo e escolha **Editar Grupo**. A página **Geral** da caixa de diálogo **Propriedades do Grupo Tablix** é aberta.  
  
3.  Clique em **Avançado**.  
  
4.  Na caixa de lista **Mapa do Documento** , digite ou selecione uma expressão que corresponda à expressão do grupo.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Repita as etapas 1 a 4 para cada grupo que você deseja exibir no mapa do documento.  
  
7.  Clique em **Executar**. O relatório é executado e o mapa do documento exibe os valores do grupo. Clique em qualquer link para ir para a página do relatório relacionada ao item.  
  
 
  
##  <a name="HideMapWhenViewRpt"></a>   
#### <a name="to-hide-the-document-map-when-you-view-a-report"></a>Para ocultar o mapa do documento quando exibir um relatório  
  
1.  No Gerenciador de Relatórios, navegue até o relatório que contém o mapa do documento.  
  
     Por exemplo, para os relatórios de exemplo em [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] , a URL a seguir especifica o relatório chamado Catálogo de Produtos.  
  
    ```  
    http://localhost/Reports/Pages/Report.aspx?ItemPath=%2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog  
    ```  
  
2.  Copie o caminho do relatório no servidor. No exemplo, o caminho do relatório é `%2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog`.  
  
3.  Crie uma nova URL com os três componentes a seguir:  
  
    -   O visualizador de relatórios no servidor de relatórios: `http://localhost/ReportServer/Pages/ReportViewer.aspx?`  
  
    -   O nome do relatório que você copiou na etapa 1, por exemplo: `%2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog`  
  
    -   Os parâmetros de informação do dispositivo que especificam se o mapa do documento será ocultado: `&rs%3aCommand=Render&rc%3aFormat=HTML4.0&rc%3aDocMap=False`  
  
     A URL a seguir é composta por esses três componentes anexos na ordem em que foram listados.  
  
    ```  
    http://localhost/ReportServer/Pages/ReportViewer.aspx?  
    %2fAdventureWorks2012+Sample+Reports%2fProduct+Catalog  
    &rs%3aCommand=Render&rc%3aFormat=HTML4.0&rc%3aDocMap=False  
    ```  
  
     Para usar essa URL, copie-a e remova todas as quebras de linha.  
  
4.  Cole a URL no Gerenciador de Relatórios e pressione ENTER. O relatório será executado e o mapa do documento será ocultado.  
  
> [!NOTE]  
>  Para obter mais informações sobre como baixar relatórios de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]exemplo, consulte [Construtor de relatórios e Report Designer relatórios de exemplo](https://go.microsoft.com/fwlink/?LinkId=198283).  
>   
>  Para obter mais informações, consulte “Acesso à URL” na [documentação do Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) nos Manuais Online do SQL Server.  
  
 
  
## <a name="see-also"></a>Consulte Também  
 [Localizando e exibindo relatórios no Gerenciador de Relatórios &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md)  
  
  
