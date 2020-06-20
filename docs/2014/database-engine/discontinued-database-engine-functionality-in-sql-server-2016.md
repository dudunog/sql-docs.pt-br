---
title: Funcionalidade de Mecanismo de Banco de Dados descontinuada no SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- VIA protocol
- unsupported features [SQL Server]
- SQL Mail
- discontinued functionality [SQL Server]
- RESTORE WITH DBO_ONLY
- BACKUP WITH PASSWORD
- user instances enabled
- BACKUP WITH MEDIAPASSWORD
- AWE
- SQL-DMO
- '*= and =*'
- 80 compatibility levels
- COMPUTE BY
- user instance timeout
- sp_dropalias
- COMPUTE
- WITH APPEND
- sys.database_principal_aliases
- sp_dboption
- DATABASEPROPERTY
- FASTFIRSTROW hint
- SET DISABLE_DEF_CNST_CHK
ms.assetid: d686cdf0-d11d-4dba-9ec8-de1a5f189f25
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 14924dedee04345c593683752baff4161c8d270d
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84933147"
---
# <a name="discontinued-database-engine-functionality-in-sql-server-2014"></a>Funcionalidade do Mecanismo de Banco de Dados descontinuada no SQL Server 2014
  Este tópico descreve os recursos do [!INCLUDE[ssDE](../includes/ssde-md.md)] que não estão mais disponíveis no [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
## <a name="discontinued-features-in-sssql14"></a><a name="SQL14"></a>Recursos descontinuados no[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 A tabela a seguir lista os recursos que foram removidos do [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
|Categoria|Recurso descontinuado|Substituição|  
|--------------|--------------------------|-----------------|  
|Nível de Compatibilidade|Nível de compatibilidade 90|Os bancos de dados devem ser definidos com o nível de compatibilidade de pelo menos 100. Quando um banco com um nível de compatibilidade de menos de 100 é atualizado para o [!INCLUDE[ssSQL14](../includes/sssql14-md.md)], o nível de compatibilidade do banco de dados é definido como 100 durante a operação de atualização.|  
  
## <a name="discontinued-features-in-sssql11"></a><a name="Denali"></a>Recursos descontinuados no[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 A tabela a seguir lista os recursos que foram removidos do [!INCLUDE[ssSQL11](../includes/sssql11-md.md)].  
  
|Categoria|Recurso descontinuado|Substituição|  
|--------------|--------------------------|-----------------|  
|Backup e restauração|**Backup {database &#124; log} com senha** e **BACKUP {DATABASE &#124; log} com MEDIAPASSWORD** foram descontinuados. **RESTORE {DATABASE &#124; log} com a senha do [Media]** continua a ser preterido.|Nenhum|  
|Backup e restauração|**RESTAURAR {LOG &#124; DO BANCO DE DADOS}... COM DBO_ONLY**|**RESTAURAR {LOG &#124; DO BANCO DE DADOS}...... COM RESTRICTED_USER**|  
|Nível de Compatibilidade|nível de compatibilidade 80|Os bancos de dados devem ser definidos com o nível de compatibilidade de pelo menos 90.|  
|Opções de configuração|`sp_configure 'user instance timeout'` e `'user instances enabled'`|Use o recurso de banco de dados local. Para obter mais informações, consulte [utilitário SqlLocalDB](../tools/sqllocaldb-utility.md)|  
|Protocolos de conexão|O suporte para o protocolo VIA é descontinuado.|Em vez disso, use TCP.|  
|Objetos de banco de dados|Cláusula `WITH APPEND` em gatilhos|Recrie o gatilho inteiro.|  
|Opções de banco de dados|`sp_dboption`|`ALTER DATABASE`|  
|Email|SQL Mail|Use o Database Mail. Para obter mais informações, consulte [Database Mail](../relational-databases/database-mail/database-mail.md) e [usar Database Mail em vez do SQL Mail](../relational-databases/policy-based-management/use-database-mail-instead-of-sql-mail.md).|  
|Gerenciamento de memória|AWE (Address Windowing Extensions) de 32 bits e suporte de inclusão de memória a quente de 32 bits.|Use um sistema operacional de 64 bits.|  
|Metadados|`DATABASEPROPERTY`|`DATABASEPROPERTYEX`|  
|Programação|SQL-DMO (SQL Server Distributed Management Objects)|SQL Server Management Objects (SMO)|  
|Dicas de consulta|Dica de `FASTFIRSTROW`|`OPTION (FAST`*n* `)` .|  
|Servidores remotos|A capacidade de os usuários criarem novos servidores remotos usando `sp_addserver` foi descontinuada. `sp_addserver` com a opção 'local' permanece disponível. Os servidores remotos preservados durante a atualização ou criados pela replicação podem ser usados.|Substitua servidores remotos usando servidores vinculados.|  
|Segurança|`sp_dropalias`|Substitua aliases por uma combinação de contas de usuário e funções de banco de dados. Use `sp_dropalias` para remover aliases em bancos de dados atualizados.|  
|Segurança|O parâmetro de versão de **PWDCOMPARE** que representa um valor de um logon anterior a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 2000 é descontinuado.|Nenhum|  
|Programação do Service Broker no SMO|A classe **Microsoft. SqlServer. Management. Smo. Broker. BrokerPriority** não implementa mais a interface **Microsoft. SqlServer. Management. Smo. IObjectPermission** .||  
|Opções Set|`SET DISABLE_DEF_CNST_CHK`|Nenhum.|  
|Tabelas do sistema|sys.database_principal_aliases|Use funções em vez de aliases.|  
|Transact-SQL|`RAISERROR` no formato `RAISERROR integer 'string'` foi descontinuado.|Reescreva a instrução usando a sintaxe **RAISERROR (...)** atual.|  
|sintaxe Transact-SQL|`COMPUTE / COMPUTE BY`|Use `ROLLUP`.|  
|sintaxe Transact-SQL|Uso de **\*=** e **=&#42;**|Use a sintaxe de junção ANSI. Para obter mais informações, consulte [from (Transact-SQL).](https://msdn.microsoft.com/library/ms177634\(SQL.105\).aspx)|  
|XEvents|databases_data_file_size_changed, databases_log_file_size_changed<br /><br /> eventdatabases_log_file_used_size_changed<br /><br /> locks_lock_timeouts_greater_than_0<br /><br /> locks_lock_timeouts|Substituído por database_file_size_change event, database_file_size_change<br /><br /> database_file_size_change event<br /><br /> lock_timeout_greater_than_0<br /><br /> lock_timeout|  
  
 **Alterações de XEvent adicionais**  
  
 **resource_monitor_ring_buffer_record**:  
  
-   Campos removidos: single_pages_kb, multiple_pages_kb  
  
-   Campos adicionados: target_kb, pages_kb  
  
 **memory_node_oom_ring_buffer_recorded**:  
  
-   Campos removidos: single_pages_kb, multiple_pages_kb  
  
-   Campos adicionados: target_kb, pages_kb  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do Mecanismo de Banco de Dados preteridos no SQL Server 2014](deprecated-database-engine-features-in-sql-server-2016.md?view=sql-server-2014)  
  
  
