---
title: Especifique uma versão como a versão mais recente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- version control services [SQL Server], latest version
- latest file version specified
- file versions [SQL Server]
ms.assetid: 407dffb1-3ecf-461e-835d-124781f26ee7
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: d598ec6f828fc7d8d59b3f998b775a752b94c4a6
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84928864"
---
# <a name="specify-a-version-as-the-latest-version"></a>Especificar uma versão como a versão mais recente
  Quando você faz o check-in de um arquivo no controle do código-fonte, essa versão se torna a mais recente; usuários que fazem check-out ou recuperam a versão mais recente recebem cópias locais do item em que foi feito check-in recentemente.  
  
 Entretanto, em algumas situações, você pode querer designar uma versão anterior de um item como a versão mais recente. Por exemplo, você faz check-out de um arquivo, modifica o arquivo e, por fim, faz check-in do arquivo. Você decide descartar suas modificações posteriormente. Como você fez o check-in do item, desfazer o check-out original não é uma opção. Nessa situação, você pode designar a versão original de check-out como a versão mais recente do item.  
  
 Você pode designar a versão mais recente:  
  
-   **Fixação de uma versão**. Quando você fixa uma versão de arquivo, as versões mais recentes que a versão fixada não são excluídas. Além disso, você pode desafixar o arquivo fixado anteriormente. Quando você fizer isso, a versão de check-in mais recente do arquivo se tornará a versão mais recente. Entretanto, você não pode fazer check-out de um arquivo fixado.  
  
-   **Revertendo para uma versão especificada**. Quando você reverte uma versão, todas as versões mais recentes do que a revertida serão excluídas do controle de código-fonte. Depois você pode fazer o check-out da versão mais recente restante.  
  
### <a name="to-pin-a-version"></a>Para fixar uma versão  
  
1.  No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], abra a solução.  
  
2.  No Gerenciador de Soluções, selecione o arquivo que você deseja especificar como versão mais recente.  
  
3.  No menu **arquivo** , aponte para **controle do código-fonte** e clique em **ViewHistory**.  
  
4.  Na caixa **de diálogo histórico de** \<file> , selecione a versão que você deseja especificar como a mais recente e clique em **fixar**.  
  
     Um símbolo de alfinete aparece próximo à versão selecionada, indicando que essa é a versão atual do arquivo. Se você tiver uma versão diferente carregada no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], será solicitado a recarregar o arquivo.  
  
### <a name="to-roll-back-to-a-version"></a>Para reverter uma versão  
  
1.  No [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], abra a solução.  
  
2.  No Gerenciador de Soluções, selecione o item que você deseja especificar como versão mais recente.  
  
3.  No menu **arquivo** , aponte para **controle do código-fonte** e clique em **histórico**.  
  
4.  Na caixa de diálogo **Opções de histórico** , clique em **OK** para exibir a caixa **de diálogo histórico de arquivo** .  
  
5.  Na caixa **histórico do arquivo** , selecione a versão que você deseja especificar como a versão mais recente e clique em **reverter**.  
  
     Uma mensagem é exibida notificando você de que todas as versões subsequentes àquelas selecionadas serão excluídas.  
  
6.  Clique em **Sim** para reverter para a versão selecionada.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciar Check-ins](../../2014/database-engine/manage-checkins.md)   
 [Fazer check-in de arquivos](../../2014/database-engine/check-in-files.md)  
  
  
