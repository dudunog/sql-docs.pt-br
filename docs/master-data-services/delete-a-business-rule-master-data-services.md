---
title: Excluir uma regra de negócio
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deleting business rules [Master Data Services]
- business rules [Master Data Services], deleting
ms.assetid: b97aa4f9-569f-451d-ad62-65b81f980299
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: d6af3aac4ac8e2a1a4026162eb6ab5f6038b5eed
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73729409"
---
# <a name="delete-a-business-rule-master-data-services"></a>Excluir uma regra de negócio (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], exclua uma regra de negócio quando ela não for mais necessária.  
  
> [!NOTE]  
>  Você pode evitar a validação de dados em relação a uma regra de negócio excluindo-a. Para obter mais informações, consulte [Excluir uma regra de negócio &#40;Master Data Services&#41;](../master-data-services/exclude-a-business-rule-master-data-services.md).  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Administração do sistema** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-delete-a-business-rule"></a>Para excluir uma regra de negócio  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Administração do Sistema**.  
  
2.  Na barra de menus, aponte para **Gerenciar** e clique em **Regras de Negócios**.  
  
3.  Na página **regras de negócio** , na lista suspensa **modelo** , selecione um modelo.  
  
4.  Na lista suspensa **Entidade** , escolha uma entidade.  
  
5.  Na lista suspensa **Tipos de Membro** , selecione um tipo de membro ao qual a regra de negócio será aplicada.  
  
6.  Na grade, clique na linha da regra de negócios que você deseja excluir.  
  
7.  Clique em **Excluir**.  
  
8.  Na caixa de diálogo de confirmação, clique em **OK**. O valor da coluna **Estado da Regra de Negócios** é **Exclusão pendente**.  
  
9. Clique em **Publicar Tudo**.  
  
10. Na caixa de diálogo de confirmação, clique em **OK**. A regra de negócio excluída não é mais exibida na grade.  
  
## <a name="see-also"></a>Consulte Também  
 [Excluir uma regra de negócio &#40;Master Data Services&#41;](../master-data-services/exclude-a-business-rule-master-data-services.md)   
 [Criar e publicar uma regra de negócio &#40;Master Data Services&#41;](../master-data-services/create-and-publish-a-business-rule-master-data-services.md)   
 [Regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)  
  
  
