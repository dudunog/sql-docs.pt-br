---
description: Conexão para o SQL Server para exclusão
title: Conexão ao SQL Server para exclusão | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 030b10c2-6b88-4c2c-bf67-22994be25a60
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1688ed8c1e95edabfea6b022b605a18a0e99d690
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88496293"
---
# <a name="connection-to-sql-server-for-delete"></a>Conexão para o SQL Server para exclusão

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Quando um logon sem uma função de banco de dados que inclui permissão de gravação (por exemplo a função **db_owner** ) ao banco de dados MSXDBCDC tenta excluir uma instância Oracle CDC, a caixa de diálogo Conectar-se ao SQL Server é exibida.  
  
 Nesta caixa de diálogo, você deve inserir as credenciais de um logon que tem permissão de gravação ao banco de dados MSXDBCDC, como a função de banco de dados **db_owner** para excluir a instância Oracle CDC.  
  
 Insira as seguintes informações na caixa de diálogo Conecte-se ao SQL Server.  
  
 **Nome do servidor**  
 Digite o nome do servidor em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está localizado.  
  
 **Autenticação**  
 Selecione uma das seguintes:  
  
-   **Autenticação do Windows**  
  
-   **Autenticação do SQL Server**: se você selecionar esta opção, deverá digitar o **Logon** e **Senha** para o usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao qual você está se conectando.  
  
 **Opções**  
 Clique na seta para exibir opções disponíveis a serem configuradas. Você pode escolher deixar estas opções com o valor padrão. As opções disponíveis são:  
  
-   **Tempo Limite de Conexão**: digite o tempo (em segundos) que o programa aguarda até que uma conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja estabelecida antes de gerar um erro de tempo limite. O valor padrão é **15**.  
  
-   **Tempo Limite de Execução**: digite o tempo (em segundos) que o programa aguarda até que uma execução de comando do SQL seja concluída antes de gerar um erro de tempo limite. O valor padrão é **30**.  
  
-   **Criptografar Conexão**: selecione **Criptografar Conexão** para verificar se a conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo estabelecida está criptografada para garantir a privacidade.  
  
-   **Avançado**: clique em **Avançado** e digite as propriedades de conexão adicionais na caixa de diálogo Propriedades Avançadas da Conexão, se necessário.  
  
## <a name="see-also"></a>Consulte Também  
 [Permissões necessárias para conexão do SQL Server para o Serviço CDC](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
  
