---
title: Validar uma versão em relação a regras de negócio
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- validating versions [Master Data Services]
- validating versions [Master Data Services], about validating versions
- versions [Master Data Services], validating
- business rules [Master Data Services], applying to all members
ms.assetid: 5aee7901-6d05-41d4-8bbb-c6f26791d1df
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 66a934d1cddad1e7fdb2e36291611fa50e9c8ce5
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85813192"
---
# <a name="validate-a-version-against-business-rules-master-data-services"></a>Validar uma versão em relação a regras de negócio (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], valide uma versão para aplicar regras de negócio a todos os membros da versão do modelo.  
  
 Este procedimento explica como usar o aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] para validar dados. Se você tiver permissão no banco de dados MDS, poderá usar um procedimento armazenado no lugar. Para obter mais informações, consulte [Procedimento armazenado de validação &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md).  
  
> [!NOTE]  
>  Todos os membros deverão ser validados antes que uma versão possa ser confirmada.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   Você deve ter permissão para acessar a área funcional **Gerenciamento de Versões** .  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
-   O status da versão deve ser **Aberto** ou **Bloqueado**.  
  
-   Na página **Validar Versões** , os membros devem existir com um status diferente de **Validação bem-sucedida**.  
  
### <a name="to-validate-a-version"></a>Para validar uma versão  
  
1.  No [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], clique em **Gerenciamento de Versões**.  
  
2.  Na página **Gerenciar Versões** , na barra de menus, clique em **Validar Versão**.  
  
3.  Na página **Validar Versões** , selecione o modelo e a versão que você deseja validar.  
  
4.  Clique em **Validar**.  
  
5.  Na caixa de diálogo de confirmação, clique em **OK**.  
  
    > [!NOTE]  
    >  Quando o indicador de progresso já não for exibido, isso significará que a versão concluiu a validação.  
  
## <a name="next-steps"></a>Próximas etapas  
  
-   [Bloquear uma versão &#40;Master Data Services&#41;](../master-data-services/lock-a-version-master-data-services.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Status de validação &#40;Master Data Services&#41;](../master-data-services/validation-statuses-master-data-services.md)   
 [Procedimento armazenado de validação &#40;Master Data Services&#41;](../master-data-services/validation-stored-procedure-master-data-services.md)   
 [Versões &#40;Master Data Services&#41;](../master-data-services/versions-master-data-services.md)   
 [Regras de negócio &#40;Master Data Services&#41;](../master-data-services/business-rules-master-data-services.md)   
 [Validar membros específicos em relação a regras de negócio &#40;Master Data Services&#41;](../master-data-services/validate-specific-members-against-business-rules-master-data-services.md)  
  
  
