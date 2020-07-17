---
title: Ações e grupos de ações de auditoria do SQL Server | Microsoft Docs
description: Saiba mais sobre os grupos de ações no nível do servidor, do banco de dados e da auditoria, bem como sobre as ações individuais na auditoria do SQL Server.
ms.custom: ''
ms.date: 07/13/2020
ms.prod: sql
ms.prod_service: security
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
f1_keywords:
- audit
helpviewer_keywords:
- audit actions [SQL Server]
- audits [SQL Server], groups
- server-level audit actions [SQL Server]
- SQL Server Audit
- audit-level audit actions [SQL Server]
- database-level audit actions [SQL Server]
- audit action groups [SQL Server]
- audits [SQL Server], actions
ms.assetid: b7422911-7524-4bcd-9ab9-e460d5897b3d
author: DavidTrigano
ms.author: datrigan
ms.openlocfilehash: 68943b7b57794d779656ca8537a7c59d4f486db8
ms.sourcegitcommit: e08d28530e0ee93c78a4eaaee8800fd687babfcc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86301884"
---
# <a name="sql-server-audit-action-groups-and-actions"></a>Ações e grupos de ações de auditoria do SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  O recurso [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit permite auditar grupos de eventos e eventos individuais no nível do servidor e do banco de dados. Para obter mais informações, veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](../../../relational-databases/security/auditing/sql-server-audit-database-engine.md).  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consistem em zero ou mais itens de ação de auditoria. Esses itens de ação de auditoria podem ser um grupo de ações, como Server_Object_Change_Group ou ações individuais, como operações SELECT em uma tabela.  
  
> [!NOTE]  
>  Server_Object_Change_Group inclui CREATE, ALTER e DROP para qualquer objeto de servidor (Banco de Dados ou Ponto de Extremidade).  
  
 As auditorias podem ter as seguintes categorias de ações:  
  
-   Nível do servidor. Essas ações incluem operações de servidor, como alterações de gerenciamento e operações de logon e logoff.  
  
-   Nível do banco de dados. Essas ações abrangem operações DML (linguagem de manipulação de dados) e DDL (linguagem de definição de dados).  
  
-   Nível da auditoria. Essas ações incluem ações no processo de auditoria.  
  
 Algumas ações realizadas nos componentes de auditoria do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] são auditadas intrinsecamente em uma auditoria específica e, nesses casos, os eventos de auditoria ocorrem automaticamente porque o evento ocorreu no objeto pai.  
  
 As seguintes ações são auditadas intrinsecamente:  
  
-   Alteração de estado da auditoria do servidor (estado de configuração em ON ou OFF)  
  
 Os seguintes eventos são auditados intrinsecamente:  
  
-   CREATE SERVER AUDIT SPECIFICATION  
  
-   ALTER SERVER AUDIT SPECIFICATION  
  
-   DROP SERVER AUDIT SPECIFICATION  
  
-   CREATE DATABASE AUDIT SPECIFICATION  
  
-   ALTER DATABASE AUDIT SPECIFICATION  
  
-   DROP DATABASE AUDIT SPECIFICATION  
  
 Todas as auditorias são desabilitadas quando criadas inicialmente.  
  
