---
title: Adicionar um sub-relatório e parâmetros (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10093"
- sql12.rtp.rptdesigner.subreportproperties.general.f1
ms.assetid: 94f960f8-a629-4f1e-8277-c3b8f0680d98
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 906f4527bdca38f4571a2e1686f885a2857e47c3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106791"
---
# <a name="add-a-subreport-and-parameters-report-builder-and-ssrs"></a>Adicionar um sub-relatório e parâmetros (Construtor de Relatórios e SSRS)
  Adicione sub-relatórios a um relatório quando quiser criar um relatório principal que seja um contêiner para vários relatórios relacionados. Um sub-relatório é uma referência a outro relatório. Para relacionar os relatórios por valores de dados (por exemplo, para que diversos relatórios exibam dados para o mesmo cliente), é preciso criar um relatório com parâmetros (por exemplo, um relatório que exiba os detalhes de um cliente específico) como o sub-relatório. Ao adicionar um sub-relatório ao relatório principal, você também pode especificar os parâmetros que serão passados para o sub-relatório.  
  
 Também é possível adicionar sub-relatórios a linhas ou colunas dinâmicas em uma tabela ou matriz. Quando o relatório principal é processado, o sub-relatório é processado para cada linha. Nesse caso, analise se você pode obter o efeito desejado usando regiões de dados ou regiões de dados aninhados.  
  
 Para adicionar um sub-relatório a um relatório, crie primeiro o relatório que atuará como sub-relatório. Para obter mais informações sobre como criar o sub-relatório, consulte [Sub-relatórios &#40;Construtor de Relatórios e SSRS&#41;](subreports-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-subreport"></a>Para adicionar um sub-relatório  
  
1.  Na guia **Inserir** , clique em **Sub-relatório**.  
  
2.  Na superfície de design, clique em um local no relatório e arraste a caixa até obter o tamanho desejado para o sub-relatório. Se preferir, clique na superfície de design para criar um sub-relatório de tamanho padrão.  
  
3.  Clique com o botão direito do mouse no sub-relatório e clique em **Propriedades do sub-relatório**.  
  
4.  Na caixa de diálogo **Propriedades do Sub-relatório** , digite um nome na caixa de texto **Nome** ou aceite o nome padrão. O nome deve ser exclusivo no relatório. Por padrão, um nome geral, como Subreport1 ou Subreport2, é atribuído.  
  
5.  Na caixa **Usar este relatório como sub-relatório** , clique em **Procurar**ou digite o nome do relatório. É preferível clicar em **Procurar** porque o caminho para o sub-relatório será especificado automaticamente. Você pode especificar o relatório de várias maneiras. Para obter mais informações, consulte [Especificando caminhos para itens externos &#40;Construtor de Relatórios e SSRS&#41;](specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
6.  (Opcional) Clique em **Sim** para **Omitir borda na quebra de página** para impedir que uma borda seja renderizada no meio do sub-relatório caso o sub-relatório se expanda por mais de uma página.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-specify-parameters-to-pass-to-a-subreport"></a>Para especificar os parâmetros que serão passados para um sub-relatório  
  
1.  No modo de exibição de Design, clique com o botão direito do mouse no sub-relatório e clique em **Propriedades do sub-relatório**.  
  
2.  Na caixa de diálogo **Propriedades do Sub-relatório** , clique em **Parâmetros**.  
  
3.  Clique em **Adicionar**. Uma linha nova é adicionada à grade de parâmetros.  
  
4.  Na caixa de texto **de Nome** , digite o nome de um parâmetro no sub-relatório ou escolha-o na caixa de listagem. Esse nome deve corresponder a um parâmetro de relatório, não a um parâmetro de consulta, no sub-relatório.  
  
5.  Na caixa de listagem **Valor** , digite ou selecione um valor a ser passado para o sub-relatório. Esse valor pode ser um texto estático ou uma expressão que referencie um campo ou outro objeto no relatório principal.  
  
    > [!NOTE]  
    >  No Construtor de Relatórios, se um parâmetro estiver ausente na lista **Parâmetros** , e se o sub-relatório tiver um valor padrão definido, o sub-relatório será processado corretamente.  
    >   
    >  No Designer de Relatórios, todos os parâmetros exigidos pelo sub-relatório devem estar incluídos na lista **Parâmetros** . Se estiver faltando um parâmetro obrigatório, o sub-relatório não será exibido corretamente no relatório principal.  
  
6.  Repita as etapas de 3 a 5 para especificar um nome e um valor para cada parâmetro do sub-relatório.  
  
7.  Para excluir um parâmetro de sub-relatório, clique no parâmetro na grade de parâmetros e clique em **Excluir**.  
  
8.  Para alterar a ordem de um parâmetro de sub-relatório, clique no parâmetro e clique no botão de seta para cima ou para baixo.  
  
     A alteração da ordem de um parâmetro de sub-relatório não afeta o processamento do sub-relatório.  
  
## <a name="see-also"></a>Consulte Também  
 [Sub-relatórios &#40;Construtor de Relatórios e SSRS&#41;](subreports-report-builder-and-ssrs.md)   
 [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](rendering-behaviors-report-builder-and-ssrs.md)  
  
  
