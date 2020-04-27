---
title: Adicionar, alterar ou excluir um parâmetro de relatório (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d44a8e0a-10cf-4502-9391-09743ffc9bad
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ebf333b49c20c7eadef4fdbcd54834c450d274c6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106692"
---
# <a name="add-change-or-delete-a-report-parameter-report-builder-and-ssrs"></a>Adicionar, alterar ou excluir um parâmetro de relatório (Construtor de Relatórios e SSRS)
  Um parâmetro de relatório fornece uma maneira de escolher dados de relatório, conectar relatórios relacionados e variar a apresentação do relatório. Você pode fornecer um valor padrão e uma lista de valores disponíveis e o usuário pode alterar a seleção.  
  
 Depois de publicar um relatório, você poderá alterar os valores padrão, os valores disponíveis e outras propriedades para um parâmetro de relatório no servidor de relatórios. Você pode fornecer vários conjuntos de valores de parâmetros padrão criando relatórios vinculados. Para obter mais informações, consulte "Setting Parameter Properties for a Published Report" na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online do SQL Server](https://go.microsoft.com/fwlink/?linkid=120955).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-or-edit-a-report-parameter"></a>Para adicionar ou editar um parâmetro de relatório  
  
1.  No painel **Dados do Relatório** , clique com o botão direito do mouse no nó **Parâmetros** e clique em **Adicionar Parâmetro**. A caixa de diálogo **Propriedades do Parâmetro do Relatório** é aberta.  
  
2.  Em **Nome**, digite o nome do parâmetro ou aceite o nome padrão.  
  
3.  No **Prompt**, digite o texto que é exibido ao lado da caixa de texto do parâmetro quando o usuário executa o relatório.  
  
4.  Na lista **Tipo de dados**, selecione o tipo de dados do valor do parâmetro.  
  
5.  Se o parâmetro pode conter um valor em branco, selecione **Permitir valor em branco**.  
  
6.  Se o parâmetro pode conter um valor nulo, selecione **Permitir valor nulo**.  
  
7.  Para permitir que um usuário selecione mais de um valor do parâmetro, selecione **Permitir diversos valores**.  
  
8.  Defina a opção de visibilidade.  
  
    -   Para mostrar o parâmetro na barra de ferramentas na parte superior do relatório, selecione **Visível**.  
  
    -   Para ocultar o parâmetro para que ele não seja exibido na barra de ferramentas, selecione **Oculto**.  
  
    -   Para ocultar o parâmetro e impedi-lo de ser modificado no servidor de relatórios depois que o relatório é publicado, selecione **Interno**. O parâmetro de relatório só pode ser exibido na definição do relatório. Para essa opção, você deve definir um valor padrão ou permitir que o parâmetro aceite um valor nulo.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-report-parameter"></a>Para excluir um parâmetro de relatório  
  
1.  No painel **Dados do Relatório** , expanda o nó **Parâmetros** .  
  
2.  Clique com o botão direito do mouse no parâmetro do relatório e clique em **Excluir**.  
  
## <a name="see-also"></a>Consulte Também  
 [Adicionar, alterar ou excluir valores disponíveis para um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](add-change-or-delete-available-values-for-a-report-parameter.md)   
 [Adicione, altere ou exclua valores padrão para um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](add-change-or-delete-default-values-for-a-report-parameter.md)   
 [Alterar a ordem de um parâmetro de relatório &#40;Construtor de Relatórios e SSRS&#41;](change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [Parâmetros de relatório &#40;Construtor de Relatórios e Report Designer&#41;](report-parameters-report-builder-and-report-designer.md)   
 [Construtor de Relatórios ajuda para caixas de diálogo, painéis e assistentes](../report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Adicionar parâmetros em cascata a um relatório &#40;Construtor de Relatórios e SSRS&#41;](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [Tutorial: adicionar um parâmetro ao seu relatório &#40;Construtor de Relatórios&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [TUTORIAIS &#40;Construtor de Relatórios&#41;](../report-builder-tutorials.md)   
 [Adicionar filtros de conjunto de dados, filtros de região e filtros de grupo &#40;Construtor de Relatórios e SSRS&#41;](add-dataset-filters-data-region-filters-and-group-filters.md)   
 [Referências de coleção de parâmetros &#40;Construtor de Relatórios e SSRS&#41;](built-in-collections-parameters-collection-references-report-builder.md)   
 [Adicionar um parâmetro com vários valores a um relatório](add-a-multi-value-parameter-to-a-report.md)  
  
  
