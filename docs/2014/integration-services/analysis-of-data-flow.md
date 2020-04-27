---
title: Análise de fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5654cb30-cad2-470c-97b3-59cb331033e5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e67c5448a6625b37c7fb17bc24ea6bdd7cb879ff
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66061596"
---
# <a name="analysis-of-data-flow"></a>Análise do Fluxo de Dados
  Você pode usar a exibição de banco de dados [Catalog. execution_data_statistics](../relational-databases/statistics/statistics.md) `SSISDB` para analisar o fluxo de dado dos pacotes. Esta exibição exibe uma linha a cada vez que um componente de fluxo de dados envia dados a um componente downstream. As informações podem ser usadas para obter um entendimento mais profundo das linhas que são enviadas para cada componente.  
  
> [!NOTE]  
>  O nível de log deve ser definido para **Detalhado** para capturar as informações com a exibição de catalog.execution_data_statistics.  
  
 O exemplo a seguir exibe o número de linhas enviadas entre componentes de um pacote.  
  
```  
use SSISDB  
select package_name, task_name, source_component_name, destination_component_name, rows_sent  
from catalog.execution_data_statistics  
where execution_id = 132  
order by source_component_name, destination_component_name  
  
```  
  
 O exemplo a seguir calcula o número de linhas por milissegundo enviadas por cada componente para uma execução específica. Os valores calculados são:  
  
-   **total_rows** – a soma de todas as linhas enviadas pelo componente  
  
-   **wall_clock_time_ms** – o tempo de execução decorrido total, em milissegundos, para cada componente  
  
-   **num_rows_per_millisecond** – o número de linhas por milissegundo enviadas por cada componente  
  
 A `HAVING` cláusula é usada para evitar um erro de divisão por zero nos cálculos.  
  
```  
use SSISDB  
select source_component_name, destination_component_name,  
    sum(rows_sent) as total_rows,  
    DATEDIFF(ms,min(created_time),max(created_time)) as wall_clock_time_ms,  
    ((0.0+sum(rows_sent)) / (datediff(ms,min(created_time),max(created_time)))) as [num_rows_per_millisecond]  
from [catalog].[execution_data_statistics]  
where execution_id = 132  
group by source_component_name, destination_component_name  
having (datediff(ms,min(created_time),max(created_time))) > 0  
order by source_component_name desc  
  
```  
  
## <a name="related-tasks"></a>Related Tasks  
 [Depurar o fluxo de dados](troubleshooting/debugging-data-flow.md)  
  
 [Solucionando problemas de ferramentas para execução de pacotes](troubleshooting/troubleshooting-tools-for-package-execution.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Dados em fluxos de dados](data-flow/data-in-data-flows.md)  
  
  
