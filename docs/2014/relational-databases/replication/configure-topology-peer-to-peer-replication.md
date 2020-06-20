---
title: Configurar Topologia (replicação ponto a ponto) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.p2pwizard.peers.f1
ms.assetid: 5377c59f-2e25-4852-a306-c87ae3dca9fd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 2dfc09f5ae7f488afd46f29c301d11b7687e0a4b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010977"
---
# <a name="configure-topology-peer-to-peer-replication"></a>Configurar Topologia (replicação ponto a ponto)
  Use a página **Configurar Topologia** para executar tarefas de configuração comuns, como adicionar novos nós, excluir nós e adicionar novas conexões entre nós existentes. O nó selecionado na página **Publicação** desse assistente é exibido na superfície de design. Para especificar opções de configuração, clique com o botão direito do mouse em um nó, em uma conexão ou na superfície de design.

> [!NOTE]
>  O Assistente para Configurar Topologia Ponto a Ponto solicita as informações da topologia quando o assistente é fechado. Se o assistente for fechado e reaberto antes de todos os nós responderem à solicitação de informações, o assistente poderá mostrar uma rede parcial.

## <a name="options"></a>Opções
 A página **Configurar topologia** contém elementos de interface e opções disponíveis ao clicar com o botão direito do mouse em um elemento. A tabela a seguir descreve cada elemento de interface.

|Elemento de interface|DESCRIÇÃO|
|-----------------------|-----------------|
|Superfície de design|Exibe outros elementos de interface. Para adicionar elementos, clique com o botão direito do mouse na superfície de design.|
|![O primeiro nó em uma topologia](media/p2pwizard-firstnode.gif "O primeiro nó em uma topologia")|O nó original na topologia. Novos nós são iniciados usando uma cópia do banco de dados de publicação do nó original.|
|![Um nó para o qual temos informações completas](media/p2pwizard-complete.gif "Um nó para o qual temos informações completas") ou uma versão posterior, para a qual a replicação tem informações completas. Para especificar opções de configuração, clique com o botão direito do mouse no nó.|
|![Um nó para o qual temos informações incompletas](media/p2pwizard-incomplete.gif "Um nó para o qual temos informações incompletas")|Um nó para o qual a replicação tem informações incompletas. Para especificar opções de configuração, clique com o botão direito do mouse no nó. A replicação tem informações incompletas por um dos seguintes motivos:<br /><br /> O nó está executando uma instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] que não armazena todos os metadados exigidos pelo assistente.<br /><br /> O nó está executando uma versão posterior do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas a replicação não consegue recuperar informações de assinatura do nó. Para solucionar essa situação:<br />-Verifique se o banco de dados no nó está online e se você pode se conectar a ele usando as mesmas credenciais que os agentes de distribuição que se conectam ao nó.<br />-Verifique se o Agente de Leitor de Log e todos os agentes de distribuição que se conectam ao nó estão em execução.<br />-Verifique se o tempo limite de atualização está definido como alto o suficiente para coletar todas as informações de topologia. Para definir o tempo limite, clique com o botão direito do mouse na superfície de design e clique em **Selecionar Tempo Limite de Atualização**.|
|Linhas cinza com setas|Conexão entre dois nós. Para adicionar uma conexão, clique com o botão direito do mouse em um dos nós que você quer conectar. Para remover uma conexão, clique com o botão direito do mouse na conexão.<br /><br /> Se a linha tiver uma única seta, a replicação terá informações incompletas para um dos nós.|

### <a name="options-for-the-design-surface"></a>Opções para a superfície de design
 **Redesenhar grafo** Redesenhe os objetos na superfície de design sem Atualizar a topologia. O novo desenho deverá fornecer uma exibição melhor da topologia.

 **Atualizar topologia** Consulte cada nó na topologia e exiba informações atualizadas sobre cada nó. Se houver muitos nós, esse processo pode levar vários minutos.

 Se o assistente solicitar informações de topologia, e, você fechar e reabrir o assistente, antes que todos os nós respondam à solicitação, essa página poderá não exibir todos os nós na topologia.

 **Adicionar um novo nó par** Adicione uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à topologia ponto a ponto. A adição de uma instância, como um nó, cria uma publicação nessa instância depois que o assistente é concluído. Depois de adicionar o nó, clique com o botão direito do mouse, para adicionar uma conexão entre o nó novo e um nó existente.

 Para participar de uma topologia ponto a ponto, a instância deve satisfazer os seguintes requisitos:

