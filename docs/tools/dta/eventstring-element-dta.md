---
title: Elemento EventString (DTA)
description: No utilitário dta, o elemento EventString especifica uma carga de trabalho de script Transact-SQL diretamente no arquivo de entrada XML.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- EventString element
ms.assetid: f76c37b4-2f6e-4274-8ee2-87e89d98e8a2
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 84adfcc937006ed9c1c079977d09e37bbfa5e922
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85785990"
---
# <a name="eventstring-element-dta"></a>Elemento EventString (DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Especifica uma carga de trabalho de script do [!INCLUDE[tsql](../../includes/tsql-md.md)] diretamente no arquivo de entrada XML.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
<Workload>  
    <EventString Weight="...">  
    ...code removed here...  
    </EventString>  
</Workload>  
```  
  
## <a name="element-attributes"></a>Atributos do elemento  
  
|Atributo|Descrição|  
|---------------|-----------------|  
|**Weight**|Opcional. Especifica o fator de peso da consulta (um fator de importância) para o evento especificado. Use um tipo de dados **float** para especificar o peso. Por exemplo, **Peso**= "100,01". O valor mínimo que você pode especificar para **Weight** é "0."|  
  
## <a name="element-characteristics"></a>Características do elemento  
  
|Característica|Descrição|  
|--------------------|-----------------|  
|**Comprimento e tipo de dados**|**string**, tamanho é ilimitado.|  
|**Valor padrão**|Nenhum.|  
|**Ocorrência**|Exigido uma vez se não houver outro tipo de carga de trabalho especificada. É preciso especificar um elemento filho **EventString**, **File**ou **Database** para o pai **Workload** , mas só pode ser usado um tipo. Por exemplo, se for especificada uma carga de trabalho com o elemento **EventString** , não será possível especificar uma carga de trabalho com o elemento **File** no mesmo arquivo de entrada XML.|  
  
## <a name="element-relationships"></a>Relações do elemento  
  
|Relação|Elementos|  
|------------------|--------------|  
|**Elemento pai**|[Elemento Workload &#40;DTA&#41;](../../tools/dta/workload-element-dta.md)|  
|**Elementos filho**|Nenhum.|  
  
## <a name="example"></a>Exemplo  
 Para obter um exemplo de uso deste elemento, consulte [Amostra do arquivo de entrada XML com carga de trabalho embutida &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência do arquivo de entrada XML &#40;Orientador de Otimização do Mecanismo de Banco de Dados&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
