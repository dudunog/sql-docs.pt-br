---
title: SQL Server grupo de serviço Web do servidor de relatório 2005 detectado (Supervisor de atualização) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- deployment [Reporting Services]
ms.assetid: 699d24eb-7756-4b41-9294-ef1a94b2f267
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: bfeff5eae569b481edfcc1cacc89c26e44edaece
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952369"
---
# <a name="sql-server-2005-report-server-web-service-group-detected-upgrade-advisor"></a>Grupo do serviço Web do servidor de relatório do SQL Server 2005 foi detectado (Supervisor de Atualização)
  O supervisor de atualização detectou que a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] está associada a um grupo de serviço Web do servidor de relatório.  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo nativo.|  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
## <a name="description"></a>Descrição  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não usa o grupo [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] de serviço Web servidor de relatórios. Quando você fizer a atualização do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], esse grupo de serviço será excluído e as listas de controle de acesso (ACLs) personalizadas desse grupo ou de usuários que pertencem a ele não serão mantidas durante a atualização.  
  
## <a name="corrective-action"></a>Ação corretiva  
 Antes da atualização, faça um backup de todas as ACLs personalizadas ou usuários pertencentes ao grupo de serviço Web do servidor de relatório do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para fazer isso, você pode usar a ferramenta de linha de comando **icacls. exe** no [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] SP2 e posterior ou a ferramenta de linha de comando Cacls. exe em sistemas operacionais Windows anteriores [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] ao SP2. Para obter mais informações sobre a sintaxe dessas ferramentas, consulte a documentação do Windows. Concluída a instalação com êxito, aplique as ACLs personalizadas ou os usuários ao grupo do Windos do servidor de relatório do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] da instância do servidor de relatório. O [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] grupo servidor de relatório do Windows assume a forma de\<SQLServerReportServerUser $*computer_name*>$\<*instance_name*>.  
  
## <a name="see-also"></a>Consulte Também  
 [Problemas de atualização do Reporting Services &#40;o supervisor de atualização&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
  
