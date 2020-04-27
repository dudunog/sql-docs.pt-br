---
title: Configurar alertas de replicação predefinidos (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server replication]
- predefined replication alerts [SQL Server replication]
ms.assetid: c0414147-7ffe-4f9a-908c-71c1b5201584
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 103f461c29e2bd7534ad5cb96836f06c972a6c5e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63187265"
---
# <a name="configure-predefined-replication-alerts-sql-server-management-studio"></a>Configurar alertas de replicação predefinidos (SQL Server Management Studio)
  A replicação oferece os seguintes alertas predefinidos que podem ser configurados para responder aos eventos de replicação:  
  
-   **Replicação: êxito do agente**    
-   **Replicação: falha do agente**    
-   **Replicação: repetição do agente**    
-   **Replicação: assinatura expirada cancelada**    
-   **Replicação: assinatura reinicializada após falha de validação**    
-   **Replicação: falha na validação de dados do assinante**    
-   **Replicação: êxito na validação de dados do assinante**    
-   **Replicação: desligamento personalizado do agente**  
  
 Configure esses alertas na pasta **Alertas** no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou na guia **Avisos** no Replication Monitor. Para obter mais informações sobre como acessar essa guia, consulte [Exibir informações e executar tarefas usando o Replication Monitor](../monitor/view-information-and-perform-tasks-replication-monitor.md).  
  
 Além desses alertas, o Replication Monitor fornece um conjunto de avisos e alertas relacionado ao status e ao desempenho. Para obter mais informações, consulte [definir limites e avisos na infraestrutura de alertas do Replication Monitor](../monitor/set-thresholds-and-warnings-in-replication-monitor.md) . Para obter mais informações, consulte [Criar um evento definido pelo usuário](../../../ssms/agent/create-a-user-defined-event.md).  
  
### <a name="to-configure-a-predefined-replication-alert-in-management-studio"></a>Para configurar um alerta de replicação predefinido no Management Studio  
  
1.  Conecte-se ao Distribuidor no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e, em seguida, expanda o nó de servidor.    
2.  Expanda a pasta **SQL Server Agent** e então, expanda a pasta **Alertas** .    
3.  Clique com o botão direito do mouse em um alerta de replicação e então clique em **Propriedades**.    
4.  Defina as opções na caixa de diálogo ** \<Propriedades** do alerta de alerta do>:    
    -   Na página **Geral** , clique em **Habilitar**; especifique em qual banco de dados deverá ser aplicado o alerta.    
    -   Na página **Resposta** , especifique se deve ser enviado um e-mail e/ou se deverá ser executado um trabalho.  
  
         Se o alerta for **replicação: falha na validação de dados do assinante**, você pode especificar o trabalho de resposta que a replicação fornece para este alerta: selecione **Executar trabalho**e, em seguida, clique no botão procurar (**...**). Na caixa de diálogo **Localizar trabalho** , clique em **procurar**. Na caixa de diálogo **Procurar Objetos** , selecione **Reinicializar as assinaturas com falha na validação de dados**. Clique em **OK** em ambas as caixas de diálogo abertas. Quando o trabalho executar, usará um RPC (Remote Procedure Call) para um procedimento armazenado que reinicializará a assinatura. Se o Publicador selecionar um Distribuidor remoto, você deverá definir um logon de servidor remoto no Publicador, para que o RPC do Distribuidor ao Publicador possa ser realizado.   
    -   Na página **Opções** , personalize o texto da resposta.    
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-configure-an-alert-for-a-threshold-in-replication-monitor"></a>Para configurar um alerta para um limite no Replication Monitor  
  
1.  Na guia **Avisos** clique em **Configurar Alertas**.    
2.  Na caixa de diálogo **Configurar Alertas de Replicação** , selecione um alerta e então clique em **Configurar**.    
3.  Defina as opções na caixa de diálogo ** \<Propriedades** do alerta de alerta do>:    
    -   Na página **Geral** , clique em **Habilitar**; especifique em qual banco de dados deverá ser aplicado o alerta.    
    -   Na página **Resposta** , especifique se deve ser enviado um e-mail e/ou se deverá ser executado um trabalho.    
         Se o alerta for **replicação: falha na validação de dados do assinante**, você pode especificar o trabalho de resposta que a replicação fornece para este alerta: selecione **Executar trabalho**e, em seguida, clique no botão procurar (**...**). Na caixa de diálogo **Localizar trabalho** , clique em **procurar**. Na caixa de diálogo **Procurar Objetos** , selecione **Reinicializar as assinaturas com falha na validação de dados**. Clique em **OK** em ambas as caixas de diálogo abertas. Quando o trabalho executar, usará um RPC (Remote Procedure Call) para um procedimento armazenado que reinicializará a assinatura. Se o Publicador selecionar um Distribuidor remoto, você deverá definir um logon de servidor remoto no Publicador, para que o RPC do Distribuidor ao Publicador possa ser realizado.   
    -   Na página **Opções** , personalize o texto da resposta.    
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]    
5.  Clique em **Fechar**.  
  
## <a name="see-also"></a>Consulte Também  
 [Usar Alertas para eventos do Agente de Replicação](../agents/use-alerts-for-replication-agent-events.md)  
  
  
