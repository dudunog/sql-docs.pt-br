---
title: 'Assistente do grupo de disponibilidade: Página de Validação'
description: Este tópico descreve as opções encontradas na página Validação do assistente de grupo de disponibilidade Always On.
ms.custom: seo-lt-2019
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.addreplicawizard.validation.f1
- sql13.swb.adddatabasewizard.validation.f1
- sql13.swb.newagwizard.validation.f1
helpviewer_keywords:
- ', listeners'
ms.assetid: c8971556-240c-491a-bc86-9cc72f71a3dd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f22ac0e249e693b7bcd102f6d9242c601e14331f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74821842"
---
# <a name="validation-page-always-on-availability-group-wizards"></a>Página Validação (Assistentes do Grupo de Disponibilidade AlwaysOn)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
  Este tópico da ajuda descreve as opções da página **Validação** . Este tópico aplica-se ao [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)], ao [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)]e ao [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Use esta página para validar se o ambiente dá suporte a todas as opções de configuração feitas nas páginas anteriores do assistente.  
  
##  <a name="validation-page-options"></a><a name="PageOptions"></a> Opções da página Validação  
 **Resultados da validação de grupo de disponibilidade.**  
 Esta grade exibe os resultados de cada etapa de validação concluída. As colunas da grade são as seguintes:  
  
 **Nome**  
 Exibe uma frase que descreve uma etapa específica.  
  
 **Resultado**  
 Exibe um dos seguintes textos de hiperlink. Para obter mais informações sobre o resultado de determinada etapa de validação, clique no hiperlink.  
  
|Result|Descrição|  
|------------|-----------------|  
|**Erro**|Indica se houve falha na etapa de validação. Clique no link para exibir a mensagem de erro.|  
|**Ignorado**|Indica que a etapa de validação foi ignorada porque não é necessária por suas seleções. Clique no link para exibir o motivo pelo qual uma etapa foi ignorada.|  
|**Êxito**|Indica que a etapa de validação foi concluída com êxito|  
|**Aviso**|Indica um problema potencial com a configuração do grupo de disponibilidade.  Clique no link para exibir a mensagem de aviso.|  
  
 **Executar Novamente a Validação**  
 Clique para repetir as etapas da validação se você fizer uma alteração fora do assistente em resposta a um erro de validação.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Usar a caixa de diálogo Novo Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-new-availability-group-dialog-box-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Réplica ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usar o Assistente para Adicionar Banco de Dados ao Grupo de Disponibilidade &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/availability-group-add-database-to-group-wizard.md)  
  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral dos grupos de disponibilidade AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
