---
title: Fontes de dados com suporte (SSAS multidimensional) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Analysis Services, data sources
- data sources [Analysis Services], about data sources
- Analysis Services, data sources
- connections [Analysis Services]
- SSAS, data sources
ms.assetid: c97e0f8d-7ddd-4941-8b51-e7832f30fbbe
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5a8cdeb912d1ead21571f1ec7f86e15b0d009514
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66072856"
---
# <a name="data-sources-supported-ssas-multidimensional"></a>Fontes de dados com suporte (SSAS multidimensional)
  Este tópico descreve os tipos de fonte de dados que você pode usar em um modelo multidimensional.  
  
##  <a name="supported-data-sources"></a><a name="bkmk_supported_ds"></a>Fontes de dados com suporte  
 Você pode recuperar dados das fontes de dados na tabela a seguir: Quando você instalar o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], a instalação não instala os provedores listados para cada fonte de dados. Alguns deles podem já estar instalados com outros aplicativos no computador; em outros casos, você precisará baixar e instalar o provedor.  
  
> [!NOTE]  
>  Também é possível usar provedores de outros fabricantes, como Oracle OLE DB Provider, na conexão com banco de dados de terceiros, com suporte fornecido por esses fabricantes.  
  
|||||  
|-|-|-|-|  
|Fonte|Versões|Tipo de arquivo|Provedores <sup>1</sup>|  
|Bancos de dados do Access|Microsoft Access 2007, 2010, 2013.|.accdb ou .mdb|Provedor OLE DB do Microsoft Jet 4.0|  
|SQL Server bancos de dados relacionais <sup>5</sup>|Microsoft SQL Server 2005, 2008, 2008 R2, 2012, 2014 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] <sup>2</sup>, SQL Server Parallel Data Warehouse (PDW) <sup>3</sup>|(não se aplica)|Provedor OLE DB para SQL Server<br /><br /> Provedor OLE DB do SQL Server Native Client<br /><br /> Provedor OLE DB do SQL Server Native 11.0 Client<br /><br /> Provedor de dados .NET Framework para SQL Client|  
|Bancos de dados relacionais da Oracle|Oracle 9i, 10g, 11g.|(não se aplica)|Provedor OLE DB Oracle<br /><br /> Provedor de Dados .NET Framework para Cliente Oracle<br /><br /> Provedor de dados do .NET Framework para SQL Server<br /><br /> Provedor de OLE DB MSDAORA <sup>4</sup><br /><br /> OraOLEDB<br /><br /> MSDASQL|  
|Bancos de dados relacionais do Teradata|Teradata V2R6, V12|(não se aplica)|Provedor OLE DB TDOLEDB<br /><br /> Provedor de .NET Data para Teradata|  
|Bancos de dados relacionais do Informix|V11.10|(não se aplica)|Provedor OLE DB para Informix|  
|Bancos de dados relacionais IBM DB2|8.1|(não se aplica)|DB2OLEDB|  
|Bancos de dados relacionais do Sybase Adaptive Server Enterprise (ASE)|15.0.2|(não se aplica)|Provedor OLE DB para Sybase|  
|Outros bancos de dados relacionais|(não se aplica)|(não se aplica)|Um provedor de OLE DB|  
  
 <sup>1</sup> fontes de dados ODBC não têm suporte para soluções multidimensionais. Embora o próprio Analysis Services trate a conexão, os designers no [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] usado para criar soluções não podem se conectar a uma fonte de dados ODBC, mesmo ao usar driver do MSDASQL. Se seus requisitos comerciais incluírem uma fonte de dados ODBC, crie uma solução tabelar em vez disso.  
  
 <sup>2</sup> para obter mais informações, [!INCLUDE[ssSDS](../../includes/sssds-md.md)]consulte, em [Azure.Microsoft.com](https://go.microsoft.com/fwlink/?LinkID=157856).  
  
 <sup>3</sup> para obter mais informações [!INCLUDE[ssSDS](../../includes/sssds-md.md)] sobre o PDW, consulte [SQL Server Data Warehouse paralelos](https://go.microsoft.com/fwlink/?LinkId=150895).  
  
 <sup>4</sup> em alguns casos, usar o provedor de OLE DB MSDAORA pode resultar em erros de conexão, especialmente com versões mais recentes do Oracle. Se você encontrar algum erro, será recomendável usar um dos outros provedores listados para Oracle.  
  
 <sup>5</sup> alguns recursos exigem um SQL Server banco de dados relacional que é executado localmente. Mais especificamente, os armazenamentos ROLAP e de write-back requerem que a fonte de dados subjacente seja um banco de dados relacional do SQL Server.  
  
## <a name="see-also"></a>Consulte Também  
 [Fontes de dados com suporte &#40;SSAS de tabela&#41;](../tabular-models/data-sources-supported-ssas-tabular.md)   
 [Fontes de dados em modelos multidimensionais](data-sources-in-multidimensional-models.md)   
 [Exibições de fontes de dados em modelos multidimensionais](data-source-views-in-multidimensional-models.md)  
  
  
