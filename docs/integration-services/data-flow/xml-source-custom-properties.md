---
description: Propriedades personalizadas da origem XML
title: Propriedades personalizadas da origem XML | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: eb29b28c-3159-41ec-b3d7-fce5b2f2be55
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8aa4a0c94f0728162230c5a282cbac7410643a4b
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194536"
---
# <a name="xml-source-custom-properties"></a>Propriedades personalizadas da origem XML

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  A origem XML contém propriedades personalizadas e as propriedades comuns a todos os componentes de fluxo de dados.  
  
 A tabela a seguir descreve as propriedades personalizadas da origem XML. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Descrição|  
|-------------------|---------------|-----------------|  
|AccessMode|Integer|O modo usado para acessar os dados XML.|  
|UseInlineSchema|Boolean|Um valor que indica se deve ser usada uma definição de esquema embutido dentro da origem XML. O valor padrão dessa propriedade é **False**.|  
|XMLData|String|O arquivo ou variáveis dos quais é possível recuperar os dados XML.<br /><br /> O valor dessa propriedade pode ser especificado com uma expressão de propriedades.|  
|XMLSchemaDefinition|String|O caminho e nome de arquivo do arquivo de definição de esquema (.xsd).<br /><br /> O valor dessa propriedade pode ser especificado com uma expressão de propriedades.|  
  
 A tabela a seguir descreve as propriedades personalizadas da saída da origem XML. Todas as propriedades são de leitura/gravação.  
  
|Nome da propriedade|Tipo de Dados|Descrição|  
|-------------------|---------------|-----------------|  
|RowsetID|String|Um valor que identifica o conjunto de linhas associado à saída.|  
  
 As colunas de saída da origem XML não têm nenhuma propriedade personalizada.  
  
 Para obter mais informações, consulte [XML Source](../../integration-services/data-flow/xml-source.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Propriedades comuns](./set-the-properties-of-a-data-flow-component.md)  
  
