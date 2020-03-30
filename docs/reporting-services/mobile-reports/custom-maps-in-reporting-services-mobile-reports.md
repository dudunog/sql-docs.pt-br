---
title: Mapas personalizados em relatórios móveis do Reporting Services | Microsoft Docs
description: Saiba mais sobre os mapas geográficos no Publicador de Relatórios Móveis do SQL Server, definidos em um formato conhecido como shapefiles ESRI.
ms.date: 12/06/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.custom: seodec18
ms.topic: conceptual
ms.assetid: 59a4ebad-587a-4770-afcd-c69216b8afd9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 17975defea6029e4077acbe45fd3f8b0d7495267
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "62759647"
---
# <a name="custom-maps-in-reporting-services-mobile-reports"></a>Mapas personalizados nos relatórios móveis do Reporting Services
Os mapas geográficos no Publicador de Relatórios Móveis do SQL Server são definidos em um formato conhecido como *ESRI shapefiles*.  
  
Criado inicialmente por uma empresa privada, esse é agora um formato semiaberto amplamente usado em grande parte dos aplicativos GIS. De acordo com esse formato, o Publicador de Relatórios Móveis exige que dois arquivos sejam fornecidos ao definir um mapa:  
  
- Um arquivo .SHP para geometrias de forma  
- Um arquivo .DBF para metadados  
  
Os nomes dos arquivos de base devem corresponder (por exemplo, *canada.shp* e *canada.dbf*). Os metadados devem incluir o campo *NAME* com o valor do nome da forma correspondente (chave) a ser usado ao preencher o mapa com os dados.  

Os dois arquivos de mapa juntos, o SHP e DBF, não podem ter mais de 512 KB. Se os arquivos de mapa forem muito grandes, use uma ferramenta como [https://mapshaper.org/](https://mapshaper.org/) para reduzir seu tamanho.  
  
Consulte como [Adicionar mapas personalizados a relatórios móveis](../../reporting-services/mobile-reports/add-a-custom-map-to-a-reporting-services-mobile-report.md).  
  
## <a name="technical-information"></a>Informações técnicas  
  
- A especificação oficial: [https://www.esri.com/library/whitepapers/pdfs/shapefile.pdf](https://www.esri.com/library/whitepapers/pdfs/shapefile.pdf)  
- O arquivo shapefile da Wikipedia: [https://en.wikipedia.org/wiki/Shapefile](https://en.wikipedia.org/wiki/Shapefile)  
  
## <a name="creating--editing-map-geometry"></a>Criando e editando geometria de mapa  
  
Criar e editar shapefiles é um processo complexo que está além do escopo deste documento. Aqui estão alguns recursos e aplicativos para ajudá-lo a começar:  
  
- ArcGIS: [https://www.arcgis.com/](https://www.arcgis.com/)  
- Plug-in MAPublisher para Adobe Illustrator: [https://www.avenza.com/mapublisher](https://www.avenza.com/mapublisher)  
- QuantumGIS (gratuito): [https://www.qgis.org/](https://www.qgis.org/)  

## <a name="existing-shapefiles"></a>Shapefiles existentes  
  
Muitos shapefiles existentes podem ser baixados da Web, de sites como Diva-GIS: [https://www.diva-gis.org/Data](https://www.diva-gis.org/Data).  

## <a name="see-also"></a>Confira também  
- [Mapas nos relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)  
- [Criar e publicar relatórios móveis com o Publicador de Relatórios Móveis do SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)   
  
  
  
