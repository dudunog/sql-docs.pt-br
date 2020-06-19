---
title: Excluir um membro ou coleção (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- collections [Master Data Services], deleting
- leaf members [Master Data Services], deleting
- deleting members [Master Data Services]
- members [Master Data Services], deleting
- consolidated members [Master Data Services], deleting
ms.assetid: 519130a7-4226-4d71-9124-d2ee0ce7e5bd
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: c37f57da9651cad37a3ac4bb267efb3da05d7616
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971603"
---
# <a name="delete-a-member-or-collection-master-data-services"></a>Excluir um membro ou uma coleção (Master Data Services)
  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], exclua um membro ou coleção quando não precisar mais dele. Se você quiser excluir membros em massa, use o processo de preparo. Para obter mais informações, consulte [desativar ou excluir membros usando o processo de preparo &#40;Master Data Services&#41;](add-update-and-delete-data-master-data-services.md).  
  
> [!NOTE]  
>  Você não poderá excluir um membro se ele for usado como um valor de atributo baseado em domínio de outro membro.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional do **Gerenciador** .  
  
-   Para membros, você deve ter, no mínimo, a permissão **Atualizar** para o objeto de modelo folha do qual você está excluindo um membro.  
  
-   Para coleções, você deve ter, no mínimo, a permissão de **Atualizar** para o objeto da coleção de folhas que você está excluindo.  
  
### <a name="to-delete-a-member-or-collection"></a>Para excluir um membro ou uma coleção  
  
1.  Na home page do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , na lista **Modelo** , selecione um modelo.  
  
2.  Na lista **Versão** , selecione uma versão.  
  
3.  Clique em **Gerenciador**.  
  
4.  Para excluir:  
  
    -   Um membro folha, na barra de menus, aponte para **Entidades** e clique no nome da entidade que contém o membro.  
  
    -   Um membro consolidado, na barra de menus, aponte para **Hierarquias** e clique no nome da hierarquia que contém o membro. Em seguida, o nó na hierarquia que contém o membro.  
  
    -   Uma coleção, na barra de menus, aponte para **Coleções** e clique no nome da entidade que contém a coleção.  
  
5.  Na grade, clique na linha do membro ou coleção que você deseja excluir.  
  
6.  Clique **Excluir Membro**, **Excluir**ou **Excluir Coleção**.  
  
7.  Na caixa de diálogo de confirmação, clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [Reativar um membro ou uma coleção &#40;Master Data Services&#41;](../../2014/master-data-services/reactivate-a-member-or-collection-master-data-services.md)   
 [Membros &#40;Master Data Services&#41;](../../2014/master-data-services/members-master-data-services.md)   
 [Coleções &#40;Master Data Services&#41;](../../2014/master-data-services/collections-master-data-services.md)  
  
  
