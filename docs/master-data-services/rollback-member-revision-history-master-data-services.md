---
description: Reverter Histórico de Revisões do Membro (Master Data Services)
title: Reverter Histórico de Revisões do Membro
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d39d3474-20e7-429f-9c8d-fcc4eb0854fc
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: fe275fe7aef826b3eeaa6ef6e959f8c8bea33b4f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461718"
---
# <a name="rollback-member-revision-history-master-data-services"></a>Reverter Histórico de Revisões do Membro (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Um histórico de revisões do membro é registrado sempre que um membro é alterado. Você pode reverter um histórico de revisões do membro para uma versão anterior.  
  
## <a name="prerequisites"></a>Pré-requisitos  
  
-   Você deve ter permissão para atualizar pelo menos um dos atributos do membro selecionado. Quando você reverter um histórico de revisões, todos os valores do atributo que podem ser atualizados serão revertidos para os valores da versão anterior.  
  
-   O histórico de revisões só estará disponível quando o tipo do log de transações da entidade for um membro.  
  
 **Para reverter um histórico de revisões do membro**  
  
1.  No Master Data Manager, clique em Explorer.  
  
2.  Escolha a entidade e o membro para a reversão.  
  
3.  Clique em **Exibir Histórico.**  
  
4.  Escolha a revisão para reverter e, em seguida, clique em **Reverter**.  
  
## <a name="see-also"></a>Consulte Também  
 [Histórico de revisão do membro &#40;Master Data Services&#41;](../master-data-services/member-revision-history-master-data-services.md)   
 [Alterar o tipo de log de transações de entidade &#40;Master Data Services&#41;](../master-data-services/change-the-entity-transaction-log-type-master-data-services.md)  
  
  
