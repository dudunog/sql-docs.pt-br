---
title: 'Lição 5: Criar o relatório filho usando o Assistente de Relatório | Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 19a3f927-ea97-4f40-a5f8-cd5f2598e4da
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 661b4f3cc63eb0c19fddb53f872e940d1f9976e2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108435"
---
# <a name="lesson-5-design-the-child-report-using-the-report-wizard"></a>Lição 5: Criar o relatório filho usando o Assistente de Relatório
  Após criar uma conexão de dados e uma tabela de dados para o relatório filho, a próxima etapa será criar o relatório filho usando o Assistente de Relatório no Designer de Relatórios. Para obter mais informações sobre o Designer de Relatórios, consulte [Criar relatórios com o Designer de Relatórios &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
### <a name="to-design-the-child-report-using-the-report-wizard"></a>Para criar o relatório filho usando o Assistente de Relatório  
  
1.  Verifique se esse site de nível superior está selecionado no **Gerenciador de Soluções**.  
  
2.  Clique com o botão direito do mouse no site e selecione **Adicionar Novo Item**.  
  
3.  Na caixa de diálogo **Adicionar novo item** , clique em **Assistente de relatório**, insira um nome para o arquivo de relatório e clique em **Adicionar**.  
  
     Isso iniciará o Assistente de Relatório.  
  
4.  Na página **Propriedades de DataSet** , na caixa **fonte de dados** , clique em **DataSet2**.  
  
     A caixa **Conjuntos de dados disponíveis** é atualizada automaticamente com a DataTable criada.  
  
5.  Clique em **Avançar**.  
  
6.  Na página **Organizar campos** , faça o seguinte:  
  
    1.  Arraste **ProductID**, **PurchaseOrderID**, **PurchaseOrderDetailID**, **OrderQty**, **ReceivedQty**, **RejectedQty**e **StockedQty** de **Campos disponíveis** até a caixa **Valores** .  
  
    2.  Clique na seta ao lado de **Soma (ProductID)**, **Soma (PurchaseOrderID)**, **Soma (PurchaseOrderDetailID)**, **Soma (OrderQty)**, **Soma (ReceivedQty)**, **Soma (RejectedQty)** e **Soma (StockedQty)** e desmarque a seleção **soma** .  
  
7.  Clique em **Avançar** duas vezes e, em seguida, clique em **concluir** para fechar o **Assistente de relatório**.  
  
     Agora você criou o arquivo .rdlc. O arquivo é aberto no Designer de Relatórios. Agora, o tablix que você criou será exibido na superfície de design.  
  
8.  Com o arquivo .rdlc aberto, adicione um parâmetro da seguinte maneira:  
  
    1.  Clique em **parâmetros** no painel **dados do relatório** e, em seguida, clique em **adicionar parâmetros**.  
  
    2.  Insira **productid** na caixa **Nome** .  
  
    3.  Confirme se a opção **Inteiro** está selecionada na caixa de listagem **Tipo de Dados** .  
  
    4.  Clique em **OK**.  
  
9. Salve o arquivo .rdlc.  
  
## <a name="next-task"></a>Próxima tarefa  
 Você criou o relatório filho com êxito usando o Assistente de Relatório. Em seguida, você adicionará um controle ReportViewer ao aplicativo de site.  
  
  
