---
description: Criar trabalhos
title: Criar trabalhos
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], creating
- SQL Server Agent jobs, creating
ms.assetid: 465fb7fc-7622-4252-a178-ea51691c935b
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: 593bf9b7233aedce7822ededafd5fa94804185e7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97477067"
---
# <a name="create-jobs"></a>Criar trabalhos
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> No momento, na [Instância Gerenciada de SQL do Azure](/azure/sql-database/sql-database-managed-instance), a maioria dos recursos do SQL Server Agent é compatível, mas não todos. Confira detalhes nas [Diferenças entre o T-SQL da Instância Gerenciada de SQL do Azure e o SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Um trabalho é uma série especificada de operações executadas sequencialmente pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Um trabalho pode realizar uma ampla gama de atividades, tais como a execução de scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] , aplicativos de prompt de comando, scripts Microsoft ActiveX, pacotes do Integration Services, comandos e consultas do Analysis Services ou tarefas de replicação. Os trabalhos podem executar tarefas repetitivas ou agendáveis, bem como notificar usuários automaticamente sobre o status do trabalho, desse modo simplificando bastante a administração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Para criar um trabalho, o usuário deve ser membro de uma das funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent ou da função de servidor fixa **sysadmin** . Um trabalho só pode ser editado por seu proprietário ou por membros da função **sysadmin** . Os membros da função **sysadmin** podem atribuir a propriedade do trabalho a outros usuários, bem como executar qualquer trabalho, independentemente de seu proprietário. Para obter mais informações sobre as funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, consulte [Funções de banco de dados fixas do SQL Server Agent](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
Podem ser criados trabalhos para execução na instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou em várias instâncias em toda a empresa. Para executar trabalhos em vários servidores, é necessário configurar pelo menos um servidor mestre e um ou mais servidores de destino. Para obter mais informações sobre servidores mestre e de destino, consulte [Administração automatizada em toda a empresa](../../ssms/agent/automated-administration-across-an-enterprise.md)  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] O Agent registra as informações do trabalho e suas etapas no histórico de trabalhos.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição|Tópico|  
|-|-|  
|Descreve como criar um trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Criar um trabalho](../../ssms/agent/create-a-job.md)|  
|Descreve como reatribuir a propriedade de trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent a outro usuário.|[Give Others Ownership of a Job](../../ssms/agent/give-others-ownership-of-a-job.md)|  
|Descreve como configurar o log de histórico de trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.|[Set Up the Job History Log](../../ssms/agent/set-up-the-job-history-log.md)|  
  
## <a name="see-also"></a>Consulte Também  
[Gerenciar etapas de trabalho](../../ssms/agent/manage-job-steps.md)  
[Administração automatizada em toda a empresa](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[Criar e anexar agendas para trabalhos](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
[Executar Trabalhos](../../ssms/agent/run-jobs.md)  
[Exibir ou modificar trabalhos](../../ssms/agent/view-or-modify-jobs.md)  
