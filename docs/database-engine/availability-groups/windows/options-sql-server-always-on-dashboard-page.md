---
title: Painel do grupo de disponibilidade no SSMS
description: Conheça a página Opções encontrada no Painel do Always On do SQL Server no SQL Server Management Studio.
ms.custom: seodec18
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: availability-groups
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Alwayson.Dashboard
ms.assetid: 4369b588-e982-4b57-80a1-beb2e879ce0b
author: cawrites
ms.author: chadam
ms.openlocfilehash: b465e35420035a9c6c10bd8db53a680baf57a4da
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97643542"
---
# <a name="options-sql-server-always-on-dashboard-page"></a>Opções (SQL Server AlwaysOn, página Painel)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

  Use a página **Painel do SQL Server AlwaysOn** da caixa de diálogo [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]**Opções** para configurar o Painel do AlwaysOn.  
  
 **Para acessar essa página:**  
  
 No menu **Ferramentas** , clique em **Opções**, expanda a pasta **SQL Server AlwaysOn** e clique em **Painel**.  
  
## <a name="on-this-page"></a>Nessa página  
 **Ativar atualização automática.**  
 Clique para habilitar a atualização automática. As opções são:  
  
-   O campo **Intervalo de atualização (em segundos)** exibe o número de segundos nos quais o painel será atualizado. O valor padrão é 30. Quando a atualização automática estiver habilitada, você poderá editar esse campo para alterar o intervalo de atualização.  
  
-   O **Número de tentativas de conexão** exibe o número de vezes que o painel tentará se conectar a uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que hospeda uma réplica de disponibilidade para um grupo de disponibilidade que o Painel está monitorando. O valor padrão é 65535. Quando a atualização automática estiver habilitada, você poderá editar esse campo para alterar o número de tentativas de conexão.  
  
 **Habilite sua política de AlwaysOn definida pelo usuário.**  
 Se você tiver definido sua própria política de AlwaysOn, clique nessa opção para habilitar sua política.  
  
## <a name="see-also"></a>Consulte Também  
 [Usar o Painel AlwaysOn &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
