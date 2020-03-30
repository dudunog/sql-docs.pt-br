---
title: Nova agenda de trabalho – Propriedades da agenda de trabalho
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.scheduleproperties.f1
- sql13.swb.maint.editrecurringjobsched.f1
ms.assetid: 5c0b1bc9-dd87-49cc-b0dd-75d0d922b177
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ace04d16e537e50c10e0eaa5c4fa432d1db7055f
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75245214"
---
# <a name="new-job-schedule---job-schedule-properties"></a>Nova agenda de trabalho – Propriedades da agenda de trabalho
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada do Banco de Dados SQL do Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Consulte [Azure SQL Database Managed Instance T-SQL differences from SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) (Diferenças entre o T-SQL da Instância Gerenciada do Banco de Dados SQL do Azure e o SQL Server) para obter detalhes.

Use essa página para exibir e alterar as propriedades da agenda.  
  
## <a name="options"></a>Opções  
**Nome**  
Digite um nome novo para a agenda.  
  
**Trabalhos na agenda**  
Exiba os trabalhos que usam a agenda.  
  
**Tipo de agenda**  
Selecione o tipo de agenda.  
  
**Enabled**  
Marque para habilitar ou desabilitar a agenda.  
  
## <a name="recurring-schedule-types-options"></a>Opções de tipos de agenda recorrentes  
**Ocorre**  
Selecione o intervalo no qual a agenda ocorre periodicamente.  
  
**Repete-se a cada**  
Selecione o número de dias ou semanas entre ocorrências periódicas da agenda. Essa opção não está disponível para agendas que ocorrem mensalmente.  
  
**Segunda-feira**  
Defina o trabalho para ocorrer em uma segunda-feira. Disponível somente para agendamentos semanais recorrentes.  
  
**Terça-feira**  
Defina o trabalho para ocorrer em uma terça-feira. Disponível somente para agendamentos semanais recorrentes.  
  
**Quarta-feira**  
Defina o trabalho para ocorrer em uma quarta-feira. Disponível somente para agendamentos semanais recorrentes.  
  
**Quinta-feira**  
Defina o trabalho para ocorrer em uma quinta-feira. Disponível somente para agendamentos semanais recorrentes.  
  
**Sexta-feira**  
Defina o trabalho para ocorrer em uma sexta-feira. Disponível somente para agendamentos semanais recorrentes.  
  
**Sábado**  
Defina o trabalho para ocorrer em um sábado. Disponível somente para agendamentos semanais recorrentes.  
  
**Domingo**  
Defina o trabalho para ocorrer em um domingo. Disponível somente para agendamentos semanais recorrentes.  
  
**Day**  
Selecione o dia do mês que a agenda ocorre. Disponível somente para agendas mensais recorrentes.  
  
**de cada**  
Selecione o número de meses entre ocorrências da agenda. Disponível somente para agendas mensais recorrentes.  
  
**O**  
Especifique uma agenda durante um dia específico da semana em uma semana específica durante o mês. Disponível somente para agendas mensais recorrentes.  
  
**Ocorre uma vez em**  
Defina a hora para que um trabalho ocorra diariamente.  
  
**Ocorre a cada**  
Defina o número de horas, minutos ou segundos entre ocorrências.  
  
**Data de início**  
Defina a data quando essa agenda ficará efetiva.  
  
**Data de término**  
Defina a data quando a agenda já não será válida.  
  
**Nenhuma data de término**  
Especifique que a agenda permanecerá efetiva indefinidamente.  
  
## <a name="one-time-schedule-types-options"></a>Opções de tipos de agendas que ocorrem apenas uma vez  
**Data**  
Selecione a data para que o trabalho seja executado.  
  
**Hora**  
Selecione a hora para que o trabalho seja executado.  
  
## <a name="see-also"></a>Consulte Também  
[Criar e anexar agendas para trabalhos](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
[Agendar um trabalho](../../ssms/agent/schedule-a-job.md)  
  
