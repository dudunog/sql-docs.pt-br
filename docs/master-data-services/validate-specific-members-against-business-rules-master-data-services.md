---
title: Validar membros específicos em relação a regras de negócio
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- applying business rules [Master Data Services]
- business rules [Master Data Services], applying to select members
ms.assetid: 2288ef43-5392-47ea-b651-ec25e5692a14
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ae7e5a0419e57d24a2f2d16b6b3407f2fb75bc77
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85812852"
---
# <a name="validate-specific-members-against-business-rules-master-data-services"></a>Validar membros específicos em relação a regras de negócio (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], aplique regras de negócio seletivamente quando desejar atualizar ou validar subconjuntos de membros com base em regras de negócio.  
  
> [!NOTE]  
>  Se você deseja aplicar regras de negócio a todos os membros em uma versão de um modelo, consulte [Validar uma versão em relação a regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
-   Você deve ter, no mínimo, a permissão **Atualizar** para o objeto de modelo ao qual está aplicando regras de negócio.  
  
### <a name="to-apply-business-rules-selectively"></a>Para aplicar regras de negócio seletivamente.  
  
1.  Na home page do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , na lista suspensa **Modelo** , selecione um modelo.  
  
2.  Na lista suspensa **Versão** , selecione uma versão.  
  
3.  Clique na guia **Gerenciador** .  
  
4.  Na barra de menus, aponte para **Entidades** e clique no nome da entidade que contém os membros aos quais você deseja aplicar regras.  
  
5.  Clique em **Aplicar Regras**. As regras de negócio são aplicadas apenas aos membros exibidos na grade.  
  
## <a name="see-also"></a>Consulte Também  
 [Validar uma versão em relação às regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-a-version-against-business-rules-master-data-services.md)   
 [Regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