-   Deverá estar configurada como um Distribuidor ou associada a um Distribuidor remoto.

-   Deve conter uma cópia do banco de dados envolvido na replicação. Essa cópia é normalmente um backup restaurado do banco de dados de publicação original.

 **Selecionar nó (s) para exibição** Selecione os nós a serem exibidos na superfície de design. Essa opção será útil se a topologia tiver um grande número de nós. Observe que você só poderá adicionar conexões entre nós visíveis na superfície de design.

 **Definir tempo limite de atualização** Especifique por quanto tempo o processo de atualização pode ser executado antes que a operação expire.

### <a name="options-for-each-node"></a>Opções para cada nó
 **Adicionar uma nova conexão de mesmo nível** Adicione uma conexão entre dois nós. Por exemplo, se você adicionar uma conexão entre o Nó A e o Nó B, a replicação adicionará duas assinaturas: a primeira habilitará o Nó A a receber alterações de publicação no Nó B e a segunda habilitará o Nó B a receber alterações de publicação no Nó A.

 **Excluir nó par** Remove um nó da topologia. Por exemplo, se você remover Nó C, a publicação desse nó será removida. As assinaturas entre Nó A e Nó C, Nó B e Nó C também serão removidas. O banco de dados no Nó C não é excluído, e, a publicação e a distribuição não são desabilitadas.

> [!NOTE]
>  Quando você configurar replicação ponto a ponto, especifique uma ID para cada nó. Esta ID, que deve ser exclusiva em todos os nós na topologia, é armazenada na coluna originator_id na tabela do sistema [MSpeer_originatorid_history](/sql/relational-databases/system-tables/mspeer-originatorid-history-transact-sql). Se um nó for removido da topologia, a ID ainda será mantida na tabela de histórico. A ID é mantida para impedir a ocorrência de falsos conflitos caso sejam feitas alterações do nó removido que ainda sejam replicadas na topologia. Se você quiser reutilizar a ID para um novo nó, primeiro exclua manualmente a ID da tabela MSpeer_originatorid_history em todos os nós. Antes de excluir uma ID de um nó, execute [sp_requestpeerresponse](/sql/relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql) para verificar se todas as alterações originadas desse nó foram replicadas.

 **Conectar-se a todos os nós exibidos** Adiciona conexões entre o nó selecionado e todos os outros nós. Por exemplo, se você selecionou essa opção para o Nó C em uma topologia de nós de árvore, a replicação adicionará quatro assinaturas: duas para habilitar o Nó A e Nó B a receber alterações da publicação no Nó C, e, duas para habilitar o Nó C a receber alterações de publicações no Nó A e Nó B.

 **Selecionar nó (s) para exibição** Selecione os nós a serem exibidos na superfície de design. Essa opção será útil se a topologia tiver um grande número de nós. Observe que você só poderá adicionar conexões entre nós visíveis na superfície de design.

### <a name="options-for-the-connection-arrows"></a>Opções para as setas de conexão
 **Remover conexão de mesmo nível** Remova uma conexão entre dois nós. Por exemplo, se você remover uma conexão entre o Nó A e o Nó B, a replicação descartará duas assinaturas: a que habilita o Nó A a receber alterações de publicação no Nó B e a que habilita o Nó B a receber alterações de publicação no Nó A.

## <a name="see-also"></a>Consulte Também
 [Configurar a publicação e a distribuição](configure-publishing-and-distribution.md) [administrar uma topologia ponto a ponto &#40;Programação Transact-SQL de replicação&#41;](administration/administer-a-peer-to-peer-topology-replication-transact-sql-programming.md) [replicação transacional ponto a ponto](transactional/peer-to-peer-transactional-replication.md)


