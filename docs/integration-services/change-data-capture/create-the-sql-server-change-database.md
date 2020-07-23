---
title: Criar o banco de dados de alteração do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- oraIns
ms.assetid: 4f79c24a-e99a-4a06-8637-51eeec406259
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a4e5e945b1d6a43829d1e9cb3998335559808480
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918742"
---
# <a name="create-the-sql-server-change-database"></a>Criar o banco de dados de alteração do SQL Server

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Quando você inicia o assistente Nova Instância, a página Criar Banco de Dados CDC é aberta. Use a página Criar Banco de Dados CDC para fornecer informações sobre a nova instância CDC e criar um novo banco de dados de alteração.  
  
 Quando você cria um novo banco de dados CDC, ele está habilitado para SQL Server CDC e esta habilitação exige um logon que é um membro da função de servidor fixa `sysadmin` .  
  
 Quando um usuário que inicia o assistente Criar uma Instância Oracle CDC não é membro da função de servidor fixa `sysadmin` , a caixa de diálogo Conecte-se ao SQL Server abre e pede as credenciais para um membro da função sysadmin para realizar a tarefa de habilitar o banco de dados para SQL Server CDC. Quando o banco de dados CDC é criado, o logon `sysadmin` é descartado e o trabalho é retomado com o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] original usado quando o Oracle Designer Console foi inserido.  
  
> [!IMPORTANT]  
>  Para tarefas diferentes de Habilitar o banco de dados para SQL Server CDC de, o logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usado para executar o Assistente de Nova Instância deverá ter a função de servidor fixa `dbcreator` e permissões UPDATE no banco de dados MSXDBCDC.  
  
 Para obter informações sobre como inserir os dados na caixa de diálogo Conecte-se ao SQL Server, consulte [SQL Server Connection for Instance Creation](../../integration-services/change-data-capture/sql-server-connection-for-instance-creation.md).  
  
## <a name="options"></a>Opções  
 **Instância Oracle CDC**  
 Digite as seguintes informações sobre a instância CDC que você está criando.  
  
-   **Nome**: digite um nome para o novo serviço. Este também será o nome do novo banco de dados de alteração.  
  
-   **Descrição**: digite uma descrição para a nova instância para ajudar a identificá-la. Isso é opcional.  
  
 **Banco de Dados de alteração do SQL Server**  
 Esta seção é usada para criar o banco de dados.  
  
1.  **Banco de Dados de Alteração**: o nome do novo banco de dados de alteração. O nome do banco de dados é o mesmo que o nome que você deu à instância. Este campo somente leitura exibe o caminho completo para o banco de dados.  
  
2.  **Criar Banco de Dados**: clique em **Criar Banco de Dados** para criar o banco de dados.  
  
     Para criar o banco de dados, o logon deve ter a função de servidor `sysasmin` . Consulte a observação de segurança acima para obter mais informações.  
  
     Depois que você criar o banco de dados, clique em **Avançar** para [Connect to an Oracle Source Database](../../integration-services/change-data-capture/connect-to-an-oracle-source-database.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Como criar a instância de banco de dados de alteração do SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [O Serviço Oracle CDC](../../integration-services/change-data-capture/the-oracle-cdc-service.md)  
  
  
