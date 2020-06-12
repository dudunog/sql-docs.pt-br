---
title: Processar dados (SSAS tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d88f2dc9-2933-4be5-9bf3-48ffbc2d0a1a
author: minewiskan
ms.author: owend
ms.openlocfilehash: e2066cb6d871f43dda719cab3539253db97bfca7
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84540058"
---
# <a name="process-data-ssas-tabular"></a>Processar dados (SSAS tabular)
  Ao importar dados para um modelo de tabela, no modo Cache, você está capturando um instantâneo desses dados no momento da importação. Em alguns casos, esses dados podem nunca serem alterados e não precisam ser atualizados no modelo. Porém, é mais provável que os dados de que você está importando sejam alterados regularmente. Para que seu modelo reflita os dados mais recentes das fontes de dados, é necessário processar (atualizar) os dados e recalcular os dados calculados. Para atualizar os dados em seu modelo, você executa uma ação de processo em todas as tabelas, em uma tabela individual, por uma partição, ou por uma conexão da fonte de dados.  
  
 Ao criar seu projeto de modelo, inicie as ações de processamento manualmente no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Após a implantação de um modelo, as operações de processamento podem ser executadas usando o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ou programadas usando um script. As tarefas descritas aqui todas pertencem a ações de processo que você pode fazer durante a criação do modelo no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para obter mais informações sobre ações de processo para um modelo implantado, consulte [Process Database, Table, or Partition](tabular-models/process-database-table-or-partition-analysis-services.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Processando os dados manualmente &#40;SSAS Tabular&#41;](manually-process-data-ssas-tabular.md)|Descreve como processar manualmente dados de workspace modelo.|  
|[Solucionar problemas de dados de processo &#40;SSAS tabular&#41;](troubleshoot-process-data-ssas-tabular.md)|Descreve como solucionar problemas de operações de processo.|  
  
  
