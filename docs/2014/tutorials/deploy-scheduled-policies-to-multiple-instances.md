---
title: Implantar políticas agendadas em várias instâncias | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: f551b8e8-3668-4ed4-852f-bae826254f4f
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 8d37dafd5501a289e45a119323eed61242707184
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68185816"
---
# <a name="deploy-scheduled-policies-to-multiple-instances"></a>Implantar diretivas agendadas em várias instâncias
  Usando Servidores Registrados, você poderá implantar políticas agendadas em servidores gerenciados a partir de um local central. Você poderá implantar diretivas agendadas a partir de um grupo de servidores local ou de um Servidor Central de Gerenciamento.  
  
 Nesta tarefa, você fará o seguinte:  
  
1.  Exportar as diretivas agendadas na tarefa anterior em uma pasta.  
  
2.  Implantar as diretivas agendadas nas instâncias de destino que são gerenciadas por meio de Servidores Registrados.  
  
 Você executará essas tarefas no computador em que concluiu as tarefas anteriores desta lição.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Esta tarefa tem os seguintes pré-requisitos:  
  
-   Você deve ter concluído as tarefas anteriores desta lição.  
  
-   As instâncias em que você implantará as diretivas agendadas deve estar executando o [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] ou uma versão posterior. A automação requer que as diretivas sejam armazenadas localmente, o que não tem suporte em versões do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] anteriores ao [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)].  
  
-   Os servidores em que você deseja implantar as políticas agendadas devem ser registrados em servidores registrados no nó **grupos** de servidores locais ou **servidores de gerenciamento central** . Para obter mais informações, consulte estes tópicos:  
  
    -   [Criar ou editar um grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-or-edit-a-server-group-sql-server-management-studio.md)  
  
    -   [Registre um servidor conectado &#40;SQL Server Management Studio&#41;](../ssms/register-servers/register-a-connected-server-sql-server-management-studio.md).  
  
    -   [Criar um servidor de gerenciamento central e um grupo de servidores &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)  
  
### <a name="to-export-the-scheduled-policies-as-xml-files"></a>Para exportar as diretivas agendadas como arquivos .xml  
  
1.  No servidor em que você configurou políticas agendadas na tarefa anterior, expanda **Gerenciamento**, **Gerenciamento de políticas**e, em seguida, clique em **políticas**.  
  
2.  No menu **Exibir** , clique em **Detalhes do Pesquisador de Objetos**.  
  
3.  No painel **detalhes** do pesquisador de objetos, selecione todas as políticas de práticas recomendadas agendadas que você deseja implantar em outros servidores por meio de servidores registrados.  
  
    > [!NOTE]  
    >  Você pode clicar no título **categoria** para classificar as políticas por categoria.  
  
4.  Clique com o botão direito do mouse na seleção e clique em **Exportar política**.  
  
5.  Se você tiver selecionado várias políticas para exportar, na caixa de diálogo **Procurar pasta** , selecione uma pasta de destino ou crie uma nova pasta. Nesta lição, crie uma nova pasta com o caminho **c:\ Scheduled_BP_Policies**e clique em **OK**.  
  
     Se você selecionou apenas uma política para exportar, na caixa de diálogo **Exportar política** , crie uma nova pasta com o caminho **c:\ Scheduled_BP_Policies**, clique em **abrir**e, em seguida, clique em **salvar**.  
  
     Os arquivos de diretivas .xml são criados no local da pasta.  
  
### <a name="to-deploy-the-scheduled-policies-to-servers-that-are-managed-through-registered-servers"></a>Para implantar as diretivas agendadas em servidores que são gerenciados por meio de Servidores Registrados  
  
1.  No menu **Exibir** , clique em **Servidores Registrados**.  
  
2.  Expanda **mecanismo de banco de dados**, expanda **grupos de servidores locais** ou **servidores de gerenciamento central**, clique com o botão direito do mouse no nó no qual você deseja implantar as políticas e clique em **importar políticas**.  
  
    > [!NOTE]  
    >  Se você clicar com o botão direito do mouse em **grupos de servidores locais** ou no próprio servidor de gerenciamento central, as políticas serão implantadas em todos os servidores gerenciados. Se você clicar com o botão direito do mouse em um grupo específico de servidores, as diretivas serão implantadas somente nos servidores desse grupo. Se você clicar com o botão direito do mouse em um servidor registrado específico, as políticas serão implantadas nesse servidor.  
  
3.  Ao lado de **arquivos a serem importados**, clique no botão de reticências (**...**).  
  
4.  Na caixa de diálogo **selecionar política** , navegue até o local da pasta onde você salvou as políticas agendadas. Para este exemplo, navegue até o local **c:\ Scheduled_BP_Policies**.  
  
5.  Selecione as políticas que você deseja importar para as instâncias de destino e clique em **abrir**.  
  
6.  Na caixa de diálogo **importar** , na lista **estado da política** , selecione o estado da política desejada. Você poderá optar por preservar o estado da diretiva, habilitar ou desabilitar as diretivas na importação. Lembre-se de que as diretivas devem ser habilitadas para execução em um agendamento.  
  
7.  Clique em **OK** para importar as políticas para todas as instâncias de destino.  
  
    > [!NOTE]  
    >  Se houver erros, a caixa de diálogo **importar** não desaparecerá. Clique na página **log** para examinar as mensagens. Clique em **Cancelar** para fechar a caixa de diálogo.  
  
8.  Para exibir as políticas de uma instância de destino, conecte-se à instância do, abra o pesquisador de objetos, expanda **Gerenciamento**e expanda **políticas**. Você deve ver as políticas importadas no nó **políticas** . Se você clicar duas vezes em cada diretiva, poderá ver a agenda ou alterar as configurações.  
  
    > [!NOTE]  
    >  Para exibir os resultados da avaliação após a execução de uma diretiva agendada, abra o log Histórico da Diretiva na instância de destino. Para abrir o log, clique com o botão direito do mouse em **Gerenciamento de políticas**e clique em **Exibir histórico**.  
  
## <a name="summary"></a>Resumo  
 Este tutorial mostrou como executar avaliações sob demanda e planejadas das diretivas de práticas recomendadas em uma ou mais instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="next"></a>Próximo  
 Este tutorial está concluído. Para retornar ao início, consulte [tutorial: avaliando práticas recomendadas usando o gerenciamento baseado em políticas](../../2014/tutorials/tutorial-evaluating-best-practices-by-using-policy-based-management.md).  
  
 Para ver uma lista de [!INCLUDE[ssDE](../includes/ssde-md.md)] tutoriais, clique [mecanismo de banco de dados tutoriais](../relational-databases/database-engine-tutorials.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Administrar servidores com Gerenciamento Baseado em Políticas](../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
