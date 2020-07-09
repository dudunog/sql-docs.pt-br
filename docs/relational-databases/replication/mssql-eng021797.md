---
title: MSSQL_ENG021797 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021797 error
ms.assetid: 54d83a1e-43fd-449c-a2b2-fdda2609a534
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 3dc052e9b950cfb10cf9265132e880dc91a39e8e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85721600"
---
# <a name="mssql_eng021797"></a>MSSQL_ENG021797
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|21797|  
|Origem do Evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|'%s' deve ser um logon válido do Windows na forma: 'MACHINE\Login' ou 'DOMAIN\Login'. Consulte a documentação de '%s'.|  
  
## <a name="explanation"></a>Explicação  
 Esse erro será gerado pelos procedimentos armazenados de replicação a seguir se o valor especificado para o parâmetro `@job_login` for nulo ou inválido. Esse erro poderá ocorrer se um membro da função de banco de dados fixa **db_owner** executar scripts de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O modelo de segurança foi alterado no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]e esses scripts devem ser atualizados.  
  
-   [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
-   [sp_addqreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)  
  
-   [sp_addpublication_snapshot &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)  
  
-   [sp_addpushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)  
  
-   [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)  
  
-   [sp_addmergepushsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)  
  
-   [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)  
  
 Esses procedimentos armazenados podem ser executados por um membro da função de servidor fixa **sysadmin** no servidor apropriado ou por um membro da função de banco de dados fixa **db_owner** no banco de dados apropriado. Os procedimentos armazenados criam um trabalho de agente e permitem que o usuário especifique a conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows em que o agente é executado. Para usuários na função **sysadmin** , os trabalhos de agente são criados implicitamente, ainda que uma conta do Windows não seja especificada (se uma conta for especificada, deve ser válida); agentes são executados no contexto da conta do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no servidor apropriado. Apesar da conta não ser exigida, é uma prática recomendada de segurança especificar uma conta separada para os agentes. Para obter mais informações, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## <a name="user-action"></a>Ação do usuário  
 Certifique-se de ter especificado uma conta válida do Windows para o parâmetro `@job_login` de cada procedimento. Se tiver scripts de replicação de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], atualize esses scripts para incluir os procedimento e os parâmetros armazenados exigidos pelo [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Para obter mais informações, consulte [Atualizar scripts de replicação &#40;programação Transact-SQL de replicação&#41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
