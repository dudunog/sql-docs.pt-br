---
title: Permissões necessárias para conexão do SQL Server para o Serviço CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: d9e968f9-180c-4fa0-a849-98f2b1942330
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2332ccdc6e14734c6caed1e09b4dfa70b79e035d
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86910822"
---
# <a name="sql-server-connection-required-permissions-for-the-cdc-service"></a>Permissões necessárias para conexão do SQL Server para o Serviço CDC

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  O Console de Configuração do Serviço CDC exige informações de conexão para que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] execute suas tarefas. Este tópico descreve as informações que podem ser fornecidas na caixa de diálogo Conecte-se ao SQL Server para definir a conexão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A caixa de diálogo Conecte-se ao SQL Server abre quando necessário, como quando as informações de conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estão disponíveis ou quando as informações existem, mas a conexão não tem as permissões necessárias.  
  
 A tabela a seguir descreve as várias tarefas em que uma conexão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é necessária e as permissões necessárias de logon/usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Tarefa|Permissões mínimas|  
|----------|-------------------------|  
|Preparar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|`dbcreator` função de servidor fixa|  
|Crie um logon Oracle CDC Service-SQL Server para ser usado pelo serviço Oracle CDC.|`public` função de servidor fixa|  
|Crie um logon do Serviço Oracle CDC para usar para registrar o novo serviço no MSXDBCDC.|`db_datareader` e `db_datawriter` no MSXDBCDC|  
|Editar um logon do Serviço Oracle CDC para atualizar o registro do serviço no MSXDBCDC.|`db_datareader` e `db_datawriter` no MSXDBCDC|  
|Excluir um logon do Serviço Oracle CDC para atualizar o registro do serviço no MSXDBCDC.|`db_datareader` e `db_datawriter` no MSXDBCDC|  
  
## <a name="see-also"></a>Consulte Também  
 [Conexão com o SQL Server](../../integration-services/change-data-capture/connection-to-sql-server.md)   
 [Conexão com o SQL Server para exclusão](../../integration-services/change-data-capture/connection-to-sql-server-for-delete.md)  
  
  
