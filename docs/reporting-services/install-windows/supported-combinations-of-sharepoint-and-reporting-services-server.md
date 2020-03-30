---
title: Combinações compatíveis do SharePoint e do servidor do Reporting Services | Microsoft Docs
description: Um relatório de servidor do SQL Server Reporting Services instalado no modo do SharePoint exige uma versão do SharePoint e o suplemento SQL Server Reporting Services (rsSharePoint.msi) para produtos do SharePoint, que é instalado nos servidores do SharePoint.
ms.date: 12/04/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint
ms.custom: seo-lt-2019, seo-mmd-2019
ms.topic: conceptual
helpviewer_keywords:
- SharePoint mode
- add-in for sharepoint
- rsSharePoint
ms.assetid: dc6a3372-db26-43f0-b7aa-f725acc635c2
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 56da894b141733357ff33ec820073c52836e4cca
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74866059"
---
# <a name="supported-combinations-of-sharepoint-and-reporting-services-server"></a>Combinações com suporte do SharePoint e do servidor do Reporting Services

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Um relatório de servidor do SQL Server Reporting Services instalado no modo do SharePoint exige uma versão do SharePoint e o suplemento SQL Server Reporting Services (rsSharePoint.msi) para produtos do SharePoint, que é instalado nos servidores do SharePoint. Este tópico resume as combinações com suporte.

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.

## <a name="supported-combinations-of-sharepoint-and-reporting-services-components"></a>Combinações com suporte de componentes do SharePoint e do Reporting Services

 A tabela a seguir resume as combinações com suporte do servidor de relatório, o suplemento do Reporting Services para produtos SharePoint e produtos SharePoint. As combinações que não estão listadas na tabela a seguir não têm suporte

### <a name="supported-combinations"></a>Combinações com suporte

||Servidor de relatório|Suplemento|Versão do SharePoint|
|-|-------------------|-------------|------------------------|
|1|SQL Server 2016|SQL Server 2016|SharePoint 2016|
|2|SQL Server 2016|SQL Server 2016|SharePoint 2013|
|3|SQL Server 2014|SQL Server 2014|SharePoint 2013|
|4|SQL Server 2014|SQL Server 2014|SharePoint 2010|
|5|SQL Server 2012 SP4|SQL Server 2014 e SQL Server 2012 SP4|SharePoint 2013|
|6|SQL Server 2012 SP3|SQL Server 2014 e SQL Server 2012 SP3|SharePoint 2013|
|7|SQL Server 2012 SP2|SQL Server 2014 e SQL Server 2012 SP2|SharePoint 2013|
|8|SQL Server 2012 SP1|SQL Server 2014 e SQL Server 2012 SP1|SharePoint 2013|
|9|SQL Server 2012 e SQL Server 2012 SP1*|SQL Server 2014|SharePoint 2010|
|10|SQL Server 2012|SQL Server 2012|SharePoint 2010|
|11|SQL Server 2008 R2|SQL Server 2014|SharePoint 2010|
|12|SQL Server 2008 R2|SQL Server 2012 e SQL Server 2012 SP1 ou posterior|SharePoint 2010|
|13|SQL Server 2008 R2|SQL Server 2008 R2|SharePoint 2010|
|14|SQL Server 2008 R2|SQL Server 2008 SP2|SharePoint 2007|
|15|SQL Server 2008 SP2|SQL Server 2008 R2|SharePoint 2010|
|16|SQL Server 2008 SP2|SQL Server 2008 e SQL Server 2008 SP2|SharePoint 2007|

 *Exceção: a integração do Power View não tem suporte.

 Para obter links para as páginas de download de suplementos, consulte [Onde encontrar o suplemento Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md).  

 **Considerações adicionais:**

- Certifique-se de atualizar todos os servidores do SharePoint no farm. Isso inclui os servidores front-end da Web e de aplicativos.

- O suporte do SharePoint 2016, inclusive integração do Power View, requer o servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e a versão do suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do SQL Server 2016 ou posterior.

- O suporte do SharePoint 2013, inclusive integração do Power View, requer o servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e a versão do suplemento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] do SQL Server 2012 SP1 ou posterior.

- O Power View foi introduzido no SQL Server 2012. Portanto, a integração do Power View ao SharePoint 2010 exige o SQL Server 2012 ou posterior do suplemento.

- O suplemento SQL Server 2008 R2 não é compatível com os servidores de relatório do SQL Server 2012 (ou posterior). O instalador de pré-requisito do SharePoint 2010 instala automaticamente o suplemento SQL Server 2008 R2. Ele deve ser desinstalado antes de instalar versões mais recentes do suplemento. A atualização no local do suplemento não tem suporte.

- **Atualização:** o SharePoint 2010 com o suplemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado não pode ser atualizado no local para o SharePoint 2013. O SharePoint 2013 exige o SQL Server 2012 SP1 ou posterior do suplemento e do servidor de relatório do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obter mais informações, consulte [Atualizar e migrar o Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).

## <a name="next-steps"></a>Próximas etapas

 [Onde encontrar o suplemento Reporting Services para produtos do SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)   
 [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-components-of-sql-server-2017.md)   
 [Requisitos de hardware e software para a instalação do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
