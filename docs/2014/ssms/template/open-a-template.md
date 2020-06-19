---
title: Abrir um modelo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- templates [Transact-SQL], opening
- opening templates
ms.assetid: 605b0f4c-5ba1-4249-ad1c-6341df77cd7a
author: stevestein
ms.author: sstein
ms.openlocfilehash: ad12b20233cb753b28c4618ce53cd28ed850984c
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061952"
---
# <a name="open-a-template"></a>Abrir um modelo
  Você pode abrir um modelo a partir do Explorador de Modelos.  
  
## <a name="to-open-a-template-from-template-explorer"></a>Para abrir um modelo a partir do Explorador de Modelos  
 Você pode abrir modelos a partir do Explorador de Modelos.  
  
1.  Para abrir o Gerenciador de Modelos, no menu **Exibir** , clique em **Gerenciador de Modelos**.  
  
2.  Na lista de categorias de modelo, expanda a categoria que contém o modelo que você deseja abrir.  
  
3.  Há três modos de abrir o modelo:  
  
    1.  Clique duas vezes no modelo para abri-lo em uma janela de editor de código.  
  
    2.  Clique com o botão direito do mouse no modelo e selecione **Abrir** para abri-lo em uma janela do editor de código.  
  
    3.  Arraste o modelo para uma janela do editor de código para adicionar o código do modelo ao conteúdo da janela do editor.  
  
 Após abrir o modelo, use a caixa de diálogo **Substituir Parâmetros do Modelo** para substituir os parâmetros do modelo pelos seus próprios valores.  
  
 Se a abertura de um modelo iniciar uma nova janela do editor, a janela será aberta com as credenciais da conexão ativa atual. Por exemplo, se você estiver concentrado em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] no Pesquisador de Objetos quando você abrir o modelo CREATE DATABASE, uma nova janela do editor será aberta usando uma conexão com essa instância. Se não houver nenhuma conexão ativa, o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] apresentará uma caixa de diálogo de logon.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciador de modelos](template-explorer.md)   
 [Substituir parâmetros do modelo](replace-template-parameters.md)  
  
  
