---
title: Elemento de particionamento (DTA)
description: No utilitário dta, o elemento Partitioning contém o esquema de particionamento que você deseja que o Orientador de Otimização do Mecanismo de Banco de Dados use durante a análise.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Partitioning element
ms.assetid: 9bc5d1d5-27a7-4434-966f-c3935794af27
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: b9c07012e71b28caac02cef3f9a4e6bc729c667c
ms.sourcegitcommit: b8933ce09d0e631d1183a84d2c2ad3dfd0602180
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/13/2020
ms.locfileid: "83151834"
---
# <a name="partitioning-element-dta"></a>Elemento de particionamento (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Contém o esquema de particionamento que você gostaria que o Database Engine Tuning Advisor usasse durante a análise.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <Partitioning>...</Partitioning>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|**string**, nenhum tamanho máximo.|  
|**Valores permitidos**|**NONE**<br /> Sem particionamento<br /><br /> **FULL**<br /> Particionamento completo (Aprimora o desempenho.)<br /><br /> **ALIGNED**<br /> Somente o particionamento alinhado (Aprimora a capacidade de gerenciamento máxima).<br /><br /> Use apenas um desses valores com este elemento.<br /><br /> **ALIGNED** significa que na recomendação gerada pelo Database Engine Tuning Advisor cada índice proposto é particionado exatamente do mesmo modo da tabela subjacente para a qual o índice está definido. Índices não clusterizados em uma exibição indexada são alinhados com a exibição indexada.|  
|**Valor padrão**|**NONE**|  
|**Ocorrência**|Necessário uma vez para o elemento **TuningOptions** , a menos que o elemento **DropOnlyMode** seja usado. Se **DropOnlyMode** for usado, você não poderá usar o **Partitioning**. Estes elementos são mutuamente exclusivos.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento TuningOptions &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementos filho**|Nenhum.|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivos de entrada XML simples &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
