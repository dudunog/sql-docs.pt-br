---
title: Recursos do conjunto de sites do Reporting Services | Microsoft Docs
description: Saiba mais sobre os recursos do conjunto de sites do SharePoint que o modo SharePoint do SQL Server Reporting Services fornece.
ms.date: 09/25/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-sharepoint
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 052a6893f28d86a7f966edfe2a4b953ccc442e27
ms.sourcegitcommit: 66a0672e47415dbd5cfd8d19075102c8c3973e70
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764692"
---
# <a name="reporting-services-site-collection-features"></a>Recursos do conjunto de sites do Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

O modo do SharePoint do Reporting Services fornece três recursos do conjunto de sites do SharePoint. Os recursos dão suporte ao ambiente geral de relatório do modo do SharePoint do Reporting Services, [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], um recurso do Suplemento SQL Server 2016 Reporting Services e operações de gerenciamento para o Reporting Services na Administração Central do SharePoint.

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.
  
## <a name="site-collection-features"></a>Recursos do conjunto de sites

 A tabela a seguir descreve os membros do conjunto de sites do Reporting Services.  
  
|Recurso|Descrição|  
|-------------|-----------------|  
|**Recurso Administração Central do Servidor de Relatório**|Habilita os Recursos para o gerenciamento da integração com um servidor de relatório do Reporting Services. Esse recurso somente é instalado e usado na coleção de sites da Administração Central do SharePoint.<br /><br /> O recurso de integração do Servidor de Relatório é ativado automaticamente na coleção de sites da Administração Central do SharePoint depois que você instala o Suplemento [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] para produtos SharePoint. Em algumas situações, você precisa ativar o recurso manualmente. Para ativar o recurso de servidor do relatório, use as páginas do Reporting Services na página Configurações de Site da Administração Central do SharePoint.<br /><br /> A versão [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] e posterior do Reporting Services do Suplemento para produtos do SharePoint ativa o recurso de integração do servidor de relatório em todos os conjuntos de sites existentes quando o Suplemento é instalado. Além disso, o recurso fica ativo automaticamente para novos conjuntos de sites.|  
|**Recurso de Integração do Servidor de Relatório**|Permite relatórios avançados usando o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Reporting Services<br /><br /> Esse recurso está Ativo por padrão.|  
|**Recurso de Integração do Power View**|Habilita a exploração de dados interativa e a apresentação visual em pastas de trabalho [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , bem como bancos de dados de tabela do Analysis.Services.<br /><br /> O recurso pode ser acessado pelos menus de contexto das seguintes fontes de dados:<br /><br /> **.rdlx**<br /><br /> **.rsds**<br /><br /> Arquivo de conexão **.bism**<br /><br /> <br /><br /> Se [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)] não aparecer nos menus de contexto, verifique se o **Recurso de Integração do Power View** está ativado.<br /><br /> Esse recurso está desativado por padrão.|  

## <a name="next-steps"></a>Próximas etapas

[Ativar o servidor de relatório e os recursos de integração do Power View no SharePoint](../../reporting-services/report-server-sharepoint/site-collection-features-report-server-and-power-view.md)   
[Configurações de Site e Recursos de Site do Reporting Services &#40;Modo SharePoint&#41;](../../reporting-services/report-server-sharepoint/site-settings-and-features-reporting-services.md)   
[Ativar o recurso de sincronização de relatório do Servidor de Relatório na Administração Central do SharePoint](../../reporting-services/report-server-sharepoint/activate-the-report-server-file-sync-feature-in-sharepoint-ca.md)  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
