---
title: Exibir ou configurar opções de conexão de servidor remoto (SQL Server) | Microsoft Docs
description: Saiba como exibir ou configurar as opções de conexão de servidor remoto no nível de servidor. É possível usar o SQL Server Management Studio ou o Transact-SQL para essa finalidade.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- remote servers [SQL Server], connection options
- servers [SQL Server], remote
- connections [SQL Server], remote servers
ms.assetid: 356d3e6b-8514-4bd2-a683-9de147949b2b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ec50e6ae39798add5a564dbeb8a971e879c18c27
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85680717"
---
# <a name="view-or-configure-remote-server-connection-options-sql-server"></a>Exibir ou configurar opções de conexão de servidor remoto (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico descreve como exibir ou configurar as opções de conexão de servidor remoto no nível de servidor no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para exibir ou configurar opções de conexão de servidor remoto usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Acompanhamento:**  [depois de configurar opções de conexão de servidor remoto](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 A execução de **sp_serveroption** requer a permissão ALTER ANY LINKED SERVER no servidor.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-view-or-configure-remote-server-connection-options"></a>Para exibir ou configurar opções de conexão de servidor remoto  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse em um servidor e clique em **Propriedades**.  
  
2.  Na caixa de diálogo **Propriedades do SQL Server – \<**_server_name_**>** , clique em **Conexões**.  
  
3.  Na página **Conexões** , verifique as configurações de **Conexões de servidor remoto** e as modifique, se necessário.  
  
4.  Repita os etapas 1 até 3, no outro servidor do par de servidor remoto.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-view-remote-server-connection-options"></a>Para exibir as opções de conexão de servidor remoto  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo usa [sp_helpserver](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md) para retornar informações sobre todos os servidores remotos.  
  
```sql  
USE master;  
GO  
EXEC sp_helpserver ;  
```  
  
#### <a name="to-configure-remote-server-connection-options"></a>Para configurar opções de conexão de servidor remoto  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_serveroption](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md) para configurar um servidor remoto. O exemplo configura um servidor remoto correspondente a outra instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `SEATTLE3`, para que seja compatível com ordenação com a instância local do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```sql  
USE master;  
EXEC sp_serveroption 'SEATTLE3', 'collation compatible', 'true';  
```  
  
##  <a name="follow-up-after-you-configure-remote-server-connection-options"></a><a name="FollowUp"></a> Acompanhamento: depois de configurar opções de conexão de servidor remoto  
 O servidor remoto deve ser interrompido e reiniciado para que a configuração entre em vigor.  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [Servidores remotos](../../database-engine/configure-windows/remote-servers.md)   
 [Servidores vinculados &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_helpserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)  
  
  
