---
title: Permissões necessárias para conexão do SQL Server para o CDC Designer | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 80334de2-17c1-43c9-951e-21a9f864e9cb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9d0c98add7ebc959f4045eccac3877cbddaeb295
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923859"
---
# <a name="sql-server-connection-required-permissions-for-the-cdc-designer"></a>Permissões necessárias para conexão do SQL Server para o Designer CDC

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  O CDC Designer Console exige informações de conexão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executar suas tarefas. Este tópico descreve as informações que podem ser fornecidas na caixa de diálogo **Conecte-se ao SQL Server** para definir a conexão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 A caixa de diálogo **Conecte-se ao SQL Server** abre quando necessário, como quando as informações de conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não estão disponíveis ou quando as informações existem, mas a conexão não tem as permissões necessárias.  
  
 A tabela a seguir descreve as várias tarefas em que uma conexão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é necessária e as permissões necessárias de logon/usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Tarefa|Permissões mínimas|  
|----------|-------------------------|  
|Exibir a lista de Serviços e Instâncias CDC usando a instância associada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|`db_datareader` em MSXDBCDC|  
|Iniciar/parar instâncias CDC|`db_datareader` e `db_datawriter` no MSXDBCDC|  
|Exibir o status da Instância CDC.|`db_owner` no banco de dados da Instância CDC|  
|Criar um novo banco de dados da Instância Oracle CDC.|`dbcreator` função de servidor fixa|  
|Criar uma nova instância Oracle CDC.|`db_datareader` em MSXDBCDC<br /><br /> `db_owner` no banco de dados CDC que foi criado.|  
|Obter scripts de implantação.|`db_datareader` e `db_datawriter` no MSXDBCDC<br /><br /> `db_owner` no banco de dados CDC relacionado|  
|Alterar configuração e adicionar/remover instâncias de captura.|`db_datareader` e `db_datawriter` no MSXDBCDC<br /><br /> `db_owner` no banco de dados CDC relacionado|  
  
## <a name="see-also"></a>Consulte Também  
 [Acessar o CDC Designer Console](../../integration-services/change-data-capture/access-the-cdc-designer-console.md)   
 [Conexão do SQL Server para a criação de instância](../../integration-services/change-data-capture/sql-server-connection-for-instance-creation.md)  
  
  