## <a name="server-level-audit-action-groups"></a>Grupos de ação de auditoria no nível do servidor  
 Grupos de ação de auditoria no nível do servidor são ações semelhantes às classes de evento security audit do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obter mais informações, confira [Referência de classe de evento do SQL Server](../../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
 A tabela a seguir descreve os grupos de ações de auditoria no nível do servidor e fornece a Classe de Evento SQL Server equivalente onde aplicável.  
  
|Nome do grupo de ações|Descrição|  
|-----------------------|-----------------|  
|APPLICATION_ROLE_CHANGE_PASSWORD_GROUP|Esse evento é gerado sempre que uma senha é alterada por uma função de aplicativo. Equivalente a [Audit App Role Change Password Event Class](../../../relational-databases/event-classes/audit-app-role-change-password-event-class.md).|  
|AUDIT_CHANGE_GROUP|Esse evento é gerado sempre que uma auditoria é criada, modificada ou excluída. Esse evento é gerado sempre que qualquer especificação de auditoria é criada, modificada ou excluída. Qualquer alteração em uma auditoria é auditada nessa auditoria. Equivalente a [Audit Change Audit Event Class](../../../relational-databases/event-classes/audit-change-audit-event-class.md).|  
|BACKUP_RESTORE_GROUP|Esse evento é gerado sempre que um comando de backup ou restauração é emitido. Equivalente à [classe de evento Audit Backup and Restore](../../../relational-databases/event-classes/audit-backup-and-restore-event-class.md).|  
|BATCH_COMPLETED_GROUP|Esse evento é gerado sempre que qualquer operação de lote de texto, procedimento armazenado ou de gerenciamento de transações conclui a execução. Ele é gerado depois que o lote é concluído e audita o lote inteiro ou o texto do procedimento armazenado, conforme enviado do cliente, incluindo o resultado. **Adicionado no SQL Server 2019.**|  
|BATCH_STARTED_GROUP|Esse evento é gerado sempre que qualquer operação de lote de texto, procedimento armazenado ou gerenciamento de transações começa a ser executada. Ele é gerado antes da execução e audita o lote inteiro ou o texto do procedimento armazenado, conforme enviado do cliente. **Adicionado no SQL Server 2019.**|  
|BROKER_LOGIN_GROUP|Esse evento é gerado para relatar mensagens de auditoria relacionadas à segurança de transporte do Service Broker. Equivalente a [Audit Broker Login Event Class](../../../relational-databases/event-classes/audit-broker-login-event-class.md).|  
|DATABASE_CHANGE_GROUP|Esse evento é gerado quando um banco de dados é criado, alterado ou descartado. Esse evento é gerado sempre que um banco de dados é criado, alterado ou descartado. Equivalente a [Audit Database Management Event Class](../../../relational-databases/event-classes/audit-database-management-event-class.md).|  
|DATABASE_LOGOUT_GROUP|Esse evento é gerado quando um usuário de banco de dados independente faz logoff de um banco de dados.|  
|DATABASE_MIRRORING_LOGIN_GROUP|Esse evento é gerado para relatar mensagens de auditoria relacionadas à segurança de transporte de espelhamento de banco de dados. Equivalente a [Audit Database Mirroring Login Event Class](../../../relational-databases/event-classes/audit-database-mirroring-login-event-class.md).|  
|DATABASE_OBJECT_ACCESS_GROUP|Esse evento é gerado sempre que objetos de banco de dados, como tipo de mensagem, assembly, contrato, são acessados. Ele é gerado para qualquer acesso a qualquer banco de dados. Observação: isso poderia gerar grandes registros de auditoria.<br /><br /> Equivalente a [Audit Database Object Access Event Class](../../../relational-databases/event-classes/audit-database-object-access-event-class.md).|  
|DATABASE_OBJECT_CHANGE_GROUP|Esse evento é gerado quando uma instrução CREATE, ALTER ou DROP é executada em objetos de banco de dados, como esquemas. Ele é gerado sempre que um objeto de banco de dados é criado, alterado ou descartado. Observação: isso poderia gerar volumes muito grandes de registros de auditoria.<br /><br /> Equivalente a [Audit Database Object Management Event Class](../../../relational-databases/event-classes/audit-database-object-management-event-class.md).|  
|DATABASE_OBJECT_OWNERSHIP_CHANGE_GROUP|Esse evento é gerado quando há uma alteração de proprietário para objetos dentro do escopo do banco de dados. Ele é gerado para qualquer alteração de propriedade de objeto em qualquer banco de dados no servidor. Equivalente a [Audit Database Object Take Ownership Event Class](../../../relational-databases/event-classes/audit-database-object-take-ownership-event-class.md).|  
|DATABASE_OBJECT_PERMISSION_CHANGE_GROUP|Esse evento é gerado quando GRANT, REVOKE ou DENY é emitido para objetos de banco de dados, como assemblies e esquemas. Ele é gerado para qualquer alteração de permissão de objeto em qualquer banco de dados no servidor. Equivalente a [Audit Database Object GDR Event Class](../../../relational-databases/event-classes/audit-database-object-gdr-event-class.md).|  
|DATABASE_OPERATION_GROUP|Esse evento é gerado quando ocorrem operações em um banco de dados, como um ponto de verificação ou uma notificação de consulta de assinatura. Esse evento é gerado em qualquer operação de banco de dados em qualquer banco de dados. Equivalente a [Audit Database Operation Event Class](../../../relational-databases/event-classes/audit-database-operation-event-class.md).|  
|DATABASE_OWNERSHIP_CHANGE_GROUP|Esse evento é gerado quando a instrução ALTER AUTHORIZATION é usada para alterar o proprietário de um banco de dados e as permissões necessárias para fazer isso estão marcadas. Ele é gerado para qualquer alteração de propriedade de banco de dados em qualquer banco de dados no servidor. Equivalente a [Audit Change Database Owner Event Class](../../../relational-databases/event-classes/audit-change-database-owner-event-class.md).|  
|DATABASE_PERMISSION_CHANGE_GROUP|Esse evento é gerado sempre que GRANT, REVOKE ou DENY é emitido para uma permissão de instrução por qualquer entidade no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (Isso se aplica a eventos somente de banco de dados, como conceder permissões em um banco de dados, por exemplo).<br /><br /> Esse evento é gerado para qualquer GDR (alteração de permissão de banco de dados) de algum banco de dados no servidor. Equivalente a [Audit Database Scope GDR Event Class](../../../relational-databases/event-classes/audit-database-scope-gdr-event-class.md).|  
|DATABASE_PRINCIPAL_CHANGE_GROUP|Esse evento é gerado quando entidades, como usuários, são criadas, alteradas ou descartadas de um banco de dados. Equivalente a [Audit Database Principal Management Event Class](../../../relational-databases/event-classes/audit-database-principal-management-event-class.md). (Também equivalente à Classe de Evento Audit Add DB Principal, que ocorre nos procedimentos armazenados sp_grantdbaccess, sp_revokedbaccess, sp_addPrincipal e sp_dropPrincipal preteridos.)<br /><br /> Esse evento é gerado sempre que uma função de banco de dados é adicionada ou removida mediante os procedimentos armazenados sp_addrole ou sp_droprole. Esse evento é gerado sempre que qualquer entidade de banco de dados é criada, alterada ou descartada de qualquer banco de dados. Equivalente a [Audit Add Role Event Class](../../../relational-databases/event-classes/audit-add-role-event-class.md).|  
|DATABASE_PRINCIPAL_IMPERSONATION_GROUP|Esse evento é gerado quando há uma operação de representação no escopo do banco de dados, como EXECUTE AS \<principal> ou SETPRINCIPAL. Ele é gerado para representações realizadas em qualquer banco de dados. Equivalente a [Audit Database Principal Impersonation Event Class](../../../relational-databases/event-classes/audit-database-principal-impersonation-event-class.md).|  
|DATABASE_ROLE_MEMBER_CHANGE_GROUP|Esse evento é gerado sempre que um logon é adicionado ou removido de uma função de banco de dados. Essa classe de evento é gerada para os procedimentos armazenados sp_addrolemember, sp_changegroup e sp_droprolemember. Esse evento é gerado em qualquer alteração do membro da função Banco de dados em qualquer banco de dados. Equivalente a [Classe de evento Audit Add Member to DB Role](../../../relational-databases/event-classes/audit-add-member-to-db-role-event-class.md).|  
|DBCC_GROUP|Esse evento é gerado sempre que uma entidade emite um comando DBCC. Equivalente a [Audit DBCC Event Class](../../../relational-databases/event-classes/audit-dbcc-event-class.md).|  
|SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP|Indica que uma entidade tentou fazer logon em um banco de dados independente e obteve falha. Os eventos nessa classe são gerados por novas conexões ou por conexões reutilizadas de um pool de conexões. Equivalente a [Audit Login Failed Event Class](../../../relational-databases/event-classes/audit-login-failed-event-class.md).|    
|FAILED_LOGIN_GROUP|Indica que uma entidade tentou efetuar logon no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e falhou. Os eventos nessa classe são gerados por novas conexões ou por conexões reutilizadas de um pool de conexões. Equivalente a [Audit Login Failed Event Class](../../../relational-databases/event-classes/audit-login-failed-event-class.md). Esta auditoria não se aplica ao Banco de Dados SQL do Azure.| 
|FULLTEXT_GROUP|Indica que ocorreu um evento de texto completo. Equivalente a [Audit Fulltext Event Class](../../../relational-databases/event-classes/audit-fulltext-event-class.md).|  
|LOGIN_CHANGE_PASSWORD_GROUP|Esse evento é gerado sempre que a senha de um logon for alterada pela instrução ALTER LOGIN ou pelo procedimento armazenado sp_password. Equivalente a [Audit Login Change Password Event Class](../../../relational-databases/event-classes/audit-login-change-password-event-class.md).|  
|LOGOUT_GROUP|Indica que uma entidade efetuou logoff no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os eventos nessa classe são gerados por novas conexões ou por conexões reutilizadas de um pool de conexões. Equivalente a [Audit Logout Event Class](../../../relational-databases/event-classes/audit-logout-event-class.md).|  
|SCHEMA_OBJECT_ACCESS_GROUP|Esse evento é gerado sempre que uma permissão de objeto é usada no esquema. Equivalente a [Audit Schema Object Access Event Class](../../../relational-databases/event-classes/audit-schema-object-access-event-class.md).|  
|SCHEMA_OBJECT_CHANGE_GROUP|Esse evento é gerado quando uma operação CREATE, ALTER ou DROP é executada em um esquema. Equivalente a [Audit Schema Object Management Event Class](../../../relational-databases/event-classes/audit-schema-object-management-event-class.md).<br /><br /> Esse evento é gerado em objetos de esquema. Equivalente a [Audit Object Derived Permission Event Class](../../../relational-databases/event-classes/audit-object-derived-permission-event-class.md).<br /><br /> Esse evento é gerado sempre que algum esquema de qualquer banco de dados é alterado. Equivalente a [Audit Statement Permission Event Class](../../../relational-databases/event-classes/audit-statement-permission-event-class.md).|  
|SCHEMA_OBJECT_OWNERSHIP_CHANGE_GROUP|Esse evento é gerado quando as permissões para alterar o proprietário do objeto de esquema (como uma tabela, um procedimento ou uma função) são verificadas. Isso ocorre quando a instrução ALTER AUTHORIZATION é usada para atribuir um proprietário a um objeto. Esse evento é gerado para qualquer alteração de propriedade de esquema em qualquer banco de dados do servidor. Equivalente a [Audit Schema Object Take Ownership Event Class](../../../relational-databases/event-classes/audit-schema-object-take-ownership-event-class.md).|  
|SCHEMA_OBJECT_PERMISSION_CHANGE_GROUP|Esse evento é gerado sempre que uma concessão, negação ou revogação é executada com relação a um objeto de esquema. Equivalente a [Audit Schema Object GDR Event Class](../../../relational-databases/event-classes/audit-schema-object-gdr-event-class.md).|  
|SERVER_OBJECT_CHANGE_GROUP|Esse evento é gerado para operações CREATE, ALTER ou DROP em objetos de servidor. Equivalente a [Audit Server Object Management Event Class](../../../relational-databases/event-classes/audit-server-object-management-event-class.md).|  
|SERVER_OBJECT_OWNERSHIP_CHANGE_GROUP|Esse evento é gerado quando o proprietário é alterado para objetos no escopo do servidor. Equivalente a [Audit Server Object Take Ownership Event Class](../../../relational-databases/event-classes/audit-server-object-take-ownership-event-class.md).|  
|SERVER_OBJECT_PERMISSION_CHANGE_GROUP|Esse evento é gerado quando GRANT, REVOKE ou DENY é emitido para uma permissão de objeto de servidor em qualquer entidade no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Equivalente a [Audit Server Object GDR Event Class](../../../relational-databases/event-classes/audit-server-object-gdr-event-class.md).|  
|SERVER_OPERATION_GROUP|Esse evento é gerado quando são usadas operações de auditoria de segurança, como alterar configurações, recursos, acesso externo ou autorização. Equivalente a [Audit Server Operation Event Class](../../../relational-databases/event-classes/audit-server-operation-event-class.md).|  
|SERVER_PERMISSION_CHANGE_GROUP|Esse evento é gerado quando GRANT, REVOKE ou DENY é emitido para permissões no escopo do servidor. Equivalente a [Audit Server Scope GDR Event Class](../../../relational-databases/event-classes/audit-server-scope-gdr-event-class.md).|  
|SERVER_PRINCIPAL_CHANGE_GROUP|Esse evento é gerado quando as entidades de servidor são criadas, alteradas ou descartadas. Equivalente a [Audit Server Principal Management Event Class](../../../relational-databases/event-classes/audit-server-principal-management-event-class.md).<br /><br /> Esse evento é gerado quando uma entidade emite os procedimentos armazenados sp_defaultdb ou sp_defaultlanguage ou as instruções ALTER LOGON. Equivalente a [Audit Addlogin Event Class](../../../relational-databases/event-classes/audit-addlogin-event-class.md).<br /><br /> Esse evento é gerado nos procedimentos armazenados sp_addlogin e sp_droplogin. Também equivalente a [Audit Login Change Property Event Class](../../../relational-databases/event-classes/audit-login-change-property-event-class.md).<br /><br /> Esse evento é gerado para os procedimentos armazenados sp_grantlogin ou sp_revokelogin. Equivalente a [Audit Login GDR Event Class](../../../relational-databases/event-classes/audit-login-gdr-event-class.md).|  
|SERVER_PRINCIPAL_IMPERSONATION_GROUP|Esse evento é gerado quando há uma representação dentro do escopo do servidor, como EXECUTE AS \<login>. Equivalente a [Audit Server Principal Impersonation Event Class](../../../relational-databases/event-classes/audit-server-principal-impersonation-event-class.md).|  
|SERVER_ROLE_MEMBER_CHANGE_GROUP|Esse evento é gerado sempre que um logon é adicionado ou removido de uma função de servidor fixa. Esse evento é gerado para os procedimentos armazenados sp_addsrvrolemember e sp_dropsrvrolemember. Equivalente a [Classe de evento Audit Add Login to Server Role](../../../relational-databases/event-classes/audit-add-login-to-server-role-event-class.md).|  
|SERVER_STATE_CHANGE_GROUP|Esse evento é gerado quando o estado do serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é modificado. Equivalente a [Audit Server Starts and Stops Event Class](../../../relational-databases/event-classes/audit-server-starts-and-stops-event-class.md).|  
|SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP|Indica que a entidade efetuou logon com êxito em um banco de dados independente.|  
|SUCCESSFUL_LOGIN_GROUP|Indica que a entidade efetuou logon com êxito no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os eventos nessa classe são gerados por novas conexões ou por conexões reutilizadas de um pool de conexões. Equivalente a [Audit Login Event Class](../../../relational-databases/event-classes/audit-login-event-class.md).|  
|TRACE_CHANGE_GROUP|Esse evento é gerado para todas as instruções que verificam a permissão ALTER TRACE. Equivalente a [Audit Server Alter Trace Event Class](../../../relational-databases/event-classes/audit-server-alter-trace-event-class.md).|  
|TRANSACTION_GROUP|Esse evento é gerado para operações BEGIN TRANSACTION, ROLLBACK TRANSACTION e COMMIT TRANSACTION, tanto para chamadas explícitas a essas instruções quanto para operações de transação implícita. Além disso, esse evento é gerado para operações UNDO de instruções individuais causadas pela reversão de uma transação.|  
|USER_CHANGE_PASSWORD_GROUP|Esse evento é gerado sempre que a senha de um usuário de banco de dados independente é alterada por meio da instrução ALTER USER.|  
|USER_DEFINED_AUDIT_GROUP|Este grupo monitora eventos gerados por meio de [sp_audit_write &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-audit-write-transact-sql.md). Normalmente, gatilhos ou procedimentos armazenados incluem chamadas para **sp_audit_write** para habilitar a auditoria de eventos importantes.|  
  
### <a name="considerations"></a>Considerações  
 Grupos de ações no nível do servidor abrangem ações em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Por exemplo, qualquer verificação de acesso de objeto de esquema em qualquer banco de dados será gravada se o grupo de ação apropriado for adicionado a uma especificação de auditoria de servidor. Em uma especificação de auditoria de banco de dados, somente acessos de objeto de esquema são registrados no banco de dados.  
  
 Ações no nível do servidor não permitem filtragem detalhada em ações no nível de banco de dados. Uma auditoria no nível do banco de dados, como auditoria de ações SELECT na tabela Clientes para logons no grupo Funcionário é necessária para implementar filtragem de ação detalhada. Não inclua objetos do escopo de servidor, como as exibições do sistema, em uma especificação de auditoria de banco de dados do usuário.  

 > [!NOTE]
 > Devido à sobrecarga envolvida em habilitar auditoria no nível da transação, do [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] SP2 CU3 e [!INCLUDE[ssSQL17](../../../includes/sssql17-md.md)] CU4 em diante, a auditoria no nível da transação é desabilitada por padrão, a menos que você tenha Conformidade de Critérios Comuns habilitada.  Se Conformidade de Critérios Comuns estiver desabilitada, você ainda poderá adicionar uma ação de TRANSACTION_GROUP a uma especificação de auditoria, mas ela coletará de fato nenhuma ação da transação.  Se você quiser configurar quaisquer ações de auditoria do TRANSACTION_GROUP, habilite a infraestrutura de auditoria no nível da transação habilitando a Conformidade de Critérios Comuns do [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)] SP2 CU3 e [!INCLUDE[ssSQL17](../../../includes/sssql17-md.md)] CU4 e posteriores em diante.  Observe que, no [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)], a auditoria no nível da transação também pode ser desabilitada e com o sinalizador de rastreamento 3427 do SP1 CU2 em diante.
  
