---
title: Elemento OnlineIndexOperation (DTA)
description: No utilitário dta, o elemento OnlineIndexOperation especifica se os itens que o Orientador de Otimização do Mecanismo de Banco de Dados recomenda podem ser criados online.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- OnlineIndexOperation element
ms.assetid: 7c5614cd-09aa-4a59-9591-347aa7d36473
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: b9299786ce9c71c393c1c0b270b345092296d7ac
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775000"
---
# <a name="onlineindexoperation-element-dta"></a>Elemento OnlineIndexOperation (DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Especifica se os índices, as exibições indexadas ou as partições que o Database Engine Tuning Advisor recomenda podem ser criados online.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <OnlineIndexOperation>...</OnlineIndexOperation>  
```  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|**string**, nenhum tamanho máximo.|  
|**Valores permitidos**|**OFF**<br /> Nenhuma estrutura de design físico recomendada pode ser criada online.<br /><br /> **ON**<br /> Todas as estruturas de design físico recomendadas podem ser criadas online.<br /><br /> **MIXED**<br /> O Orientador de Otimização do Mecanismo de Banco de Dados tenta recomendar estruturas de design físico que podem ser criadas online quando possível.<br /><br /> Use um desses valores com esse elemento. Se os índices são criados online, a palavra-chave **ONLINE = ON** será acrescentada à definição de seus objetos.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Opcional. Se usado, só pode ser utilizado uma vez para o elemento **TuningOptions** .|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento TuningOptions &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementos filho**|Nenhum.|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso desse elemento, veja [Exemplo de arquivos de entrada XML simples &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
