---
description: Perfis de Agente
title: Perfis de agente | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.profiles.perfprofiles.f1
helpviewer_keywords:
- Agent Profiles dialog box
ms.assetid: 0422e99c-e688-419b-bb4c-c7bebeef1d8d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 71c77753c578b825ca04ff26fbe172f9a990db16
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88380432"
---
# <a name="agent-profiles"></a>Perfis de Agente
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
   Use a caixa de diálogo **Perfis de Agente** para gerenciar perfis de agente. Perfis de agente fornecem um modo conveniente para gerenciar parâmetros em runtime para cada agente. Cada agente tem um perfil padrão e alguns agentes têm perfis adicionais predefinidos. Por exemplo, o Merge Agent tem um perfil de "vínculo lento" projetado para baixas conexões de largura de banda. Perfis predefinidos são suficientes para a maioria dos aplicativos, mas você também pode criar perfis definidos pelo usuário, que permite personalizar o comportamento do agente.  
  
## <a name="options"></a>Opções  
 **Selecionar uma página**  
 Selecione um agente no painel esquerdo e os perfis para o agente são exibidos no painel direito.  
  
 **Padrão para Novo**  
 Selecione o perfil que será usado quando são criados trabalhos para um agente de um determinado tipo. Por exemplo, se você criar um número de assinaturas para uma publicação de mesclagem, o trabalho do Merge Agent usará o perfil selecionado para cada assinatura. Se você quiser alterar o perfil dos trabalhos existentes, selecione um perfil e clique em **Alterar Agentes Existentes**.  
  
 **Nome**  
 O nome do perfil.  
  
 **Tipo**  
 O tipo de perfil: **Usuário** (definido pelo usuário) ou **Sistema** (predefinido).  
  
 **Propriedades (...)**  
 Clique para exibir os valores usados para cada parâmetro no perfil do agente.  
  
 **Novo**  
 Clique para criar um novo perfil.  
  
 **Delete (excluir)**  
 Selecione um perfil definido pelo usuário e então clique em **Excluir** para excluir aquele perfil. Perfis predefinidos não podem ser excluídos.  
  
 **Alterar Agentes Existentes**  
 Selecione um perfil e clique em **Alterar Agentes Existentes** para especificar que todos os trabalhos existentes, para um agente de um tipo específico, devem usar o perfil selecionado. Por exemplo, se você criou um número de assinaturas para uma publicação de mesclagem e quer alterar o perfil para especificar que um trabalho do Merge Agent para cada uma dessas assinaturas deve usar **Perfil do agente de vínculo lento**, selecione o perfil e clique em **Alterar Agentes Existentes**.  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhar com perfis do Agente de Replicação](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)   
 [Visão geral dos agentes de replicação](../../relational-databases/replication/agents/replication-agents-overview.md)   
 [Perfis do agente de replicação](../../relational-databases/replication/agents/replication-agent-profiles.md)  
  
  
