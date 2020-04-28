---
title: O que&#39;s New no Analysis Services e Business Intelligence | Microsoft Docs
ms.custom: ''
ms.date: 06/07/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: aa69c299-b8f4-4969-86d8-b3292fe13f08
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1458dcf473ffbf7fc9bab13c2c688a4e01954c56
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175525"
---
# <a name="what39s-new-in-sql-server-2014-analysis-services"></a>O que&#39;s New no SQL Server 2014 Analysis Services
  Com exceção à funcionalidade adicionada com suporte a relatórios de Power View em modelos multidimensionais, [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] o não é alterado da versão anterior.

 Para obter informações sobre [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] outros produtos e tecnologias diferentes nesta versão, consulte What ' [s New in SQL Server 2014](../sql-server/what-s-new-in-sql-server-2016.md).

## <a name="updates-to-design-tool-installation"></a>Atualizações da instalação da Ferramenta de Design
 O [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] para Business Intelligence (SSDT-BI), anteriormente conhecido como Business Intelligence Development Studio (BIDS), é usado para criar modelos do Analysis Services, relatórios do Reporting Services e pacotes do Integration Services. Você pode baixar o SSDT-BI nos locais a seguir:

-   [Download do SSDT-BI para Visual Studio 2013](https://go.microsoft.com/fwlink/p/?LinkId=396526)

-   [Download do SSDT-BI para Visual Studio 2012](https://go.microsoft.com/fwlink/p/?LinkID=273673)

 Se você tiver uma versão anterior do SSDT-BI ou BIDS instalado no computador, a versão mais recente será instalada lado a lado da versão anterior. É comum executar versões mais recentes e anteriores das ferramentas de design em uma única estação de trabalho para que você possa modificar projetos e soluções associados às versões específicas do servidor.

> [!NOTE]
>  Existem vários sites de download para as versões do Visual Studio 2012 e do Visual Studio 2013 do SSDT. A maioria deles não incluem os modelos de projeto de BI. O uso dos links acima oferecerão a você a versão correta. Você saberá que tem a versão correta do SSDT-BI se vir a pasta Business Intelligence Project templates. Essa pasta contém modelos de projeto para o Analysis Services, o Reporting Services e o Integration Services. Dependendo de como você tiver instalado o SSDT-BI, provavelmente também verá um modelo de projeto adicional para bancos de dados do SQL Server.

 ![Novos modelos de projeto no SSDT](media/ssdt-biprojects.png "Novos modelos de projeto no SSDT")

## <a name="features-recently-added-power-view-for-multidimensional-models"></a>Recursos adicionados recentemente: Power View para Modelos Multidimensionais
 A capacidade de criar relatórios do Power View em modelos multidimensionais foi introduzida pela primeira vez na Atualização Cumulativa 4 do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 1. Agora, a funcionalidade Power View para Modelos Multidimensionais faz parte do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].

 **Relatório do Power View para um Modelo Multidimensional**

 ![Relatório do Power View](media/powerviewreport-wn.gif "Relatório do Power View")

 Essa funcionalidade ajuda as organizações a maximizarem investimentos existentes em BI, permitindo que modelos multidimensionais (também conhecidos como cubos OLAP) sejam usados como as ferramentas de relatório de cliente mais recentes. Dependendo dos tipos de dados no modelo multidimensional, os usuários poderão criar com facilidade uma variedade de visualizações dinâmicas de tabelas e matrizes a gráficos de bolhas e mapas geográficos. Os modelos multidimensionais também dão suporte a consultas usando DAX (Data Analysis Expressions).

 O Power View para Modelos Multidimensionais exige a funcionalidade interna de relatório do Power View no [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (no modo do SharePoint). Outras versões do Power View, especificamente o Suplemento Power View no Excel 2013, não dão suporte a modelos multidimensionais.

 Para saber mais, consulte [Power View para Modelos Multidimensionais](https://msdn.microsoft.com/library/dn140246.aspx).


