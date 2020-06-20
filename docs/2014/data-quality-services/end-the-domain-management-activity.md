---
title: Encerrar a atividade de gerenciamento de domínio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: ab6505ad-3090-453b-bb01-58435e7fa7c0
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 16e030b52e4c7f99368efd8054f87df495b67257
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937707"
---
# <a name="end-the-domain-management-activity"></a>Terminar a atividade Gerenciamento de Domínio
  Este tópico descreve como concluir, fechar ou cancelar a atividade de gerenciamento de domínio no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). O gerenciamento de domínio não é executado por um assistente, portanto, os controles descritos abaixo podem ser usados de qualquer uma das páginas da atividade de gerenciamento de domínio.  
  
## <a name="end-domain-management"></a>Gerenciamento de Domínio de Fim  
 **Concluir**  
 Clique para concluir o gerenciamento de domínio. Será exibido um pop-up que permite que você faça o seguinte:  
  
-   **Sim – Publique a base de dados de conhecimento e saia**: a base de dados de conhecimento será publicada para uso do usuário atual ou de outros usuários. A base de dados de conhecimento não será bloqueada, o estado da base de dados de conhecimento (na tabela de bases de dados de conhecimento) será definido como vazio e as atividades de Gerenciamento de Domínio e Descoberta da Base de Dados de Conhecimento estarão disponíveis. Você será retornado à tela Abrir Base de Dados de Conhecimento.  
  
-   **Não-salve o trabalho na base de dados de conhecimento e saia**: seu trabalho será salvo, a base de dados de conhecimento permanecerá bloqueada e o estado da base de dados de conhecimento será definido como em funcionamento. As atividades de Gerenciamento de Domínio e Descoberta da Base de Dados de Conhecimento estarão disponíveis. Você será retornado à home page.  
  
-   **Cancelar – Mantenha-se na tela atual**: o pop-up será fechado e você será retornado para a tela Gerenciamento de Domínio.  
  
 **Cancelar**  
 Clique para encerrar a atividade de Gerenciamento de Domínio, o que resultará na perda do trabalho, e retorne à página inicial do DQS.  
  
 **Fechar**  
 Clique para salvar seu trabalho e retornar para a home page do DQS. A base de conhecimento será bloqueada e o estado da base de conhecimento na tabela de base de conhecimento na tela **Abrir Base de Dados de Conhecimento** será **Gerenciamento de Domínio**. Depois de clicar em **Fechar**para executar a atividade de Gerenciamento de Domínio, você precisará retornar para a tela **Gerenciamento de Domínio** , clicar em **Concluir**e, em seguida, clicar em **Sim** para publicar a base de conhecimento ou em **Não** para salvar o trabalho na base de conhecimento e sair.  Para obter mais informações sobre como abrir uma base de dados de conhecimento bloqueada, consulte [Open a Knowledge Base](../../2014/data-quality-services/open-a-knowledge-base.md).  
  
  
