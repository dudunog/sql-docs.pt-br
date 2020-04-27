---
title: Atualizar transformações de pesquisa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Lookup transformation and upgrading
- upgrading caching for Lookup transformation
- upgrading Lookup transformation
ms.assetid: d9b2c281-91ee-4e20-bdf0-0cd77d4a4241
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: eae7433569972c217161f1681b2f7089c7604335
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66091506"
---
# <a name="upgrade-lookup-transformations"></a>Atualizar transformação Pesquisa
  Ao atualizar do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , considere a possibilidade de modificar pacotes para aproveitar os novos recursos da Transformação Pesquisa. A transformação dá suporte a tipos de cache e opções de saída de dados disponíveis no [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]. Para obter mais informações sobre saídas de dados e cache adicionais, consulte [Lookup Transformation](../../integration-services/data-flow/transformations/lookup-transformation.md).  
  
 No [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)], os tipos de cache disponíveis são cache cheio, cache parcial e nenhum cache. No [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)], você pode configurar uma transformação Pesquisa para usar um desses tipos de cache. Para obter mais informações sobre como implementar o cache parcial ou nenhum cache, consulte [implementar uma pesquisa no modo sem cache ou cache parcial](../../integration-services/data-flow/transformations/implement-a-lookup-in-no-cache-or-partial-cache-mode.md). Para obter informações sobre como implementar o cache completo, consulte [implementar uma transformação Lookup em modo de cache cheio usando o Gerenciador de conexões de cache](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-cache-connection-manager.md) e [implementar uma transformação pesquisa em modo de cache cheio usando o gerenciador de conexões OLE DB](../../integration-services/connection-manager/lookup-transformation-full-cache-mode-ole-db-connection-manager.md).  
  
 No [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)], a transformação Pesquisa teve uma entrada, uma saída e uma saída de erro. As linhas nas entradas que possuem entradas correspondentes no conjunto de dados de referência são manipuladas pela saída. Linhas na entrada que não possuem entradas correspondentes são tratadas como erros e podem ser redirecionadas para a saída de erro. No [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)], a transformação Pesquisa tem duas saídas: uma saída de correspondência e outra sem-correspondência.  
  
 Por padrão, quando você executa uma transformação Pesquisa que foi criada no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], o [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] trata as linhas sem entradas correspondentes como erros e permite que você redirecione as linhas a uma saída de erro. Você tem a opção de configurar a transformação Pesquisa para tratar as linhas como não erro e redirecioná-las para a saída sem-correspondência.  
  
 Para obter mais informações, consulte [Editor de transformação pesquisa &#40;&#41;de página Geral ](../../integration-services/general-page-of-integration-services-designers-options.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Transformação pesquisa](../../integration-services/data-flow/transformations/lookup-transformation.md)  
  
  
