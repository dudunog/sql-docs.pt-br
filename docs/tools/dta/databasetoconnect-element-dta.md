---
title: Elemento DatabaseToConnect (DTA)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DatabaseToConnect element
ms.assetid: 65153a66-3aee-4429-99b7-0816ac23c285
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 5ea514d4f401eeebc822e8d6bbaafcf09282da34
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75306902"
---
# <a name="databasetoconnect-element-dta"></a>Elemento DatabaseToConnect (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Especifica o primeiro banco de dados que o Orientador de Otimização do Mecanismo de Banco de Dados conecta ao ajustar uma carga de trabalho.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
    <TuningOptions>  
...code removed here...  
      <DatabaseToConnect>...</DatabaseToConnect>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|DESCRIÇÃO|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|**string**, comprimento ilimitado.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Opcional. Pode ser usado uma vez para cada elemento **TuningOptions** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento TuningOptions &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementos filho**|Nenhum|  
  
## <a name="remarks"></a>Comentários  
 Use o **DatabaseToConnect** para especificar o nome do primeiro banco de dados que o Orientador de Otimização do Mecanismo de Banco de Dados conectará quando iniciar a sessão de ajuste. Você pode especificar apenas um banco de dados com esse elemento. Se forem especificados vários nomes de banco de dados, o Orientador de Otimização do Mecanismo de Banco de Dados retornará um erro.  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso, veja a [Amostra do arquivo de entrada XML com carga de trabalho embutida &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
