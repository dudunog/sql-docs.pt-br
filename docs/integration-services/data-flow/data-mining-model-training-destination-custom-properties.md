---
description: Propriedades personalizadas do destino Treinamento do Modelo de Mineração de Dados
title: Propriedades personalizadas do destino do treinamento do modelo de mineração de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: f0a70216-fdac-44ae-af29-35f65626217c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8ed5f1b09cbbaa4d20c891a03d9846949eedc8bc
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196432"
---
# <a name="data-mining-model-training-destination-custom-properties"></a>Propriedades personalizadas do destino Treinamento do Modelo de Mineração de Dados

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  O destino Treinamento do Modelo de Mineração de Dados tem propriedades personalizadas e as propriedades comum a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino Treinamento do Modelo de Mineração de Dados. Todas as propriedades são de leitura/gravação.  
  
|Propriedade|Tipo de Dados|Descrição|  
|--------------|---------------|-----------------|  
|ASConnectionId|String|O identificador exclusivo do gerenciador de conexões.|  
|ASConnectionString|String|A cadeia de caracteres de conexão com uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou com um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|ObjectRef|String|Uma marca XML que identifica a estrutura de mineração de dados usada pela transformação.|  
  
 A entrada e as colunas de entrada do destino Treinamento do Modelo de Mineração de Dados não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Destino de treinamento do modelo de Data Mining](../../integration-services/data-flow/data-mining-model-training-destination.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades comuns](./set-the-properties-of-a-data-flow-component.md)  
  
