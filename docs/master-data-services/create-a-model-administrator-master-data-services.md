---
title: Criar um administrador de modelo
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- administrators [Master Data Services], creating
ms.assetid: dae17afc-3b39-490e-b51f-2d8da26d429e
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 1a81be69eee7a0fa8ea61b4491a296552aca51ff
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85814015"
---
# <a name="create-a-model-administrator-master-data-services"></a>Criar um administrador de modelo (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], crie um administrador de modelos quando desejar que um grupo ou um usuário tenha todas as permissões para todos os objetos em um ou mais modelos.  
  
> [!TIP]  
>  Para simplificar a administração, crie um grupo local ou do Windows e configure-o como um administrador de modelo. Isso lhe permitirá adicionar e remover usuários do grupo sem acessar o [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)].  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Permissões de Usuário e Grupo** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-create-a-model-administrator"></a>Para criar um administrador de modelo  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Permissões de Usuário e Grupo**.  
  
2.  Na página **Usuários** ou **Grupos** , selecione a linha do usuário ou grupo que deseja editar.  
  
3.  Clique em **Editar usuário selecionado**.  
  
4.  Clique na guia **Modelos** .  
  
5.  Opcionalmente, selecione um modelo na lista **Modelo** .  
  
6.  Clique em **Editar**.  
  
7.  Clique no modelo ao qual você deseja atribuir permissão.  
  
8.  No menu, selecione **Administrador**.  
  
9. Conclua as etapas 7 e 8 para cada modelo do qual o grupo ou usuário deverá ser administrador.  
  
10. Clique em **Save** (Salvar).  
  
## <a name="see-also"></a>Consulte Também  
 [Administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)   
 [Atribuir permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)   
 [Atribuir permissões de membro de hierarquia &#40;Master Data Services&#41;](../master-data-services/assign-hierarchy-member-permissions-master-data-services.md)   
 [Permissões de objeto de modelo &#40;Master Data Services&#41;](../master-data-services/model-object-permissions-master-data-services.md)   
 [Permissões de membro de hierarquia &#40;Master Data Services&#41;](../master-data-services/hierarchy-member-permissions-master-data-services.md)  
  
  
