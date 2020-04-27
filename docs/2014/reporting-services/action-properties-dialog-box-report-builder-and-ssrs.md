---
title: Caixa de diálogo Propriedades da ação (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.shared.action.f1
- "10413"
- "10504"
- sql12.rtp.rptdesigner.calculatedseriesproperties.action.f1
- sql12.rtp.rptdesigner.pictureproperties.action.f1
- sql12.rtp.rptdesigner.actionproperties.f1
- sql12.rtp.rptdesigner.charttitleproperties.action.f1
- "10133"
- "10052"
- "10147"
- sql12.rtp.rptdesigner.chartproperties.action.f1
- "10122"
- sql12.rtp.rptdesigner.serieslabelproperties.action.f1
- sql12.rtp.rptdesigner.textboxproperties.action.f1
- "10162"
- "10168"
- sql12.rtp.rptdesigner.textproperties.action.f1
- sql12.rtp.rptdesigner.placeholderproperties.action.f1
- "10250"
- "10129"
- "10244"
- sql12.rtp.rptdesigner.seriesproperties.action.f1
ms.assetid: 2c5d915b-4f97-42cf-b8f1-49ca3ff3d0f9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3d6069d5720121b02c627528ec772cb61ddb0a10
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66110079"
---
# <a name="action-properties-dialog-box-report-builder-and-ssrs"></a>Caixa de diálogo Propriedades de Ação (Construtor de Relatórios e SSRS)
  A caixa de diálogo **Ação** pode ser usada para habilitar opções de hiperlink para um gráfico, um medidor e elementos de mapa com suporte para links. Defina uma ação para que um usuário possa clicar no relatório e vincular a uma URL, para um relatório diferente no mesmo servidor de relatório ou em um site do SharePoint integrado a um servidor de relatório ou para um local diferente no mesmo relatório.  
  
## <a name="options"></a>Opções  
 **Habilitar como uma ação**  
 Selecione uma opção para indicar a ação que será executada quando o usuário clicar no item.  
  
 **Nenhum**  
 Escolha esta opção para indicar que o item não tem nenhuma ação.  
  
 **Ir para o relatório**  
 Escolha esta opção para criar um link para um relatório detalhado localizado em um servidor de relatório. As opções adicionais a seguir aparecem quando você seleciona **Ir para o relatório**.  
  
 **Especifique um relatório**  
 Digite ou selecione o nome do relatório que você deseja usar como um relatório detalhado. Relatórios detalhados devem estar no mesmo servidor de relatório que esse relatório.  
  
 Em um relatório publicado em um servidor de relatório configurado para o modo nativo, use um caminho completo ou relativo sem a extensão do nome de arquivo. Se o relatório estiver na mesma pasta do relatório atual, use apenas o nome do relatório. Se o relatório estiver em outra pasta no mesmo servidor de relatório, use um caminho relativo ou um caminho completo. Um caminho relativo inicia na pasta atual e é movido para cima na hierarquia de pastas, por exemplo,../Folder2/Report1. Um caminho completo inicia em /, a pasta base. Por exemplo, /Reports/Report1.  
  
 Para um relatório publicado em um servidor de relatórios configurado para o modo integrado do SharePoint, use uma URL totalmente qualificada incluindo a extensão do nome de arquivo (.rdl). Por exemplo, http://*\<SharePointservername>/\<site>*/Documents/Report1.RDL. Não há suporte para caminhos relativos.  
  
 Para obter mais informações, consulte [Como especificar caminhos para itens externos &#40;Construtor de Relatórios e SSRS&#41;](report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md) na [documentação do Construtor de Relatórios](https://go.microsoft.com/fwlink/?LinkId=154494) em msdn.microsoft.com.  
  
 **Use estes parâmetros para executar o relatório**  
 Adicione uma lista de parâmetros para passar para o relatório detalhado. Os nomes de parâmetro devem corresponder aos parâmetros definidos para o relatório de destino. Use os botões **Adicionar** e **Excluir** para adicionar ou remover parâmetros e use as setas para cima e para baixo para ordenar a lista de parâmetros.  
  
 **Adicionar**  
 Adicione um novo parâmetro para passar para o relatório detalhado.  
  
 **Delete (excluir)**  
 Exclua um parâmetro para o relatório detalhado.  
  
 **Seta para cima**  
 Mova o parâmetro para cima na lista.  
  
 **Seta para baixo**  
 Mova o parâmetro para baixo na lista.  
  
 **Nome**  
 Digite o texto que é o nome de um parâmetro definido no relatório detalhado.  
  
 **Valor**  
 Digite ou selecione um valor para passar para o parâmetro nomeado no relatório detalhado. Clique no botão **expressão** (*FX*) para editar a expressão.  
  
 **Omitir**  
 Selecione para impedir que o parâmetro execute. Por padrão, esta caixa de seleção é desmarcada e não ativa. Para marcar a caixa de seleção, clique no botão **expressão** (*FX*) e digite **true** ou crie uma expressão. A caixa de seleção é marcada quando você clica em **OK** na caixa de diálogo **Expressão** .  
  
 **Ir para o indicador**  
 Escolha esta opção para definir um link para um indicador no relatório atual. A opção adicional a seguir aparece quando você seleciona **Ir para o indicador**.  
  
 **Selecione o indicador**  
 Digite ou selecione uma ID de indicador para o relatório passar quando o usuário clicar no link. Clique no botão expressão (**FX**) para alterar a expressão. A ID de indicador pode ser uma ID estática ou uma expressão que seja avaliada por uma ID de indicador. A expressão pode incluir um campo que contenha uma ID de indicador.  
  
 Para criar um link para um indicador, você deve primeiro definir a propriedade Bookmark de um item de relatório. Para definir a propriedade Bookmark, selecione um item de relatório e, no painel Propriedades, digite um valor ou uma expressão para a ID do indicador. Por exemplo, GráficoDeVendas ou 5MaioresVendas.  
  
 **Ir para a URL**  
 Escolha esta opção para definir um vínculo para uma página da Web. Digite ou selecione a URL de uma página da Web ou uma expressão que seja avaliada por uma URL de uma página da Web. Clique no botão **expressão** (*FX*) para alterar a expressão. Essa expressão pode conter um campo com uma URL. A opção adicional a seguir aparece quando você seleciona **Ir para a URL**.  
  
 **Selecionar a URL**  
 Digite ou insira a URL do item. Para um item publicado em um servidor de relatórios configurado para o modo nativo, use um caminho completo ou relativo. Por exemplo, http://*\<ServerName>*/images/image1.jpg. Para um item publicado em um servidor de relatório configurado no modo integrado do SharePoint, use uma URL totalmente qualificada (por exemplo, http://*\<SharePointservername>/\<site>*/Documents/images/image1.jpg).  
  
## <a name="see-also"></a>Consulte Também  
 [Gráficos &#40;Construtor de Relatórios e SSRS&#41;](report-design/charts-report-builder-and-ssrs.md)   
 [Construtor de Relatórios ajuda para caixas de diálogo, painéis e assistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Parâmetros de relatório &#40;Construtor de Relatórios e Report Designer&#41;](report-design/report-parameters-report-builder-and-report-designer.md)   
 [Adicionar um sub-relatório e parâmetros &#40;Construtor de Relatórios e SSRS&#41;](report-design/add-a-subreport-and-parameters-report-builder-and-ssrs.md)   
 [Classificação interativa, mapas de documentos e links &#40;Construtor de Relatórios e SSRS&#41;](report-design/interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)  
  
  
