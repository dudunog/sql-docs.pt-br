---
title: Propriedades personalizadas do destino de processamento de dimensões | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9700f663-53f2-49b6-b1ef-92c7b752d6a1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2f46acb401bf04e9b0445c452e26d69de42a2d94
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71292824"
---
# <a name="dimension-processing-destination-custom-properies"></a>Propriedades personalizadas do destino de processamento de dimensões

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  O destino Processamento de Dimensões tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino Processamento de Dimensões. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de Dados|DESCRIÇÃO|  
|--------------|---------------|-----------------|  
|ASConnectionString|String|A cadeia de caracteres de conexão com uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou com um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|KeyDuplicate|Inteiro (enumeração)|Quando UseDefaultConfiguration é **False**, um valor que indica como tratar erros de chave duplicada. Os valores possíveis são **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). O valor padrão dessa propriedade é **IgnoreError** (0).|  
|KeyErrorAction|Inteiro (enumeração)|Quando UseDefaultConfiguration for **False**, um valor que indica como tratar erros de chave. Os valores possíveis são **ConvertToUnknown** (0) e **DiscardRecord** (1). O valor padrão dessa propriedade é **ConvertToUnknown** (0).|  
|KeyErrorLimit|Integer|Quando UseDefaultConfiguration for **False**, o limite superior de erros de chave permitido.|  
|KeyErrorLimitAction|Inteiro (enumeração)|Quando UseDefaultConfiguration é **False**, um valor que indica a ação a ser realizada quando **KeyErrorLimit** for atingido. Os valores possíveis são **StopLogging** (1) e **StopProcessing** (0). O valor padrão dessa propriedade é **StopProcessing** (0).|  
|KeyErrorLogFile|String|Quando UseDefaultConfiguration é **False**, o caminho e o nome do arquivo de log de erro.|  
|KeyNotFound|Inteiro (enumeração)|Quando for UseDefaultConfiguration é **False**, um valor que indica como tratar erros de chave ausentes. Os valores possíveis são **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). O valor padrão dessa propriedade é **IgnoreError** (0).|  
|NullKeyConvertedToUnknown|Inteiro (enumeração)|Quando UseDefaultConfiguration é **False**, um valor que indica como tratar chaves nulas convertidas para o valor desconhecido. Os valores possíveis são **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). O valor padrão dessa propriedade é **IgnoreError** (0).|  
|NullKeyNotAllowed|Inteiro (enumeração)|Quando UseDefaultConfiguration é **False**, um valor que indica como tratar nulos não permitidos. Os valores possíveis são **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). O valor padrão dessa propriedade é **IgnoreError** (0).|  
|ProcessType|Inteiro (enumeração)|O tipo de processamento de dimensões usado pela transformação. Os valores são **ProcessAdd** (1) (incremental), **ProcessFull** (0) e **ProcessUpdate** (2).|  
|UseDefaultConfiguration|Boolean|Um valor que especifica se a transformação usa a configuração de erro padrão. Se essa propriedade for **False**, a transformação incluirá informações sobre processamento de erros.|  
  
 A entrada e as colunas de entrada do destino Processamento de Dimensões não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Destino de processamento de dimensões](../../integration-services/data-flow/dimension-processing-destination.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades comuns](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
  
