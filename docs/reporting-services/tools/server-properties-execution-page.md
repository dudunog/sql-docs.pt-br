---
title: Propriedades do Servidor (página Execução) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.serverproperties.execution.f1
ms.assetid: 53b77db1-b013-4dac-82dd-30c0de276639
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e8259591c54068cde134c98ae405dd77fac6fab4
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "65571363"
---
# <a name="server-properties-execution-page"></a>Propriedades do Servidor (página Execução)
  Use essa página para definir um valor de intervalo para execução do relatório. Esse valor se aplica a todos os relatórios processados pela instância de servidor do relatório atual. Você pode anular esse valor para relatórios individuais. O valor especificado deve acomodar todos os processamentos de relatório que ocorrem no servidor de relatório, mais processamento da consulta executado no servidor do banco de dados quando o servidor de relatório recupera dados usados no relatório.  
  
 Para abrir essa página, inicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se a uma instância de servidor de relatórios, clique com o botão direito do mouse no nome do servidor de relatórios e selecione **Propriedades**. Clique em **Execução** para abrir essa página.  
  
## <a name="options"></a>Opções  
 **Não exceder o tempo limite de execução do relatório**  
 Permita a um servidor de relatório tempo ilimitado para concluir o processamento do relatório.  
  
 **Limitar a execução do relatório ao seguinte número de segundos**  
 Defina uma restrição de tempo na execução do relatório. O período de tempo inicia quando o relatório é solicitado. Se o período de tempo terminar antes que o relatório seja totalmente processado, o servidor de relatório cancelará o processo e quaisquer consultas em andamento às fontes de dados externas.  
  
## <a name="see-also"></a>Consulte Também  
 [Definir propriedades do servidor de relatório &#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md)   
 [Conectar-se a um servidor de relatório no Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Definir as propriedades do processamento de relatórios](../../reporting-services/report-server/set-report-processing-properties.md)   
 [Definindo valores de tempo limite para processamento de relatórios e conjuntos de dados compartilhados &#40;SSRS&#41;](../../reporting-services/report-server/setting-time-out-values-for-report-and-shared-dataset-processing-ssrs.md)   
 [Servidor de Relatório na ajuda F1 do Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)  
  
  