## <a name="database-level-audit-action-groups"></a>Grupos de ação de auditoria no nível de banco de dados  
 Grupos de ação de auditoria no nível de banco de dados são ações semelhantes às classes de evento Security Audit Event do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obter mais informações sobre classes de evento, consulte [Referência de classe de evento do SQL Server](../../../relational-databases/event-classes/sql-server-event-class-reference.md).  
  
 A tabela a seguir descreve os grupos de ações de auditoria no nível de banco de dados e fornece a Classe de Evento do SQL Server equivalente onde aplicável.  
  
|Nome do grupo de ações|Descrição|  
|-----------------------|-----------------|  
|APPLICATION_ROLE_CHANGE_PASSWORD_GROUP|Esse evento é gerado sempre que uma senha é alterada por uma função de aplicativo. Equivalente a [Audit App Role Change Password Event Class](../../../relational-databases/event-classes/audit-app-role-change-password-event-class.md).|  
|AUDIT_CHANGE_GROUP|Esse evento é gerado sempre que uma auditoria é criada, modificada ou excluída. Esse evento é gerado sempre que qualquer especificação de auditoria é criada, modificada ou excluída. Qualquer alteração em uma auditoria é auditada nessa auditoria. Equivalente a [Audit Change Audit Event Class](../../../relational-databases/event-classes/audit-change-audit-event-class.md).|  
|BACKUP_RESTORE_GROUP|Esse evento é gerado sempre que um comando de backup ou restauração é emitido. Equivalente à [classe de evento Audit Backup and Restore](../../../relational-databases/event-classes/audit-backup-and-restore-event-class.md).|  
|BATCH_COMPLETED_GROUP|Esse evento é gerado sempre que qualquer operação de lote de texto, procedimento armazenado ou de gerenciamento de transações conclui a execução. Ele é gerado depois que o lote é concluído e audita o lote inteiro ou o texto do procedimento armazenado, conforme enviado do cliente, incluindo o resultado.|  
|BATCH_STARTED_GROUP|Esse evento é gerado sempre que qualquer operação de lote de texto, procedimento armazenado ou gerenciamento de transações começa a ser executada. Ele é gerado antes da execução e audita o lote inteiro ou o texto do procedimento armazenado, conforme enviado do cliente.|  
|DATABASE_CHANGE_GROUP|Esse evento é gerado quando um banco de dados é criado, alterado ou descartado. Equivalente a [Audit Database Management Event Class](../../../relational-databases/event-classes/audit-database-management-event-class.md).|  
|DATABASE_LOGOUT_GROUP|Esse evento é gerado quando um usuário de banco de dados independente faz logoff de um banco de dados. Equivalente à [classe de evento Audit Backup and Restore](../../../relational-databases/event-classes/audit-backup-and-restore-event-class.md).|  
|DATABASE_OBJECT_ACCESS_GROUP|Esse evento é gerado sempre que são acessados objetos de banco de dados, como certificados e chaves assimétricas. Equivalente a [Audit Database Object Access Event Class](../../../relational-databases/event-classes/audit-database-object-access-event-class.md).|  
|DATABASE_OBJECT_CHANGE_GROUP|Esse evento é gerado quando uma instrução CREATE, ALTER ou DROP é executada em objetos de banco de dados, como esquemas. Equivalente a [Audit Database Object Management Event Class](../../../relational-databases/event-classes/audit-database-object-management-event-class.md).|  
|DATABASE_OBJECT_OWNERSHIP_CHANGE_GROUP|Esse evento é gerado quando há uma alteração de proprietário para objetos dentro do escopo do banco de dados. Equivalente a [Audit Database Object Take Ownership Event Class](../../../relational-databases/event-classes/audit-database-object-take-ownership-event-class.md).|  
|DATABASE_OBJECT_PERMISSION_CHANGE_GROUP|Esse evento é gerado quando GRANT, REVOKE ou DENY é emitido para objetos de banco de dados, como assemblies e esquemas. Equivalente a [Audit Database Object GDR Event Class](../../../relational-databases/event-classes/audit-database-object-gdr-event-class.md).|  
|DATABASE_OPERATION_GROUP|Esse evento é gerado quando ocorrem operações em um banco de dados, como um ponto de verificação ou uma notificação de consulta de assinatura. Equivalente a [Audit Database Operation Event Class](../../../relational-databases/event-classes/audit-database-operation-event-class.md).|  
|DATABASE_OWNERSHIP_CHANGE_GROUP|Esse evento é gerado quando a instrução ALTER AUTHORIZATION é usada para alterar o proprietário de um banco de dados e as permissões necessárias para fazer isso estão marcadas. Equivalente a [Audit Change Database Owner Event Class](../../../relational-databases/event-classes/audit-change-database-owner-event-class.md).|  
|DATABASE_PERMISSION_CHANGE_GROUP|Esse evento é gerado sempre que GRANT, REVOKE ou DENY é emitido para uma permissão de instrução por qualquer usuário no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de eventos somente de banco de dados, como conceder permissões em um banco de dados. Equivalente a [Audit Database Scope GDR Event Class](../../../relational-databases/event-classes/audit-database-scope-gdr-event-class.md).|  
|DATABASE_PRINCIPAL_CHANGE_GROUP|Esse evento é gerado quando entidades, como usuários, são criadas, alteradas ou descartadas de um banco de dados. Equivalente a [Audit Database Principal Management Event Class](../../../relational-databases/event-classes/audit-database-principal-management-event-class.md). Também equivalente a [Classe de evento Audit Add DB User](../../../relational-databases/event-classes/audit-add-db-user-event-class.md), que ocorre nos procedimentos armazenados sp_grantdbaccess, sp_revokedbaccess, sp_adduser e sp_dropuser preteridos.<br /><br /> Esse evento é gerado sempre que uma função de banco de dados é adicionada ou removida mediante os procedimentos armazenados sp_addrole e sp_droprole preteridos. Equivalente a [Audit Add Role Event Class](../../../relational-databases/event-classes/audit-add-role-event-class.md).|  
|DATABASE_PRINCIPAL_IMPERSONATION_GROUP|Esse evento é gerado quando há uma representação dentro do escopo do banco de dados, como EXECUTE AS \<user>. Equivalente a [Audit Database Principal Impersonation Event Class](../../../relational-databases/event-classes/audit-database-principal-impersonation-event-class.md).|  
|DATABASE_ROLE_MEMBER_CHANGE_GROUP|Esse evento é gerado sempre que um logon é adicionado ou removido de uma função de banco de dados. Essa classe de evento é usada com os procedimentos armazenados sp_addrolemember, sp_changegroup e sp_droprolemember. Equivalente à [Classe de evento Audit Add Member to DB Role](../../../relational-databases/event-classes/audit-add-member-to-db-role-event-class.md)|  
|DBCC_GROUP|Esse evento é gerado sempre que uma entidade emite um comando DBCC. Equivalente a [Audit DBCC Event Class](../../../relational-databases/event-classes/audit-dbcc-event-class.md).|  
|SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP|Indica que uma entidade tentou fazer logon em um banco de dados independente e obteve falha. Os eventos nessa classe são gerados por novas conexões ou por conexões reutilizadas de um pool de conexões. Esse evento é gerado.|  
|SCHEMA_OBJECT_ACCESS_GROUP|Esse evento é gerado sempre que uma permissão de objeto é usada no esquema. Equivalente a [Audit Schema Object Access Event Class](../../../relational-databases/event-classes/audit-schema-object-access-event-class.md).|  
|SCHEMA_OBJECT_CHANGE_GROUP|Esse evento é gerado quando uma operação CREATE, ALTER ou DROP é executada em um esquema. Equivalente a [Audit Schema Object Management Event Class](../../../relational-databases/event-classes/audit-schema-object-management-event-class.md).<br /><br /> Esse evento é gerado em objetos de esquema. Equivalente a [Audit Object Derived Permission Event Class](../../../relational-databases/event-classes/audit-object-derived-permission-event-class.md). Também equivalente a [Audit Statement Permission Event Class](../../../relational-databases/event-classes/audit-statement-permission-event-class.md).|  
|SCHEMA_OBJECT_OWNERSHIP_CHANGE_GROUP|Esse evento é gerado quando as permissões para alterar o proprietário do objeto de esquema, como uma tabela, um procedimento ou função é verificada. Isso ocorre quando a instrução ALTER AUTHORIZATION é usada para atribuir um proprietário a um objeto. Equivalente a [Audit Schema Object Take Ownership Event Class](../../../relational-databases/event-classes/audit-schema-object-take-ownership-event-class.md).|  
|SCHEMA_OBJECT_PERMISSION_CHANGE_GROUP|Esse evento é gerado sempre que uma concessão, negação ou revogação é emitida para um objeto de esquema. Equivalente a [Audit Schema Object GDR Event Class](../../../relational-databases/event-classes/audit-schema-object-gdr-event-class.md).|  
|SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP|Indica que a entidade efetuou logon com êxito em um banco de dados independente.|  
|USER_CHANGE_PASSWORD_GROUP|Esse evento é gerado sempre que a senha de um usuário de banco de dados independente é alterada por meio da instrução ALTER USER.|  
|USER_DEFINED_AUDIT_GROUP|Este grupo monitora eventos gerados por meio de [sp_audit_write &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-audit-write-transact-sql.md).|  
  
