---
title: Conexão ao SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5bb582f9-68d3-4c1e-ab02-6fc16807f1a5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e87e29349cdef9db94e917f6fe543b327c5abf9f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71298860"
---
# <a name="connection-to-sql-server"></a>Conexão com o SQL Server

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Quando um logon sem uma função de banco de dados que inclui permissão de gravação (por exemplo a função **db_owner** ) ao banco de dados MSXDBCDC tenta criar uma instância Oracle CDC, a caixa de diálogo Conecte-se ao SQL Server é exibida.  
  
 Nesta caixa de diálogo, você deve inserir as credenciais para um logon que tem permissão de gravação ao banco de dados MSXDBCDC, como a função de banco de dados **db_owner** para criar a nova instância Oracle CDC.  
  
 Insira as seguintes informações na caixa de diálogo Conecte-se ao SQL Server.  
  
### <a name="server-name"></a>Nome do servidor  
 Digite o nome do servidor em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está localizado.  
  
### <a name="authentication"></a>Autenticação  
 Selecione uma das seguintes:  
  
-   Autenticação do Windows  
  
-   **Autenticação do SQL Server**: se você selecionar esta opção, deverá digitar o **Logon** e **Senha** para o usuário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao qual você está se conectando.  
  
### <a name="options"></a>Opções  
 Clique na seta para exibir opções disponíveis a serem configuradas. Você pode escolher deixar estas opções com o valor padrão. As opções disponíveis são:  
  
-   **Tempo Limite de Conexão**: digite o tempo (em segundos) que o programa aguarda até que uma conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seja estabelecida antes de gerar um erro de tempo limite. O valor padrão é **15**.  
  
-   **Tempo Limite de Execução**: digite o tempo (em segundos) que o programa aguarda até que uma execução de comando do SQL seja concluída antes de gerar um erro de tempo limite. O valor padrão é **30**.  
  
-   **Criptografar Conexão**: selecione **Criptografar Conexão** para verificar se a conexão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está sendo estabelecida está criptografada para garantir a privacidade.  
  
-   **Avançado**: clique em **Avançado** e digite as propriedades de conexão adicionais na caixa de diálogo Propriedades Avançadas da Conexão, se necessário.  
  
## <a name="see-also"></a>Consulte Também  
 [Permissões necessárias para conexão do SQL Server para o Serviço CDC](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
  
