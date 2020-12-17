---
description: Exibir ou modificar trabalhos
title: Exibir ou modificar trabalhos
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], modifying
- jobs [SQL Server Agent], viewing
- modifying jobs
- viewing jobs
- SQL Server Agent jobs, viewing
- SQL Server Agent jobs, modifying
- displaying jobs
ms.assetid: 57f649b8-190c-4304-abd7-7ca5297deab7
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 7c16b835eff545c4623ccf9845a523f2e56bf865
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97422452"
---
# <a name="view-or-modify-jobs"></a>Exibir ou modificar trabalhos
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada de SQL do Azure](/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira detalhes nas [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Você pode exibir qualquer trabalho criado. Após executar um trabalho, você também pode exibir seu histórico. Exibir o histórico de um trabalho permite-lhe observar quando o trabalho foi executado, o status do trabalho como um todo e o status de cada etapa do trabalho. É possível saber se o trabalho já falhou no passado, quando foi concluído com êxito pela última vez e que saída o trabalho criou a cada execução. Os membros da função de servidor fixa **sysadmin** podem exibir ou modificar qualquer trabalho, independentemente do proprietário.  
  
> [!NOTE]  
> Um trabalho deve ter sido executado pelo menos uma vez para haver um histórico de trabalhos. Você pode limitar o tamanho total do log de histórico do trabalho, bem com o tamanho por trabalho.  
  
Além disso, você também pode modificar um trabalho para atender a novos requisitos. É possível modificar:  
  
-   Opções de resposta  
  
-   Agendas  
  
-   Etapas de trabalho  
  
-   Propriedade  
  
-   Categoria do trabalho  
  
-   Servidores de destino (somente em trabalhos multisservidor)  
  
Para assegurar que as alterações em trabalhos multisservidor entrem em vigor, é necessário postá-las na lista de downloads para que os servidores de destino possam baixar o trabalho atualizado. Para garantir que os servidores de destino disponham das definições de trabalho mais atuais, poste uma instrução INSERT após atualizar o trabalho multisservidor, da seguinte maneira:  
  
```  
EXECUTE sp_post_msx_operation 'INSERT', 'JOB', '<job id>'  
```  
  
Para obter mais informações, consulte [sp_purge_jobhistory (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-purge-jobhistory-transact-sql.md).  
  
Os membros da função de servidor fixa **sysadmin** podem exibir a definição ou o histórico de qualquer trabalho, bem como modificá-los.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição|Tópico|  
|-|-|  
|Descreve como exibir trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[View a Job](../../ssms/agent/view-a-job.md)|  
|Descreve como exibir o log de histórico de trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[View the Job History](../../ssms/agent/view-the-job-history.md)|  
|Descreve como excluir o conteúdo do log de histórico de trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Clear the Job History Log](../../ssms/agent/clear-the-job-history-log.md)|  
|Descreve como definir limites de tamanho para logs de históricos de trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Resize the Job History Log](../../ssms/agent/resize-the-job-history-log.md)|  
|Descreve como alterar as propriedades de trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Modify a Job](../../ssms/agent/modify-a-job.md)|  
  
## <a name="see-also"></a>Consulte Também  
[sysjobhistory](../../relational-databases/system-tables/dbo-sysjobhistory-transact-sql.md)  
