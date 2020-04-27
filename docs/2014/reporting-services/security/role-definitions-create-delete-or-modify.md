---
title: Criar, excluir ou modificar uma função (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- roles [Reporting Services], creating
- deleting roles
- removing roles
- roles [Reporting Services], definitions
- modifying roles
- roles [Reporting Services], deleting
- roles [Reporting Services], modifying
ms.assetid: 3d1d56e6-a283-44a7-8417-36cb4d2c74d1
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 066c69298126cbc635d388d75659b98dcff95917
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66101804"
---
# <a name="create-delete-or-modify-a-role-management-studio"></a>Criar, excluir ou modificar uma função (Management Studio)
  O Reporting Services fornece funções predefinidas que definem um nível de acesso a um servidor de relatório. Cada usuário ou grupo que requer acesso ao servidor de relatório faz isso através de uma função que descreve as tarefas que podem ser executadas. As funções são definidas para o servidor de relatório como um todo. Não é possível variar uma definição de função para partes específicas do servidor de relatório nem especificar que uma função seja usada de modo diferente dependendo das circunstâncias.  
  
 Para criar, modificar ou excluir funções, use o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você só pode excluir funções que não são usadas.  
  
 Para atribuir usuários e grupos às funções criadas, use o Gerenciador de Relatórios. Para obter mais informações, consulte [conceder acesso de usuário a um servidor de relatório &#40;Report Manager&#41;](grant-user-access-to-a-report-server.md).  
  
> [!NOTE]  
>  Se o servidor de relatório estiver configurado para o modo integrado do SharePoint e você estiver conectado ao site do SharePoint no qual o servidor de relatório está integrado, poderá exibir e modificar os níveis de permissão que controlam o acesso ao conteúdo e às operações do servidor de relatório.  
  
### <a name="to-create-a-role-definition"></a>Para criar uma definição de função  
  
1.  No Pesquisador de Objetos, expanda um nó do servidor de relatório.  
  
2.  Expanda a pasta Segurança.  
  
3.  Se você estiver criando uma definição de função no nível do item, clique com o botão direito do mouse em **Funções**e aponte para **Nova Função**.  
  
     Se você estiver criando uma definição de função no nível do sistema, clique com o botão direito do mouse em **Funções do Sistema**e aponte para **Nova Função do Sistema**.  
  
4.  Digite um nome exclusivo para a função. Um nome deve conter pelo menos um caractere. Ele também pode incluir espaços e alguns símbolos, mas não os caracteres ; ? : \@ & = +, $/* \< > | "ou/.  
  
5.  Como opção, digite uma descrição. No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , essa descrição só é visível nesta página. Os usuários que exibem esse item por meio do Gerenciador de Relatórios podem ver essa descrição nessa ferramenta.  
  
6.  Selecione as tarefas que os membros dessa função podem executar.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-or-modify-a-role-definition"></a>Para excluir ou modificar uma definição de função  
  
1.  No Pesquisador de Objetos, expanda um nó do servidor de relatório.  
  
2.  Expanda a pasta Segurança.  
  
3.  Para excluir ou modificar uma definição de função no nível do item, expanda a pasta Funções. Execute uma das ações a seguir:  
  
    1.  Para excluir uma definição de função, clique com o botão direito do mouse no item e clique em **Excluir**. A caixa de diálogo **Excluir Objeto** é exibida. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    2.  Para modificar uma definição de função, clique com o botão direito do mouse no item e clique em **Propriedades**. A página Geral da caixa de diálogo **Propriedades de Função do Usuário** é exibida.  
  
         Selecione as tarefas que os membros desta função podem executar e clique em **OK**.  
  
4.  Para excluir ou modificar uma definição de função no nível do sistema, expanda a pasta **Funções do Sistema** . Execute uma das ações a seguir:  
  
    1.  Para excluir uma definição de função do sistema, clique com o botão direito do mouse no item e clique em **Excluir**. A caixa de diálogo **Excluir Objeto** é exibida. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
    2.  Para modificar uma definição de função do sistema, clique com o botão direito do mouse no item e clique em **Propriedades**. A página Geral da caixa de diálogo **Propriedades de Função do Sistema** é exibida.  
  
         Selecione as tarefas que os membros desta função podem executar e clique em **OK** para aplicar as alterações.  
  
## <a name="see-also"></a>Consulte Também  
 [Conectar-se a um servidor de relatório no Management Studio](../tools/connect-to-a-report-server-in-management-studio.md)   
 (create-and-manage-role-assignments.md)   
 [Reporting Services no SQL Server Management Studio &#40;SSRS&#41;](../tools/reporting-services-in-sql-server-management-studio-ssrs.md)  
  
  
