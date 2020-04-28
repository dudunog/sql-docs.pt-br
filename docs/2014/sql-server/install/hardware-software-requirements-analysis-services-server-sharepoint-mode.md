---
title: Requisitos de hardware e software para o Analysis Services Server no modo do SharePoint (SQL Server 2014) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: database-engine
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.topic: conceptual
ms.custom: ''
ms.date: 06/13/2017
ms.openlocfilehash: 8f645ca9bdb6176505a6277af0f0482be5b62f09
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75245609"
---
# <a name="hardware-and-software-requirements-for-analysis-services-server-in-sharepoint-mode-sql-server-2014"></a>Requisitos de hardware e software para servidor do Analysis Services no modo do SharePoint (SQL Server 2014)

O [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] oferece suporte ao SharePoint 2010 e ao SharePoint 2013. O [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2013 é executado fora do farm do SharePoint, embora ele possa ser instalado em servidores do SharePoint. O [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 é executado em servidores de aplicativos em um farm do SharePoint 2010, e usa os recursos e a infraestrutura do SharePoint para dar suporte a operações do servidor. Para instalar o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] para uma versão do SharePoint, use o assistente de instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Após a instalação, siga estas etapas:  
  
- Execute a versão apropriada da ferramenta de configuração do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] para a versão do SharePoint.  
  
