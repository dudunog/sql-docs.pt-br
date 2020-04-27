---
title: Página Configuração da Web (Gerenciador de Configuração do Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.webconfigpg.f1
ms.assetid: 7b900778-0169-4e42-9faf-98dc1c01313e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 12ba4a2d03e98d5f2dac79917e23a93c0a24cdb0
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65481215"
---
# <a name="web-configuration-page-master-data-services-configuration-manager"></a>Página Configuração da Web (Gerenciador de Configuração do Master Data Services)
  Use a página **Configuração da Web** para criar um novo site ou aplicativo Web. Depois de selecionar um aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , você poderá especificar o banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] do aplicativo e habilitar o Data Quality Services.  
  
## <a name="configure-the-web-application"></a>Configurar o aplicativo Web  
  
|Nome do controle|Descrição|  
|------------------|-----------------|  
|**Site**|Crie um novo site, selecione o site padrão ou selecione outro site disponível (se estiver listado). Esta lista exibe os sites que são definidos no ISS (Serviços de Informações da Internet) no computador local. Quando você cria um novo site, um novo aplicativo Web é criado automaticamente. Quando você selecionar o padrão ou outro site existente, crie um aplicativo manualmente.|  
|**Aplicativo Web**|Selecione um aplicativo Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] para configuração. Esta caixa mostra os aplicativos Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] apenas no site selecionado.<br /><br /> Se nada for exibido, clique em **Criar Aplicativo** para criar um site.|  
|**Criar aplicativo**|Abre a caixa de diálogo **Criar Aplicativo Web** , na qual você cria um aplicativo Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] no site selecionado. Este botão é habilitado apenas quando o site selecionado não tem aplicativo Web raiz configurado como o aplicativo Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] .|  
  
## <a name="associate-application-with-database"></a>Associar um aplicativo ao banco de dados  
  
|Nome do controle|Descrição|  
|------------------|-----------------|  
|**Selecionar**|Abre a caixa de diálogo **Conectar ao Servidor** , na qual você se conecta a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e seleciona um banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para associar ao aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] selecionado.|  
|**Instância do SQL Server**|Exibe o nome da instância selecionada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que hospeda o banco de dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Esse é um espaço em branco até você se conectar a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e selecionar um banco de dados.|  
|**Backup de banco de dados**|Exibe o nome do banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] associado ao aplicativo Web do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] selecionado. Esse é um espaço em branco até você se conectar a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e selecionar um banco de dados.|  
  
## <a name="enable-dqs-integration"></a>Habilitar a integração DQS  
  
|Nome do controle|Descrição|  
|------------------|-----------------|  
|**Habilitar a integração com o Data Quality Services**|Selecione esta opção para habilitar a funcionalidade Data Quality disponível no [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)][!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]. Para obter mais informações, consulte [Habilitar a integração do Data Quality Services com Master Data Services](install-windows/enable-data-quality-services-integration-with-master-data-services.md).|  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar o banco de dados e o site para Master Data Services](../../2014/master-data-services/set-up-the-database-and-website-for-master-data-services.md)   
 [Requisitos do aplicativo Web &#40;Master Data Services&#41;](install-windows/web-application-requirements-master-data-services.md)   
 [Criar um aplicativo Web Master Data Manager &#40;Master Data Services&#41;](install-windows/create-a-master-data-manager-web-application-master-data-services.md)   
 [MDS 2014 e erro "Serviço indisponível"](https://blogs.msdn.com/b/womeninanalytics/archive/2015/08/19/mds-2014-and-service-unavailable-error.aspx)  
  
  
