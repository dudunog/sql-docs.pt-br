---
title: Salvar um relatório em uma biblioteca do SharePoint (Construtor de Relatórios) | Microsoft Docs
description: Este artigo descreve os requisitos e o processo necessários para salvar relatórios em um servidor de relatório configurado para integração com o SharePoint.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: 4daa1eee-78b7-43d0-8b22-4a98e8fa66ba
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 41331a57b9eb8c3981a82e826794b9031b3eb73c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "80290850"
---
# <a name="save-a-report-to-a-sharepoint-library-report-builder"></a>Salvar um relatório em uma biblioteca do SharePoint (Construtor de Relatórios)
  Para salvar um relatório em um servidor de relatório configurado para integração com o SharePoint, vá até o servidor do SharePoint e estabeleça uma conexão com o servidor de relatório. Na definição de relatório, todas as referências a itens relacionados ao relatório devem usar valores específicos a um servidor de relatório do SharePoint. Os itens relacionados incluem sub-relatórios, relatórios detalhados e recursos, como imagens baseadas na Web. Para obter mais informações, consulte [Especificando caminhos para itens externos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/specifying-paths-to-external-items-report-builder-and-ssrs.md).  
  
 Você deve ter permissão de **Membro** ou **Proprietário** no site do SharePoint para definir as propriedades no projeto.  
  
### <a name="to-save-a-report-to-a-sharepoint-site"></a>Para salvar um relatório em um site do SharePoint  
  
1.  No botão Construtor de Relatórios, clique em **Salvar**. A caixa de diálogo **Salvar Como** _\<Item de Relatório>_ será exibida.  
  
    > [!NOTE]  
    >  Se você estiver salvando um relatório de novo, ele será salvo novamente automaticamente em seu local anterior. Use a opção **Salvar como** para alterar o local.  
  
2.  Se desejar, clique em **Sites e Servidores Recentes** para mostrar uma lista de servidores de relatório e sites do SharePoint usados recentemente.  
  
3.  Navegue até o site do SharePoint e clique em **Salvar**.  
  
    > [!NOTE]  
    >  Se você deixar um relatório alterado durante mais de 10 horas sem salvá-lo, ele será desconectado do servidor sem ser salvado. Se isso acontecer, na barra de status inferior direita, clique em **Desconectar**e clique em **Conectar**. O servidor mais recente estará na lista de servidores disponíveis. Selecione-o e o relatório reconectará.  
  
## <a name="see-also"></a>Consulte Também  
 [Localizando, exibindo e gerenciando relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)  
  
  
