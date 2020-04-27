---
title: Propriedades personalizadas do destino de processamento de dimensões | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9700f663-53f2-49b6-b1ef-92c7b752d6a1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b63e508f87b9766507c541a7ed81e42466bbd1e8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62827372"
---
# <a name="dimension-processing-destination-custom-properies"></a>Propriedades personalizadas do destino de processamento de dimensões
  O destino Processamento de Dimensões tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino Processamento de Dimensões. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de Dados|DESCRIÇÃO|  
|--------------|---------------|-----------------|  
|ASConnectionString|String|A cadeia de caracteres de conexão com uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou com um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|KeyDuplicate|Inteiro (enumeração)|Quando UseDefaultConfiguration é `False`, um valor que indica como tratar erros de chave duplicada. Os valores possíveis são `IgnoreError` (0), `ReportAndContinue` (1) e `ReportAndStop` (2). O valor padrão dessa propriedade é `IgnoreError` (0).|  
|KeyErrorAction|Inteiro (enumeração)|Quando UseDefaultConfiguration é `False`, um valor que indica como tratar o erro de chave. Os valores possíveis são `ConvertToUnknown` (0) e `DiscardRecord` (1). O valor padrão dessa propriedade é `ConvertToUnknown` (0).|  
|KeyErrorLimit|Integer|Quando UseDefaultConfiguration é `False`, o limite superior de erros de chave que estão habilitados.|  
|KeyErrorLimitAction|Inteiro (enumeração)|Quando UseDefaultConfiguration é `False`, um valor que indica a ação a ser tomada `KeyErrorLimit` quando é atingido. Os valores possíveis são `StopLogging` (1) e `StopProcessing` (0). O valor padrão dessa propriedade é `StopProcessing` (0).|  
|KeyErrorLogFile|String|Quando UseDefaultConfiguration é `False`, o caminho e o nome de arquivo do arquivo de log de erros.|  
|KeyNotFound|Inteiro (enumeração)|Quando UseDefaultConfiguration é `False`, um valor que indica como tratar erros de chave ausentes. Os valores possíveis são `IgnoreError` (0), `ReportAndContinue` (1) e `ReportAndStop` (2). O valor padrão dessa propriedade é `IgnoreError` (0).|  
|NullKeyConvertedToUnknown|Inteiro (enumeração)|Quando UseDefaultConfiguration é `False`, um valor que indica como lidar com chaves nulas convertidas para o valor desconhecido. Os valores possíveis são `IgnoreError` (0), `ReportAndContinue` (1) e `ReportAndStop` (2). O valor padrão dessa propriedade é `IgnoreError` (0).|  
|NullKeyNotAllowed|Inteiro (enumeração)|Quando UseDefaultConfiguration é `False`, um valor que indica como tratar nulos não permitidos. Os valores possíveis são `IgnoreError` (0), `ReportAndContinue` (1) e `ReportAndStop` (2). O valor padrão dessa propriedade é `IgnoreError` (0).|  
|ProcessType|Inteiro (enumeração)|O tipo de processamento de dimensões usado pela transformação. Os valores são `ProcessAdd` (1) (incremental), `ProcessFull` (0) e `ProcessUpdate` (2).|  
|UseDefaultConfiguration|Boolean|Um valor que especifica se a transformação usa a configuração de erro padrão. Se essa propriedade for `False`, a transformação incluirá informações sobre processamento de erros.|  
  
 A entrada e as colunas de entrada do destino Processamento de Dimensões não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Destino de processamento de dimensões](dimension-processing-destination.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades comuns](../common-properties.md)  
  
  
