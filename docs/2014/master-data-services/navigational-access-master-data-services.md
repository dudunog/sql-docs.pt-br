---
title: Acesso de navegação (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- navigational access [Master Data Services]
- security [Master Data Services], navigational access
ms.assetid: 3403b7b0-44e2-48c3-a1b7-9c4612b874b8
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 1d190d55c45530adde1b41658c975bbfc19c0b91
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65482632"
---
# <a name="navigational-access-master-data-services"></a>Acesso de navegação (Master Data Services)
  O acesso de navegação se aplica à segurança do objeto do modelo que é atribuída na guia **Modelos** .  
  
 O acesso de navegação é o acesso que você obtém a níveis mais altos do que o acesso ao qual você atribuiu segurança.  
  
 Neste exemplo, as permissões são atribuídas a uma entidade e, portanto, o acesso de navegação é concedido no nível do modelo.  
  
 ![mds_conc_inheritance_model](../../2014/master-data-services/media/mds-conc-inheritance-model.gif "mds_conc_inheritance_model")  
  
 **Entities**  
  
 Quando você atribui permissão a uma entidade, seus membros folha ou seus membros consolidados, o acesso de navegação significa que você pode ler ou atualizar o nome e o código de todos os membros. Você também pode ler o nome do modelo.  
  
 **Atributos**  
  
 Quando você atribui permissão a um atributo, o acesso de navegação significa que você pode ler ou atualizar o nome e o código de todos os membros da entidade. Você também pode ler o nome do modelo.  
  
 **Coleções**  
  
 Quando atribui permissões a coleções, você pode ler ou atualizar o nome, o código, a descrição e a ID do proprietário. Você também pode ler o nome do modelo.  
  
## <a name="see-also"></a>Consulte Também  
 [Como as permissões são determinadas &#40;Master Data Services&#41;](how-permissions-are-determined-master-data-services.md)  
  
  
