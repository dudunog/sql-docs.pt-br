---
title: Elemento de banco de dados para servidor (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
author: stevestein
ms.author: sstein
ms.openlocfilehash: 87df538858c9294cb8986da3df0d2b3814411326
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85057757"
---
# <a name="database-element-for-server-dta"></a>Elemento de banco de dados para servidor (DTA)
  Especifica o banco de dados que deseja ajustar em um servidor específico.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|Comprimento e tipo de dados|Nenhum.|  
|Valor padrão|Nenhum.|  
|Ocorrência|Exigido uma ou mais vezes por elemento `Server`.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|Elemento pai|[Elemento Server &#40;DTA&#41;](server-element-dta.md)|  
|Elementos filho|[Elemento Name para Database &#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [Elemento Schema para Database &#40;DTA&#41;](schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>Comentários  
 Esse elemento tem o nome **DatabaseDetailsTypecomplexType** no Esquema XML do Orientador de Otimização do Mecanismo de Banco de Dados. Não confunda este elemento do `Database` com aquele cujo pai raiz é o elemento `Configuration`. Para obter mais informações, veja [Elemento Database para configuração &#40;DTA&#41;](database-element-for-configuration-dta.md).  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso do `Database` elemento, consulte [elemento de servidor &#40;DTA&#41;](server-element-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
