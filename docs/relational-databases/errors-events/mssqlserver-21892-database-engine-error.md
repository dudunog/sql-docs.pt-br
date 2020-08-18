---
description: MSSQLSERVER_21892
title: MSSQLSERVER_21892 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21892 (Database Engine error)
ms.assetid: 199818e8-28f4-440e-ad85-7bea88f51153
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7027096df3b4a9e6a92ebf6953e3fab51defc984
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88332622"
---
# <a name="mssqlserver_21892"></a>MSSQLSERVER_21892
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|21892|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SQLErrorNum21892|  
|Texto da mensagem|Não é possível consultar sys.availability_replicas no primário do grupo de disponibilidade associado ao nome de rede virtual '%s' quanto aos nomes de servidor das réplicas membro: erro = %d, mensagem de erro = %s.'|  
  
## <a name="explanation"></a>Explicação  
**sp_validate_replica_hosts_as_publishers** consulta o primário atual do grupo de disponibilidade associado ao publicador redirecionado, a fim de determinar as instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospedam as réplicas membro.  Quando essa consulta falha, o erro 21892 é retornado.  
  
Normalmente, **sp_validate_replica_hosts_as_publishers** está no primeiro uso do servidor vinculado temporário; portanto, se houver problemas de conectividade, será provável que eles apareçam primeiro com **sp_validate_replica_hosts_as_publishers**. Ao contrário de **sp_validate_redirected_publisher**, o servidor vinculado usado por **sp_validate_replica_hosts_as_publishers** sempre usa as credenciais do chamador ao se conectar a qualquer um dos hosts de réplica do grupo de disponibilidade.  
  
## <a name="user-action"></a>Ação do usuário  
Ao executar este procedimento armazenado, verifique se a execução está sendo realizada a partir de um logon válido em todas as réplicas. O logon exigirá autorização suficiente para consultar tabelas de metadados de grupo de disponibilidade, bem como para consultar as tabelas de metadados de assinatura na réplica do banco de dados publicador.  
  
Examine o erro referenciado original para determinar a causa da falha e execute a ação corretiva apropriada.  
  
