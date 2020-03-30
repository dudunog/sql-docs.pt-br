---
title: Adicionar uma imagem associada aos dados (Construtor de Relatórios) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: df4c38d4-bfcc-41c4-aa6d-952ca6fd7a2e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1ab11e39d435a2a4f965c4a6cb5cf367ae2b4d84
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77080763"
---
# <a name="add-a-data-bound-image-report-builder-and-ssrs"></a>Adicionar uma imagem associada a dados (Construtor de Relatórios e SSRS)
  Um relatório pode incluir uma referência a uma imagem armazenada em um banco de dados. Essa imagem é chamada de *imagem associada a dados*. As imagens exibidas ao lado dos nomes de produtos em uma lista de produtos são exemplos de imagens associadas a dados.  
  
 A adição de uma imagem associada a dados ao cabeçalho ou rodapé de uma página requer etapas adicionais. Para obter mais informações, consulte [Cabeçalhos e rodapés de página &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-data-bound-image"></a>Para adicionar uma imagem associada a dados  
  
1.  No modo design de relatório, crie uma tabela com uma conexão da fonte de dados e um conjunto de dados com um campo que contém dados de imagem binários. Para obter mais informações, consulte [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md).  
  
2.  Insira uma coluna em sua tabela. Para obter mais informações, consulte [Inserir ou excluir uma coluna &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md).  
  
3.  No menu **Inserir** , clique em **Imagem**e na linha de dados da nova coluna.  
  
4.  Na página Geral da caixa de diálogo **Propriedades da Imagem** , digite um nome na caixa de texto **Nome** ou aceite o padrão.  
  
5.  (Opcional) Na caixa de texto **Dica de Ferramenta** , digite o texto a ser exibido quando o usuário passar o mouse sobre a imagem no relatório renderizado para HTML.  
  
6.  Em **Selecione a origem da imagem**, clique em **Banco de Dados**.  
  
7.  Em **Usar este Campo**, selecione o campo que contém imagens no seu relatório.  
  
8.  Em **Usar este tipo MIME**, selecione o tipo MIME ou o formato de arquivo da imagem; por exemplo, bmp.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     Um espaço reservado para imagem é exibido na superfície de design do relatório.  
  
## <a name="see-also"></a>Consulte Também  
 [Imagens &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [Inserir uma imagem em um relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md)   
 [Adicionar uma imagem externa &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-an-external-image-report-builder-and-ssrs.md)   
 [Caixa de diálogo Propriedades da Imagem, Geral &#40;Construtor de Relatórios e SSRS&#41;](https://msdn.microsoft.com/library/c2218b93-f7fe-46ef-995f-d7dadf9752ec)  
  
  
