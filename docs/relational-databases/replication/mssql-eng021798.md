---
title: MSSQL_ENG021798 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021798 error
ms.assetid: 596f5092-75ab-4a19-8582-588687c7b089
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: cecd059fba314e3ee50221b1a7b62d706ad71375
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "76288453"
---
# <a name="mssql_eng021798"></a>MSSQL_ENG021798
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|21798|  
|Origem do Evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico||  
|Texto da mensagem|O trabalho do agente '%s' deve ser adicionado por meio de '%s' antes de continuar. Consulte a documentação de '%s'.|  
  
## <a name="explanation"></a>Explicação  
 Para criar uma publicação, é necessário ser membro da função de servidor fixa **sysadmin** no Publicador ou membro da função de banco de dados fixa **db_owner** no banco de dados de publicação. Se você for membro da função **db_owner** , o erro será gerado se:  
  
-   Você executar scripts do [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. O modelo de segurança foi alterado no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]e esses scripts devem ser atualizados.  
  
-   O procedimento armazenado **sp_addpublication** é executado antes da execução de [sp_addlogreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md). Isso se aplica a todas as publicações transacionais.  
  
-   O procedimento armazenado **sp_addpublication** é executado antes da execução de [sp_addqreader_agent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md). Isso se aplica a publicações transacionais habilitadas para assinaturas de atualização enfileiradas (um valor TRUE para o parâmetro `@allow_queued_tran` de **sp_addpublication**).  
  
 Os procedimentos armazenados **sp_addlogreader_agent** e **sp_addqreader_agent** criam um trabalho de agente e permitem que você especifique a conta do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows em que o agente é executado. Para usuários na função **sysadmin** , os trabalhos de agente são criados implicitamente se **sp_addlogreader_agent** e **sp_addqreader_agent** não forem executados. Os agentes são executados no contexto da conta do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no Distribuidor. Embora **sp_addlogreader_agent** e **sp_addqreader_agent** não sejam solicitados para usuários na função **sysadmin** , é uma prática recomendada de segurança especificar uma conta separada para os agentes. Para obter mais informações, consulte [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md).  
  
## <a name="user-action"></a>Ação do usuário  
 Certifique-se de executar os procedimentos na ordem correta. Para obter mais informações, consulte [Criar uma assinatura](../../relational-databases/replication/publish/create-a-publication.md). Se você tiver scripts de replicação de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], atualize esses scripts para incluir os procedimentos e os parâmetros armazenados exigidos por [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões posteriores. Para obter mais informações, consulte [Atualizar scripts de replicação &#40;programação Transact-SQL de replicação&#41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
