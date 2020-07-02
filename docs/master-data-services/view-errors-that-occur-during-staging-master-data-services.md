---
title: Exiba os erros ocorridos durante o preparo
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- staging process [Master Data Services], viewing errors
ms.assetid: 6d2bff84-624b-47fc-a4a5-d9ea01d13412
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: af131613399fd45dd363f21f9f92216556be456b
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85812301"
---
# <a name="view-errors-that-occur-during-staging-master-data-services"></a>Exibir erros que ocorrem durante o preparo (Master Data Services)

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  No [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)], você pode exibir os erros ocorridos durante o processo de preparo. No banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , há duas exibições que mostram erros:  
  
-   stg.viw_name_MemberErrorDetails para atualizações de membro folha ou consolidado.  
  
-   stg.viw_name_RelationshipErrorDetails para atualizações de relação de hierarquia.  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Para executar esse procedimento:  
  
-   No banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] , você deve ter permissões SELECT para a exibição stg.viw_name_MemberErrorDetails ou stg.viw_name_RelationshipErrorDetails.  
  
-   Você deve ser um administrador de modelo. Para obter mais informações, consulte [administradores &#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md).  
  
### <a name="to-view-staging-errors"></a>Para exibir erros de preparo  
  
1.  Abra o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] e conecte-se à instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] de seu banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  
  
2.  Abra uma nova consulta.  
  
3.  Digite o texto a seguir, substituindo name pelo nome de sua tabela de preparo, por exemplo, viw_Product_MemberErrorDetails.  
  
     `SELECT * FROM stg.viw_name_MemberErrorDetails`  
  
4.  Execute a consulta. Os detalhes do erro são exibidos no campo **ErrorDescription** .  
  
## <a name="next-steps"></a>Próximas etapas  
 Para obter mais detalhes sobre mensagens de erro, consulte [Erros de processo de preparo &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral: importando dados de tabelas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [Solucionando problemas do processo de preparo (Master Data Services)](https://social.technet.microsoft.com/wiki/contents/articles/troubleshooting-the-staging-process-master-data-services.aspx)  
  
  