## <a name="database-level-audit-actions"></a>Ações de auditoria no nível do banco de dados  
 Ações no nível do banco de dados oferecem suporte à auditoria de ações específicas diretamente no esquema do banco de dados e em objetos do esquema, como tabelas, exibições, procedimentos armazenados, funções, procedimentos armazenados estendidos, filas e sinônimos. Tipos, coleção de esquema XML, banco de dados e esquema não são auditados. A auditoria de objetos de esquema pode ser configurada no esquema e no banco de dados, o que indica que os eventos em todos os objetos do esquema contidos no esquema ou banco de dados especificado serão auditados. A tabela a seguir descreve ações de auditoria no nível de banco de dados.  
  
|Ação|Descrição|  
|------------|-----------------|  
|SELECT|Esse evento é gerado sempre que SELECT é emitido.|  
|UPDATE|Esse evento é gerado sempre que UPDATE é emitido.|  
|INSERT|Esse evento é gerado sempre que INSERT é emitido.|  
|Delete (excluir)|Esse evento é gerado sempre que DELETE é emitido.|  
|Execute|Esse evento é gerado sempre que EXECUTE é emitido.|  
|RECEIVE|Esse evento é gerado sempre que RECEIVE é emitido.|  
|REFERENCES|Esse evento é gerado sempre que uma permissão REFERENCES é verificada.|  
  
