---
title: Propriedades personalizadas do destino DataReader | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f151c3e8-3811-457d-a3d3-6158ca65a646
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9394139b6085fc4f5d59a8202503f6c9e3d750f1
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86916736"
---
# <a name="datareader-destination-custom-properties"></a>Propriedades personalizadas do destino DataReader

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  O destino DataReader tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino DataReader. Todas as propriedades, exceto **DataReader** , são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|DESCRIÇÃO|  
|-------------------|---------------|-----------------|  
|DataReader|String|O nome da classe do destino DataReader.|  
|FailOnTimeout|Boolean|Indica se deve haver falha na ocorrência de **ReadTimeout** . O valor padrão dessa propriedade é **False**.|  
|ReadTimeout|Integer|O número de milissegundos antes de um tempo limite. O valor padrão dessa propriedade é 30000 (30 segundos).|  
  
 A entrada e as colunas de entrada do destino DataReader não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [DataReader Destination](../../integration-services/data-flow/datareader-destination.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
