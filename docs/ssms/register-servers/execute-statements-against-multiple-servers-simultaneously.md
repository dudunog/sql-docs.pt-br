---
description: Executar instruções em vários servidores simultaneamente
title: Executar instruções em vários servidores simultaneamente
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- multiserver queries
- executing queries against multiple servers
- queries [SQL Server], multiserver
ms.assetid: 197760f3-0a06-43de-8162-69c27d3fbe56
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 07/18/2016
ms.openlocfilehash: 627eff46acaae38b675814e84ea76e7a7ea64f2d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417952"
---
# <a name="execute-statements-against-multiple-servers-simultaneously"></a>Executar instruções em vários servidores simultaneamente

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Este tópico descreve como consultar vários servidores ao mesmo tempo no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], criando um grupo de servidores locais ou um Servidor de Gerenciamento Central e um ou mais grupos de servidor, e um ou mais servidores registrados dentro dos grupos e, em seguida, consultar o grupo completo. 

Os resultados retornados pela consulta podem ser combinados em um único painel de resultados ou em painéis de resultados separados. O conjunto de resultados pode incluir colunas adicionais para o nome do servidor e o logon usado pela consulta em cada servidor. Os servidores de gerenciamento centrais e os servidores registrados subordinados podem ser registrados somente com o uso da Autenticação do Windows. Os servidores em grupos de servidores locais podem ser registrados usando Autenticação do Windows ou a Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> **OBSERVAÇÃO:** Antes de executar os procedimentos a seguir, crie um Servidor de Gerenciamento Central e grupos de servidores. Para obter mais informações, consulte [Criar um servidor de gerenciamento central e um grupo de servidores &#40;SQL Server Management Studio&#41;](../../tools/sql-server-management-studio/create-a-central-management-server-and-server-group.md).  

  
##  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Como as conexões mantidas por um Servidor de Gerenciamento Central são executadas no contexto do usuário com o uso da Autenticação do Windows, as permissões efetivas nos servidores registrados podem variar. Por exemplo, o usuário pode ser membro da função de servidor fixa sysadmin na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] A, mas pode ter permissões limitadas na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] B.  
  
 ## <a name="execute-statements-against-multiple-configuration-targets-simultaneously"></a>Executar instruções em vários destinos de configuração simultaneamente  

1.  No SQL Server Management Studio, no menu **Exibir** , clique em **Servidores Registrados**.  
  
2.  Expanda um Servidor de Gerenciamento Central, clique com o botão direito do mouse em um grupo de servidores, aponte para **Conectar**e, em seguida, clique em **Nova Consulta**.  
  
3.  No Editor de Consultas, digite e execute uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] , como a seguinte:  
  
    ```  
    USE master  
    GO  
    SELECT * FROM sysdatabases;  
    GO  
    ```  
  
     Por padrão, o painel de resultados combinará os resultados da consulta de todos os servidores no grupo de servidor.  
  
#### <a name="to-change-the-multiserver-results-options"></a>Para alterar as opções de resultados de vários servidores  
  
1.  No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], no menu **Ferramentas** , clique em **Opções**.  
  
2.  Expanda **Resultados da Consulta**, expanda **SQL Server**e então clique em **Resultados de Multisservidor**.  
  
3.  Na página **Resultados de Multisservidor** , especifique as configurações de opção que você quer e então clique em **OK**.  
  
## <a name="see-also"></a>Consulte Também  
 [Administrar vários servidores usando os Servidores de Gerenciamento Centrais](../../relational-databases/administer-multiple-servers-using-central-management-servers.md)  
  
  
