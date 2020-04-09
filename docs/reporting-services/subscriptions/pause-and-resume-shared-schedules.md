---
title: Pausar e retomar agendamentos compartilhados | Microsoft Docs
description: Neste artigo, você aprenderá a pausar e retomar uma agenda compartilhada que está em uso, mas não em andamento. É possível pausar e retomar em modo nativo ou no modo do SharePoint.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
helpviewer_keywords:
- pausing schedules
- report-specific schedules [Reporting Services]
- shared schedules [Reporting Services], resuming
- resuming schedules
- continuing schedules
- schedules [Reporting Services], resuming
- schedules [Reporting Services], pausing
ms.assetid: e416be75-5234-4aa6-a3de-77f60f25169a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 93a24bc7b76ba780ccd8136eb75702f8c3b236ef
ms.sourcegitcommit: c6a2efe551e37883c1749bdd9e3c06eb54ccedc9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2020
ms.locfileid: "80742100"
---
# <a name="pause-and-resume-shared-schedules"></a>Pause and Resume Shared Schedules
  Você pode pausar e retomar uma agenda compartilhada em uso. Pausar uma agenda compartilhada é uma maneira de congelar temporariamente uma agenda usada para disparar o processamento de relatórios e assinaturas. Somente agendas compartilhadas podem ser pausadas e reiniciadas. Não é possível pausar agendas específicas a relatórios.  
  
 Não é possível pausar e retomar o processamento de um relatório em andamento. Você só pode pausar e retomar agendamentos que estejam na fila de agendamento do serviço SQL Server Agent. Um trabalho em andamento está fora do escopo do mecanismo de agendamento. Para obter mais informações, consulte [Gerenciar um processo em execução](../../reporting-services/subscriptions/manage-a-running-process.md)  
  
 Enquanto uma agenda compartilhada estiver pausada, todas as operações que teriam ocorrido são ignoradas. Ao permitir que uma agenda compartilhada continue, o processamento de relatórios e assinaturas ocorrerá no próximo horário agendado, usando o horário local do servidor. O servidor de relatórios do modo nativo ou aplicativos de serviço do SharePoint não compensa pelas operações agendadas que teriam ocorrido se o agendamento não tivesse sido pausado.  
  
 Neste tópico:  
  
-   [Pausar e retomar agendas compartilhadas (modo Nativo)](#bkmk_native)  
  
-   [Pausar e retomar agendas compartilhadas (modo SharePoint)](#bkmk_sharepoint)  
  
##  <a name="pause-and-resume-shared-schedules-native-mode"></a><a name="bkmk_native"></a> Pausar e retomar agendas compartilhadas (modo Nativo)  
 Para pausar e retomar uma agenda compartilhada, use a página Agendas no Gerenciador de Relatórios. Não é possível usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]; ele não oferece opções para pausar e retomar agendas. Para obter mais informações, consulte [Create, Modify, and Delete Schedules](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md).  
  
#### <a name="to-pause-or-resume-a-shared-schedule"></a>Para pausar ou retomar uma agenda compartilhada  
  
1.  No Gerenciador de Relatórios, clique em **Configurações do Site**.  
  
2.  Clique em **Agendas**.  
  
3.  Selecione a agenda e clique em **Pausar** ou em **Retomar** na faixa de opções. Se uma Agenda estiver pausada, a coluna **Status** conterá **Pausada**.  
  
##  <a name="pause-and-resume-shared-schedules-sharepoint-mode"></a><a name="bkmk_sharepoint"></a> Pausar e retomar agendas compartilhadas (modo SharePoint)  
 Para pausar e retomar uma agenda compartilhada, use a página Configurações do Site ou o PowerShell. As agendas são gerenciadas por site do SharePoint.  
  
#### <a name="to-pause-or-resume-a-shared-schedule"></a>Para pausar ou retomar uma agenda compartilhada  
  
1.  Clique em **Ações do Site**.  
  
2.  Clique em **Configurações de Site**.  
  
3.  Na seção Reporting Services, clique em **Gerenciar Agendas Compartilhadas**.  
  
4.  Selecione a agenda e clique em **Pausar Agendas Selecionadas** ou **Executar Agendas Selecionadas**. Se uma Agenda estiver pausada, a coluna **Status** conterá **Pausada**.  
  
## <a name="see-also"></a>Consulte Também  
 [Agendas](../../reporting-services/subscriptions/schedules.md)   
 [Criar, modificar e excluir agendas](../../reporting-services/subscriptions/create-modify-and-delete-schedules.md)   
 [Alterar as configurações de fuso horário e relógio em um servidor de relatório](../../reporting-services/subscriptions/change-time-zones-and-clock-settings-on-a-report-server.md)   
 [Gerenciar um processo em execução](../../reporting-services/subscriptions/manage-a-running-process.md)  
  
  
