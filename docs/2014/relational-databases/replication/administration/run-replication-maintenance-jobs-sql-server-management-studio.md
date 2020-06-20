---
title: Executar trabalhos de manutenção de replicação (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server replication]
ms.assetid: 0dc485a0-5a50-41eb-a29d-f2b2fb920174
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 74c00479e5587c8662d81e554cae5add2e295183
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068760"
---
# <a name="run-replication-maintenance-jobs-sql-server-management-studio"></a>Executar trabalhos de manutenção de replicação (SQL Server Management Studio)
  A replicação usa os seguintes trabalhos de manutenção:  
  
-   **Reinicializar assinaturas com falha na validação de dados**
-   **Limpeza de histórico de agente: distribuição**
-   **Atualizador de monitoramento de replicação para distribuição.**
-   **Verificação de agentes de replicação**
-   **Limpeza de distribuição: distribuição**
-   **Limpeza de assinaturas expiradas**  
  
 Inicie e pare esses trabalhos na pasta **Trabalhos** do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] e na guia **Agentes** do Replication Monitor. Para obter informações sobre como iniciar o Replication Monitor, consulte [Start the Replication Monitor](../monitor/start-the-replication-monitor.md) (Iniciar o Replication Monitor). Exiba e modifique as propriedades de cada trabalho na caixa de diálogo **Propriedades do trabalho – \<Job> ** que está disponível na mesma pasta e guia.  
  
### <a name="to-start-or-stop-a-replication-maintenance-job-in-management-studio"></a>Para iniciar ou parar um trabalho de manutenção de replicação no Management Studio  
  
1.  Conecte-se ao Distribuidor no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e, em seguida, expanda o nó de servidor.  
  
2.  Expanda a pasta **SQL Server Agent** e, em seguida, a pasta **Trabalhos** .  
  
3.  Clique com o botão direito do mouse em um trabalho e então clique em **Iniciar Trabalho** ou **Parar Trabalho**.  
  
### <a name="to-start-or-stop-a-replication-maintenance-job-in-replication-monitor"></a>Para iniciar ou parar um trabalho de manutenção de replicação no Replication Monitor  
  
1.  Expanda um Grupo do publicador no Replication Monitor e, então, selecione um Publicador.  
  
2.  Clique na guia **Agentes** .  
  
3.  Clique com o botão direito do mouse em um trabalho na grade e então clique em **Iniciar Trabalho** ou **Parar Trabalho**.  
  
### <a name="to-view-and-modify-properties-for-a-replication-maintenance-job-in-management-studio"></a>Para exibir e modificar propriedades de um trabalho de manutenção de replicação no Management Studio  
  
1.  Conecte-se ao Distribuidor no [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]e, em seguida, expanda o nó de servidor.  
  
2.  Expanda a pasta **SQL Server Agent** e, em seguida, a pasta **Trabalhos** .  
  
3.  Clique com o botão direito do mouse em um trabalho e clique em **Propriedades**.  
  
4.  Na caixa de diálogo **Propriedades \<Job> do trabalho –** , modifique todas as propriedades, se necessário, e clique em **OK**.  
  
### <a name="to-view-and-modify-properties-for-a-replication-maintenance-job-in-replication-monitor"></a>Para exibir e modificar propriedades de um trabalho de manutenção de replicação no Replication Monitor  
  
1.  Expanda um Grupo do publicador no Replication Monitor e, então, selecione um Publicador.  
  
2.  Clique na guia **Agentes** .  
  
3.  Clique com o botão direito do mouse em um trabalho na grade e então clique em **Propriedades**.  
  
4.  Na caixa de diálogo **Propriedades \<Job> do trabalho –** , modifique todas as propriedades, se necessário, e clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciar e parar um agente de replicação &#40;SQL Server Management Studio&#41;](../agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)   
 [Exibir informações e executar tarefas usando o Replication Monitor](../monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Administração do agente de replicação](../agents/replication-agent-administration.md)  
  
  
