---
title: Propriedades personalizadas de arquivo simples | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7f2caeab-784c-4b0c-9b3e-6a88d1ccdbf9
author: janinezhang
ms.author: janinez
ms.openlocfilehash: f83cf140b370783d21ee2254e7361a2ae3467424
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84915536"
---
# <a name="flat-file-custom-properties"></a>Propriedades personalizadas de arquivo simples
  **Propriedades personalizadas de fontes**  
  
 A fonte de Arquivo Simples tem as propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da fonte de Arquivo Simples. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|DESCRIÇÃO|  
|-------------------|---------------|-----------------|  
|FileNameColumnName|String|O nome de uma coluna de saída que contém o nome de arquivo. Se nenhum nome for especificado, nenhuma coluna de saída que contém o nome de arquivo será gerada.<br /><br /> Observação: essa propriedade não está disponível no **Editor de Fonte de Arquivo Simples**, mas pode ser definida por meio do **Editor Avançado**.|  
|RetainNulls|Boolean|Um valor que especifica se os valores Nulos do arquivo de origem devem ser retidos como valores Nulos quando os dados forem processados pelo mecanismo Pipeline de Transformação de Dados. O valor padrão dessa propriedade é `False`.|  
  
 A saída da fonte de Arquivo Simples não tem nenhuma propriedade personalizada.  
  
 A tabela a seguir descreve as propriedades personalizadas das colunas de saída da fonte de Arquivo Simples. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|DESCRIÇÃO|  
|-------------------|---------------|-----------------|  
|FastParse|Boolean|Um valor que indica se as colunas usam as rotinas de análise mais rápidas, mas que não fazem distinção entre localidades, fornecido pelo DTS, ou as rotinas de análise padrão que fazem distinção entre localidades. Para obter mais informações, consulte [Fast Parse](../fast-parse.md) e [Standard Parse](../standard-parse.md). O valor padrão dessa propriedade é `False`.<br /><br /> Observação: essa propriedade não está disponível no **Editor de Fonte de Arquivo Simples**, mas pode ser definida por meio do **Editor Avançado**.|  
  
 Para obter mais informações, consulte [Flat File Source](flat-file-source.md).  
  
 **Propriedades personalizadas de destino**  
  
 O destino Arquivo Simples tem propriedades personalizadas e propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas do destino Arquivo Simples. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|DESCRIÇÃO|  
|-------------------|---------------|-----------------|  
|Cabeçalho|String|Um bloco de texto inserido no arquivo antes que qualquer dado seja gravado.<br /><br /> O valor dessa propriedade pode ser especificado com uma expressão de propriedades.|  
|Overwrite|Boolean|Um valor que especifica se será substituído ou adicionado a um arquivo de destino existente de mesmo nome. O valor padrão dessa propriedade é `True`.|  
  
 A entrada e as colunas de entrada do destino Arquivo Simples não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [Flat File Destination](flat-file-destination.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades comuns](../common-properties.md)  
  
  
