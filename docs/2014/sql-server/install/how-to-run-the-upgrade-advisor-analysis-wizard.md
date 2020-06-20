---
title: Como executar o assistente de análise do supervisor de atualização | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Analysis Wizard
ms.assetid: d7d2a1e2-1179-4c05-9b0f-555b04dd1199
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 548abb55ffcf6b8b0eca4ab7052a7995ef271a54
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059279"
---
# <a name="how-to-run-the-upgrade-advisor-analysis-wizard"></a>Como fazer: Para executar o Assistente para Análise do Supervisor de Atualização
  Você inicia o Assistente para Análise do Supervisor de Atualização na página inicial do Supervisor de Atualização. Este tópico descreve como executar o Assistente para Análise do Supervisor de Atualização.  
  
> [!IMPORTANT]
>  Quando você executa o Assistente para Análise do Supervisor de Atualização, o Supervisor de Atualização salva os relatórios na pasta de relatórios padrão. Entretanto, o visualizador de relatórios exibe apenas os cinco relatórios mais recentes salvos. O local padrão dos relatórios é meus documentos \\ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] upgrade Advisor\110\Reports.  
  
### <a name="to-run-the-upgrade-advisor-analysis-wizard"></a>Para executar o assistente de análise do supervisor de atualização  
  
1.  Na página inicial do supervisor de atualização, clique em **Iniciar assistente de análise do supervisor de atualização**.  
  
2.  Na página ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componentes** , digite o nome do servidor a ser verificado na caixa **nome do servidor** e clique em **detectar**. Use as políticas a seguir para o nome de servidor:  
  
    -   Para verificar instâncias não clusterizadas, insira o nome do computador.  
  
    -   Para verificar instâncias clusterizadas, digite o nome do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] virtual.  
  
    -   Para verificar os componentes não clusterizados que estão instalados em um nó de um cluster, insira o nome do nó.  
  
    > [!WARNING]  
    >  O Supervisor de Atualização não oferece suporte à conexão a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não é definida para usar a porta padrão (1433) para conexões de cliente. Se você desejar se conectar a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não usa a porta padrão (1433), crie um alias usando o endereço IP e a porta. Para obter mais informações sobre como configurar protocolos de cliente e criar um alias para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instâncias, consulte [Configurar protocolos de cliente](../../database-engine/configure-windows/configure-client-protocols.md).  
    >   
    >  Se você não tiver [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado no computador no qual está executando o supervisor de atualização, clique em **Iniciar**e em executar `cliconfg` . Isso abre a caixa de diálogo ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utilitário de rede do cliente** . Use a guia **alias** para criar o alias.  
  
3.  Examine a lista de componentes detectados, modifique as seleções conforme necessário e clique em **Avançar**.  
  
4.  Na página **parâmetros de conexão** , selecione a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você deseja verificar, selecione o método de autenticação e, se necessário, insira informações de nome de usuário e senha e clique em **Avançar**.  
  
     O nome de instância padrão é MSSQLSERVER.  
  
5.  No caso dos componentes selecionados, digite as informações solicitadas. Para obter mais informações sobre caixas de diálogo individuais, consulte [referência da interface do usuário do supervisor de atualização](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md).  
  
6.  Na página **confirmar a configuração do supervisor de atualização** , examine as informações inseridas. Você pode selecionar **enviar relatórios para [!INCLUDE[msCoName](../../includes/msconame-md.md)] ** se desejar enviar seu relatório de atualização. Você também pode visualizar a política de privacidade.  
  
7.  Clique em **executar** para analisar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
8.  Quando a análise for concluída, clique em **Iniciar relatório** para exibir os problemas de atualização detectados.  
  
## <a name="see-also"></a>Consulte Também  
 [Como iniciar o supervisor de atualização](../../../2014/sql-server/install/how-to-launch-upgrade-advisor.md)   
 [Executando o supervisor de atualização &#40;a interface do usuário&#41;](../../../2014/sql-server/install/running-upgrade-advisor-user-interface.md)   
 [Trabalhando com o Supervisor de Atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