- Para o SharePoint 2013, instale a [instalação ou desinstale o suplemento PowerPivot para SharePoint &#40;SharePoint 2013&#41;](https://docs.microsoft.com/analysis-services/instances/install-windows/install-or-uninstall-the-power-pivot-for-sharepoint-add-in-sharepoint-2013).  

##  <a name="sql-server-edition-requirements"></a><a name="bkmk_sqleditions"></a> Requisitos de edição do SQL Server  
 Os recursos de business intelligence não estão disponíveis em todas as edições do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obter detalhes, consulte [recursos com suporte nas edições do SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md) e [edições e componentes do SQL Server 2014](../editions-and-components-of-sql-server-2016.md).  
  
 As notas de versão atuais podem ser encontradas em [notas de versão do Microsoft SQL Server 2014](https://go.microsoft.com/fwlink/?LinkID=296445).  
  

  
##  <a name="sql-server-licensing"></a><a name="bkmk_sqllicense"></a>Licenciamento de SQL Server  
 Para obter mais informações sobre o licenciamento do SQL Server, consulte:  
  
-   [Folha de SQL Server de licenciamento 2014](https://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf) (https://download.microsoft.com/download/6/6/F/66FF3259-1466-4BBA-A505-2E3DA5B2B1FA/SQL_Server_2014_Licensing_Datasheet.pdf).  
  
-   [Como comprar: suporte a modelos de licenciamento do SQL Server](https://www.microsoft.com/licensing/product-licensing/sql-server-2014?activetab=sql-server-2014-pivot%3aprimaryr2) (https://www.microsoft.com/licensing/product-licensing/sql-server-2014?activetab=sql-server-2014-pivot%3aprimaryr2).  
  
##  <a name="analysis-services-installed-on-sharepoint-2013"></a><a name="bkmk_ssas__sharepoint_2013"></a>Analysis Services instalado no SharePoint 2013  
 Se você instalar o servidor do Analysis Services no modo do SharePoint em um servidor sozinho, os requisitos mínimos do sistema serão baseados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] em vez de nos requisitos do SharePoint Server.  
  
 [Requisitos de hardware e software para instalação do SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)  
  
 O [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint é melhor executado em servidores comerciais de nova geração que oferecem limites de RAM mais altos e maior capacidade de processamento. Grandes quantidades de RAM são usadas para armazenar dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] na memória. A RAM dá suporte à capacidade de adaptação a alterações estruturais. Processadores adicionais dão suporte a exames de dados brutos não agregados de longa execução. Os dados supõem sua estrutura em um ambiente dinâmico, em resposta à análise de dados controlada pelo usuário iniciada diretamente de um cliente Excel ou interface front-end.  
  
> [!TIP]  
>  O [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint utiliza caches L2 e L3. Para melhorar o desempenho, é recomendável o uso de processadores com caches L2 e L3 maiores.  
  
 A seguinte tabela descreve as configurações de hardware mínima e recomendada para um servidor autônomo do [!INCLUDE[ssGeminiShortvnext](../../includes/ssgeminishortvnext-md.md)] que não faça parte do farm do SharePoint:  
  
|Componente|Mínimo|Recomendadas|  
|---------------|-------------|-----------------|  
|Processador|Processador de núcleo duplo de 64 bits, 3 gigahertz.|16 núcleos|  
|RAM|8 gigabytes de RAM|64 gigabytes de RAM|  
|Armazenamento|80 gigabytes de armazenamento|80 gigabytes ou mais|  
  
 Se você instalar o servidor do Analysis Services no modo do SharePoint em um servidor do farm do SharePoint, analise os requisitos mínimos do sistema para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e o SharePoint Server nos seguintes links:  
  
-   [Requisitos de hardware e software para instalação do SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [Requisitos de hardware e software para o SharePoint 2013](https://technet.microsoft.com/library/cc262485\(office.15\).aspx).  
  
 As recomendações padrão de hardware e software do SharePoint 2013 são para uma solução de gerenciamento de documentos baseada na Web para um grupo de trabalho ou equipe. Como o processamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] faz uso intenso de dados, a recomendação padrão é suficiente se a carga de trabalho geral é pequena; por exemplo, menos de 100 usuários ou pastas de trabalho. Uma implantação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] maior exige capacidade adicional de computação.  
  
##  <a name="analysis-services-installed-on-a-sharepoint-2010-server"></a><a name="bkmk_ssas__sharepoint_2010"></a>Analysis Services instalado em um servidor do SharePoint 2010  
 O [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] 2010 é executado em servidores de aplicativos em um farm do SharePoint 2010, e usa os recursos e a infraestrutura do SharePoint para dar suporte a operações do servidor. A seguinte tabela resume os requisitos relacionados às implantações do SharePoint 2010:  
  
|Componente|Requisito|  
|---------------|-----------------|  
|Versão do SharePoint|SharePoint 2010 Enterprise, com Serviços do Excel, Serviço de Repositório Seguro e o Claims to Windows Token Service configurados no mesmo farm de servidores.<br /><br /> O SharePoint deve ser instalado utilizando a opção Farm de Servidores na Instalação do SharePoint (a opção de instalação Autônoma do SharePoint não é permitida). O [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] exige que a infraestrutura do farm de servidores ofereça suporte ao acesso administrativo e a dados. A instalação autônoma não fornece estes serviços.<br /><br /> A edição de desenvolvedor, executada no Windows 7 ou no Windows Vista, não tem suporte em instalações de servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].|  
|Service Packs|O SharePoint Server 2010 Service Pack 1 (SP1) é necessário.<br /><br /> O SharePoint 2010 Service Pack 1 é necessário para os recursos do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)][!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)].<br /><br /> A atualização cumulativa de agosto de 2010 do SharePoint 2010, ou posterior, é necessária para atualizar uma versão anterior do [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] com o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. A atualização cumulativa do agosto de 2010, ou posterior, deve ser instalada depois de instalar o SharePoint Service Pack 1. Uma nova instalação do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] não requer a atualização cumulativa. Para obter mais informações, consulte [atualização cumulativa de agosto de 2010 para SharePoint foi lançada](https://blogs.technet.com/b/stefan_gossner/archive/2010/09/02/august-2010-cumulative-update-for-sharepoint-has-been-released.aspx).|  
|Aplicativo Web do SharePoint|O [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint 2010 oferece suporte apenas a aplicativos Web do SharePoint configurados para a autenticação de modo clássico. Se estiver adicionando o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint a um farm existente, verifique se o aplicativo Web que você pretende usar com ele está configurado para a autenticação de modo clássico. Para obter instruções sobre como verificar o modo de autenticação, consulte a seção "verificar se o aplicativo Web usa autenticação de modo clássico" em [implantar soluções PowerPivot no SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint).|  
|Os provedores de dados necessários à atualização de dados do servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]|A atualização de dados do servidor repete as mesmas etapas de recuperação de dados usadas para importar os dados originalmente. Isso significa que os provedores de dados usados para importar os dados em uma estação de trabalho cliente também devem estar presentes no servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint.<br /><br /> Além disso, o uso de feeds de dados em um servidor SharePoint requer que você tenha o ADO.NET Data Services. O programa do Instalador de Pré-requisitos do SharePoint não instala esse software para você. O software a seguir deve ser instalado manualmente.<br /><br /> Os assemblies de runtime do ADO.NET Data Services 3.5 SP1, usados para exportar uma lista do SharePoint como um feed de dados. Baixe e instale a versão que corresponde a seu sistema operacional:<br /><br /> Para o Windows Server 2008 R2, use [a atualização do ADO.NET Data Services para .NET Framework 3,5 SP1 para Windows 7 e Windows Server 2008 R2](https://www.microsoft.com/download/details.aspx?id=2343). O Windows Server 2008 R2 **SP1** já contém o provedor atualizado.<br /><br /> Para o Windows Server 2008, use [a atualização do ADO.NET Data Services para .NET Framework 3,5 SP1 para windows 2000, Windows server 2003, Windows XP, Windows Vista e Windowshttps://go.microsoft.com/fwlink/?LinkId=158125)Server 2008 (](https://www.microsoft.com/download/details.aspx?id=22734).|  
  
 [Determinar os requisitos de hardware e software (SharePoint 2010) (https://go.microsoft.com/fwlink/?LinkId=169734)](https://go.microsoft.com/fwlink/?LinkId=169734)  
  
## <a name="additional-information"></a>Informações adicionais  