### <a name="considerations"></a>Considerações  
*  As ações de auditoria no nível de banco de dados não se aplicam a Colunas.  
  
*  Quando o processador de consulta parametriza a consulta, o parâmetro pode aparecer no log de eventos de auditoria em vez de nos valores de coluna da consulta. 
 
*  As instruções de RPC não são registradas. 
  
## <a name="audit-level-audit-action-groups"></a>Grupos de ação de auditoria no nível de auditoria  
 Também é possível auditar as ações no processo de auditoria. Isso pode ocorrer no escopo de servidor ou no escopo do banco de dados. No escopo do banco de dados, isso ocorre somente para especificações de auditoria de banco de dados. A tabela a seguir descreve grupos de ações de auditoria no nível da auditoria.  
  
|Nome do grupo de ações|Descrição|  
|-----------------------|-----------------|  
|AUDIT_CHANGE_GROUP|Esse evento é gerado sempre que um dos comandos a seguir é emitido:<br /><br /> CREATE SERVER AUDIT<br /><br /> ALTER SERVER AUDIT<br /><br /> DROP SERVER AUDIT<br /><br /> CREATE SERVER AUDIT SPECIFICATION<br /><br /> ALTER SERVER AUDIT SPECIFICATION<br /><br /> DROP SERVER AUDIT SPECIFICATION<br /><br /> CREATE DATABASE AUDIT SPECIFICATION<br /><br /> ALTER DATABASE AUDIT SPECIFICATION<br /><br /> DROP DATABASE AUDIT SPECIFICATION|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
 [Criar uma especificação de auditoria de banco de dados e de servidor](../../../relational-databases/security/auditing/create-a-server-audit-and-database-audit-specification.md)  
  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-transact-sql.md)  
  
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-audit-transact-sql.md)  
  
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-server-audit-transact-sql.md)  
  
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/create-server-audit-specification-transact-sql.md)  
  
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-server-audit-specification-transact-sql.md)  
  
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-server-audit-specification-transact-sql.md)  
  
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/create-database-audit-specification-transact-sql.md)  
  
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-database-audit-specification-transact-sql.md)  
  
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](../../../t-sql/statements/drop-database-audit-specification-transact-sql.md)  
  
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../../t-sql/statements/alter-authorization-transact-sql.md)  
  
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)  
  
 [sys.server_audits &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)  
  
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)  
  
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)  
  
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)  
  
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)  
  
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)  
  
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)  
  
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)  
  
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)  
  
  
