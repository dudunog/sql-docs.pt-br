---
title: Ações e grupos de ações de auditoria do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 10/19/2016
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: e204a1865c2a928079fcd9b32b31a8ae0c0bd0a8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63238130"
---
# <a name="sql-server-audit-action-groups-and-actions"></a>Ações e grupos de ações de auditoria do SQL Server
  O recurso [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit permite auditar grupos de eventos e eventos individuais no nível do servidor e do banco de dados. Para obter mais informações, veja [Auditoria do SQL Server &#40;Mecanismo de Banco de Dados&#41;](sql-server-audit-database-engine.md).  
  
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
 Grupos de ação de auditoria no nível do servidor são ações semelhantes às classes de evento security audit do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obter mais informações, confira [Referência de classe de evento do SQL Server](../../event-classes/sql-server-event-class-reference.md).  
  
 A tabela a seguir descreve os grupos de ações de auditoria no nível do servidor e fornece a Classe de Evento SQL Server equivalente onde aplicável.  
  
|Nome do grupo de ações|DESCRIÇÃO|  
|-----------------------|-----------------|  
|APPLICATION_ROLE_CHANGE_PASSWORD_GROUP|Esse evento é gerado sempre que uma senha é alterada por uma função de aplicativo. Equivalente a [Audit App Role Change Password Event Class](../../event-classes/audit-app-role-change-password-event-class.md).|  
|AUDIT_CHANGE_GROUP|Esse evento é gerado sempre que uma auditoria é criada, modificada ou excluída. Esse evento é gerado sempre que qualquer especificação de auditoria é criada, modificada ou excluída. Qualquer alteração em uma auditoria é auditada nessa auditoria. Equivalente a [Audit Change Audit Event Class](../../event-classes/audit-change-audit-event-class.md).|  
|BACKUP_RESTORE_GROUP|Esse evento é gerado sempre que um comando de backup ou restauração é emitido. Equivalente à [classe de evento Audit Backup and Restore](../../event-classes/audit-backup-and-restore-event-class.md).|  
|BROKER_LOGIN_GROUP|Esse evento é gerado para relatar mensagens de auditoria relacionadas à segurança de transporte do Service Broker. Equivalente a [Audit Broker Login Event Class](../../event-classes/audit-broker-login-event-class.md).|  
|DATABASE_CHANGE_GROUP|Esse evento é gerado quando um banco de dados é criado, alterado ou descartado. Esse evento é gerado sempre que um banco de dados é criado, alterado ou descartado. Equivalente a [Audit Database Management Event Class](../../event-classes/audit-database-management-event-class.md).|  
|DATABASE_LOGOUT_GROUP|Esse evento é gerado quando um usuário de banco de dados independente faz logoff de um banco de dados. Equivalente à classe de evento Audit Database Logout.|  
|DATABASE_MIRRORING_LOGIN_GROUP|Esse evento é gerado para relatar mensagens de auditoria relacionadas à segurança de transporte de espelhamento de banco de dados. Equivalente a [Audit Database Mirroring Login Event Class](../../event-classes/audit-database-mirroring-login-event-class.md).|  
|DATABASE_OBJECT_ACCESS_GROUP|Esse evento é gerado sempre que objetos de banco de dados, como tipo de mensagem, assembly, contrato, são acessados.<br /><br /> Ele é gerado para qualquer acesso a qualquer banco de dados. **Observação:**  Isso poderia potencialmente levar a registros de auditoria grandes. <br /><br /> Equivalente a [Audit Database Object Access Event Class](../../event-classes/audit-database-object-access-event-class.md).|  
|DATABASE_OBJECT_CHANGE_GROUP|Esse evento é gerado quando uma instrução CREATE, ALTER ou DROP é executada em objetos de banco de dados, como esquemas. Ele é gerado sempre que um objeto de banco de dados é criado, alterado ou descartado. **Observação:**  Isso pode levar a grandes quantidades de registros de auditoria. <br /><br /> Equivalente a [Audit Database Object Management Event Class](../../event-classes/audit-database-object-management-event-class.md).|  
|DATABASE_OBJECT_OWNERSHIP_CHANGE_GROUP|Esse evento é gerado quando há uma alteração de proprietário para objetos dentro do escopo do banco de dados. Ele é gerado para qualquer alteração de propriedade de objeto em qualquer banco de dados no servidor. Equivalente a [Audit Database Object Take Ownership Event Class](../../event-classes/audit-database-object-take-ownership-event-class.md).|  
|DATABASE_OBJECT_PERMISSION_CHANGE_GROUP|Esse evento é gerado quando GRANT, REVOKE ou DENY é emitido para objetos de banco de dados, como assemblies e esquemas. Ele é gerado para qualquer alteração de permissão de objeto em qualquer banco de dados no servidor. Equivalente a [Audit Database Object GDR Event Class](../../event-classes/audit-database-object-gdr-event-class.md).|  
|DATABASE_OPERATION_GROUP|Esse evento é gerado quando ocorrem operações em um banco de dados, como um ponto de verificação ou uma notificação de consulta de assinatura. Esse evento é gerado em qualquer operação de banco de dados em qualquer banco de dados. Equivalente a [Audit Database Operation Event Class](../../event-classes/audit-database-operation-event-class.md).|  
|DATABASE_OWNERSHIP_CHANGE_GROUP|Esse evento é gerado quando a instrução ALTER AUTHORIZATION é usada para alterar o proprietário de um banco de dados e as permissões necessárias para fazer isso estão marcadas. Ele é gerado para qualquer alteração de propriedade de banco de dados em qualquer banco de dados no servidor. Equivalente a [Audit Change Database Owner Event Class](../../event-classes/audit-change-database-owner-event-class.md).|  
|DATABASE_PERMISSION_CHANGE_GROUP|Esse evento é gerado sempre que GRANT, REVOKE ou DENY é emitido para uma permissão de instrução por qualquer entidade no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (Isso se aplica a eventos somente de banco de dados, como conceder permissões em um banco de dados, por exemplo).<br /><br /> Esse evento é gerado para qualquer GDR (alteração de permissão de banco de dados) de algum banco de dados no servidor. Equivalente a [Audit Database Scope GDR Event Class](../../event-classes/audit-database-scope-gdr-event-class.md).|  
|DATABASE_PRINCIPAL_CHANGE_GROUP|Esse evento é gerado quando entidades, como usuários, são criadas, alteradas ou descartadas de um banco de dados. Equivalente a [Audit Database Principal Management Event Class](../../event-classes/audit-database-principal-management-event-class.md). (Também equivalente à Classe de Evento Audit Add DB Principal, que ocorre nos procedimentos armazenados sp_grantdbaccess, sp_revokedbaccess, sp_addPrincipal e sp_dropPrincipal preteridos.)<br /><br /> Esse evento é gerado sempre que uma função de banco de dados é adicionada ou removida mediante os procedimentos armazenados sp_addrole ou sp_droprole. Esse evento é gerado sempre que qualquer entidade de banco de dados é criada, alterada ou descartada de qualquer banco de dados. Equivalente a [Audit Add Role Event Class](../../event-classes/audit-add-role-event-class.md).|  
|DATABASE_PRINCIPAL_IMPERSONATION_GROUP|Esse evento é gerado quando há uma operação de representação no escopo do banco de dados, como EXECUTE AS \<entidade> ou SETPRINCIPAL. Ele é gerado para representações realizadas em qualquer banco de dados. Equivalente a [Audit Database Principal Impersonation Event Class](../../event-classes/audit-database-principal-impersonation-event-class.md).|  
|DATABASE_ROLE_MEMBER_CHANGE_GROUP|Esse evento é gerado sempre que um logon é adicionado ou removido de uma função de banco de dados. Essa classe de evento é gerada para os procedimentos armazenados sp_addrolemember, sp_changegroup e sp_droprolemember. Esse evento é gerado em qualquer alteração do membro da função Banco de dados em qualquer banco de dados. Equivalente a [Classe de evento Audit Add Member to DB Role
](../../event-classes/audit-add-member-to-db-role-event-class.md).|  
|DBCC_GROUP|Esse evento é gerado sempre que uma entidade emite um comando DBCC. Equivalente a [Audit DBCC Event Class](../../event-classes/audit-dbcc-event-class.md).|  
|SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP|Indica que uma entidade tentou fazer logon em um banco de dados independente e obteve falha. Os eventos nessa classe são gerados por novas conexões ou por conexões reutilizadas de um pool de conexões. Equivalente a [Audit Login Failed Event Class](../../event-classes/audit-login-failed-event-class.md).|  
|FAILED_LOGIN_GROUP|Indica que uma entidade tentou efetuar logon no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e falhou. Os eventos nessa classe são gerados por novas conexões ou por conexões reutilizadas de um pool de conexões. Equivalente a [Audit Login Failed Event Class](../../event-classes/audit-login-failed-event-class.md).|  
|FULLTEXT_GROUP|Indica que ocorreu um evento de texto completo. Equivalente a [Audit Fulltext Event Class](../../event-classes/audit-fulltext-event-class.md).|  
|LOGIN_CHANGE_PASSWORD_GROUP|Esse evento é gerado sempre que a senha de um logon for alterada pela instrução ALTER LOGIN ou pelo procedimento armazenado sp_password. Equivalente a [Audit Login Change Password Event Class](../../event-classes/audit-login-change-password-event-class.md).|  
|LOGOUT_GROUP|Indica que uma entidade efetuou logoff no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os eventos nessa classe são gerados por novas conexões ou por conexões reutilizadas de um pool de conexões. Equivalente a [Audit Logout Event Class](../../event-classes/audit-logout-event-class.md).|  
|SCHEMA_OBJECT_ACCESS_GROUP|Esse evento é gerado sempre que uma permissão de objeto é usada no esquema. Equivalente a [Audit Schema Object Access Event Class](../../event-classes/audit-schema-object-access-event-class.md).|  
|SCHEMA_OBJECT_CHANGE_GROUP|Esse evento é gerado quando uma operação CREATE, ALTER ou DROP é executada em um esquema. Equivalente a [Audit Schema Object Management Event Class](../../event-classes/audit-schema-object-management-event-class.md).<br /><br /> Esse evento é gerado em objetos de esquema. Equivalente a [Audit Object Derived Permission Event Class](../../event-classes/audit-object-derived-permission-event-class.md).<br /><br /> Esse evento é gerado sempre que algum esquema de qualquer banco de dados é alterado. Equivalente a [Audit Statement Permission Event Class](../../event-classes/audit-statement-permission-event-class.md).|  
|SCHEMA_OBJECT_OWNERSHIP_CHANGE_GROUP|Esse evento é gerado quando as permissões para alterar o proprietário do objeto de esquema (como uma tabela, um procedimento ou uma função) são verificadas. Isso ocorre quando a instrução ALTER AUTHORIZATION é usada para atribuir um proprietário a um objeto. Esse evento é gerado para qualquer alteração de propriedade de esquema em qualquer banco de dados do servidor. Equivalente a [Audit Schema Object Take Ownership Event Class](../../event-classes/audit-schema-object-take-ownership-event-class.md).|  
|SCHEMA_OBJECT_PERMISSION_CHANGE_GROUP|Esse evento é gerado sempre que uma concessão, negação ou revogação é executada com relação a um objeto de esquema. Equivalente a [Audit Schema Object GDR Event Class](../../event-classes/audit-schema-object-gdr-event-class.md).|  
|SERVER_OBJECT_CHANGE_GROUP|Esse evento é gerado para operações CREATE, ALTER ou DROP em objetos de servidor. Equivalente a [Audit Server Object Management Event Class](../../event-classes/audit-server-object-management-event-class.md).|  
|SERVER_OBJECT_OWNERSHIP_CHANGE_GROUP|Esse evento é gerado quando o proprietário é alterado para objetos no escopo do servidor. Equivalente a [Audit Server Object Take Ownership Event Class](../../event-classes/audit-server-object-take-ownership-event-class.md).|  
|SERVER_OBJECT_PERMISSION_CHANGE_GROUP|Esse evento é gerado quando GRANT, REVOKE ou DENY é emitido para uma permissão de objeto de servidor em qualquer entidade no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Equivalente a [Audit Server Object GDR Event Class](../../event-classes/audit-server-object-gdr-event-class.md).|  
|SERVER_OPERATION_GROUP|Esse evento é gerado quando são usadas operações de auditoria de segurança, como alterar configurações, recursos, acesso externo ou autorização. Equivalente a [Audit Server Operation Event Class](../../event-classes/audit-server-operation-event-class.md).|  
|SERVER_PERMISSION_CHANGE_GROUP|Esse evento é gerado quando GRANT, REVOKE ou DENY é emitido para permissões no escopo do servidor, como criar um logon. Equivalente a [Audit Server Scope GDR Event Class](../../event-classes/audit-server-scope-gdr-event-class.md).|  
|SERVER_PRINCIPAL_CHANGE_GROUP|Esse evento é gerado quando as entidades de servidor são criadas, alteradas ou descartadas. Equivalente a [Audit Server Principal Management Event Class](../../event-classes/audit-server-principal-management-event-class.md).<br /><br /> Esse evento é gerado quando uma entidade emite os procedimentos armazenados sp_defaultdb ou sp_defaultlanguage ou as instruções ALTER LOGON. Equivalente a [Audit Addlogin Event Class](../../event-classes/audit-addlogin-event-class.md).<br /><br /> Esse evento é gerado nos procedimentos armazenados sp_addlogin e sp_droplogin. Também equivalente a [Audit Login Change Property Event Class](../../event-classes/audit-login-change-property-event-class.md).<br /><br /> Esse evento é gerado para o sp_grantlogin ou sp_revokelogin procedimentos armazenados. Equivalente a [Audit Login GDR Event Class](../../event-classes/audit-login-gdr-event-class.md).|  
|SERVER_PRINCIPAL_IMPERSONATION_GROUP|Esse evento é gerado quando há uma representação dentro do escopo do servidor, como EXECUTE AS \<logon>. Equivalente a [Audit Server Principal Impersonation Event Class](../../event-classes/audit-server-principal-impersonation-event-class.md).|  
|SERVER_ROLE_MEMBER_CHANGE_GROUP|Esse evento é gerado sempre que um logon é adicionado ou removido de uma função de servidor fixa. Esse evento é gerado para os procedimentos armazenados sp_addsrvrolemember e sp_dropsrvrolemember. Equivalente a [Classe de evento Audit Add Login to Server Role
](../../event-classes/audit-add-login-to-server-role-event-class.md).|  
|SERVER_STATE_CHANGE_GROUP|Esse evento é gerado quando o estado do serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é modificado. Equivalente a [Audit Server Starts and Stops Event Class](../../event-classes/audit-server-starts-and-stops-event-class.md).|  
|SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP|Indica que a entidade efetuou logon com êxito em um banco de dados independente. Equivalente à classe de evento Audit Successful Database Authentication.|  
|SUCCESSFUL_LOGIN_GROUP|Indica que a entidade efetuou logon com êxito no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os eventos nessa classe são gerados por novas conexões ou por conexões reutilizadas de um pool de conexões. Equivalente a [Audit Login Event Class](../../event-classes/audit-login-event-class.md).|  
|TRACE_CHANGE_GROUP|Esse evento é gerado para todas as instruções que verificam a permissão ALTER TRACE. Equivalente a [Audit Server Alter Trace Event Class](../../event-classes/audit-server-alter-trace-event-class.md).|  
|USER_CHANGE_PASSWORD_GROUP|Esse evento é gerado sempre que a senha de um usuário de banco de dados independente é alterada por meio da instrução ALTER USER.|  
|USER_DEFINED_AUDIT_GROUP|Este grupo monitora eventos gerados por meio de [sp_audit_write &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-audit-write-transact-sql). Normalmente, gatilhos ou procedimentos armazenados incluem chamadas para `sp_audit_write` para habilitar a auditoria de eventos importantes.|  
  
### <a name="considerations"></a>Considerações  
 Grupos de ações no nível do servidor abrangem ações em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Por exemplo, qualquer verificação de acesso de objeto de esquema em qualquer banco de dados será gravada se o grupo de ação apropriado for adicionado a uma especificação de auditoria de servidor. Em uma especificação de auditoria de banco de dados, somente acessos de objeto de esquema são registrados no banco de dados.  
  
 Ações no nível do servidor não permitem filtragem detalhada em ações no nível de banco de dados. Uma auditoria no nível do banco de dados, como auditoria de ações SELECT na tabela Clientes para logons no grupo Funcionário é necessária para implementar filtragem de ação detalhada. Não inclua objetos do escopo de servidor, como as exibições do sistema, em uma especificação de auditoria de banco de dados do usuário.  
  
## <a name="database-level-audit-action-groups"></a>Grupos de ação de auditoria no nível de banco de dados  
 Grupos de ação de auditoria no nível de banco de dados são ações semelhantes às classes de evento Security Audit Event do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Para obter mais informações sobre classes de evento, consulte [Referência de classe de evento do SQL Server](../../event-classes/sql-server-event-class-reference.md).  
  
 A tabela a seguir descreve os grupos de ações de auditoria no nível de banco de dados e fornece a Classe de Evento do SQL Server equivalente onde aplicável.  
  
|Nome do grupo de ações|Descrição|  
|-----------------------|-----------------|  
|APPLICATION_ROLE_CHANGE_PASSWORD_GROUP|Esse evento é gerado sempre que uma senha é alterada por uma função de aplicativo. Equivalente a [Audit App Role Change Password Event Class](../../event-classes/audit-app-role-change-password-event-class.md).|  
|AUDIT_CHANGE_GROUP|Esse evento é gerado sempre que uma auditoria é criada, modificada ou excluída. Esse evento é gerado sempre que qualquer especificação de auditoria é criada, modificada ou excluída. Qualquer alteração em uma auditoria é auditada nessa auditoria. Equivalente a [Audit Change Audit Event Class](../../event-classes/audit-change-audit-event-class.md).|  
|BACKUP_RESTORE_GROUP|Esse evento é gerado sempre que um comando de backup ou restauração é emitido. Equivalente à [classe de evento Audit Backup and Restore](../../event-classes/audit-backup-and-restore-event-class.md).|  
|DATABASE_CHANGE_GROUP|Esse evento é gerado quando um banco de dados é criado, alterado ou descartado. Equivalente a [Audit Database Management Event Class](../../event-classes/audit-database-management-event-class.md).|  
|DATABASE_LOGOUT_GROUP|Esse evento é gerado quando um usuário de banco de dados independente faz logoff de um banco de dados. Equivalente à [classe de evento Audit Backup and Restore](../../event-classes/audit-backup-and-restore-event-class.md).|  
|DATABASE_OBJECT_ACCESS_GROUP|Esse evento é gerado sempre que são acessados objetos de banco de dados, como certificados e chaves assimétricas. Equivalente a [Audit Database Object Access Event Class](../../event-classes/audit-database-object-access-event-class.md).|  
|DATABASE_OBJECT_CHANGE_GROUP|Esse evento é gerado quando uma instrução CREATE, ALTER ou DROP é executada em objetos de banco de dados, como esquemas. Equivalente a [Audit Database Object Management Event Class](../../event-classes/audit-database-object-management-event-class.md).|  
|DATABASE_OBJECT_OWNERSHIP_CHANGE_GROUP|Esse evento é gerado quando há uma alteração de proprietário para objetos dentro do escopo do banco de dados. Equivalente a [Audit Database Object Take Ownership Event Class](../../event-classes/audit-database-object-take-ownership-event-class.md).|  
|DATABASE_OBJECT_PERMISSION_CHANGE_GROUP|Esse evento é gerado quando GRANT, REVOKE ou DENY é emitido para objetos de banco de dados, como assemblies e esquemas. Equivalente a [Audit Database Object GDR Event Class](../../event-classes/audit-database-object-gdr-event-class.md).|  
|DATABASE_OPERATION_GROUP|Esse evento é gerado quando ocorrem operações em um banco de dados, como um ponto de verificação ou uma notificação de consulta de assinatura. Equivalente a [Audit Database Operation Event Class](../../event-classes/audit-database-operation-event-class.md).|  
|DATABASE_OWNERSHIP_CHANGE_GROUP|Esse evento é gerado quando a instrução ALTER AUTHORIZATION é usada para alterar o proprietário de um banco de dados e as permissões necessárias para fazer isso estão marcadas. Equivalente a [Audit Change Database Owner Event Class](../../event-classes/audit-change-database-owner-event-class.md).|  
|DATABASE_PERMISSION_CHANGE_GROUP|Esse evento é gerado sempre que GRANT, REVOKE ou DENY é emitido para uma permissão de instrução por qualquer usuário no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de eventos somente de banco de dados, como conceder permissões em um banco de dados. Equivalente a [Audit Database Scope GDR Event Class](../../event-classes/audit-database-scope-gdr-event-class.md).|  
|DATABASE_PRINCIPAL_CHANGE_GROUP|Esse evento é gerado quando entidades, como usuários, são criadas, alteradas ou descartadas de um banco de dados. Equivalente a [Audit Database Principal Management Event Class](../../event-classes/audit-database-principal-management-event-class.md). Também equivalente a [Classe de evento Audit Add DB User](../../event-classes/audit-add-db-user-event-class.md), que ocorre nos procedimentos armazenados sp_grantdbaccess, sp_revokedbaccess, sp_adduser e sp_dropuser preteridos.<br /><br /> Esse evento é gerado sempre que uma função de banco de dados é adicionada ou removida mediante os procedimentos armazenados sp_addrole e sp_droprole preteridos. Equivalente a [Audit Add Role Event Class](../../event-classes/audit-add-role-event-class.md).|  
|DATABASE_PRINCIPAL_IMPERSONATION_GROUP|Esse evento é gerado quando há uma representação dentro do escopo do banco de dados, \<como execute as User> ou SETUSER. Equivalente a [Audit Database Principal Impersonation Event Class](../../event-classes/audit-database-principal-impersonation-event-class.md).|  
|DATABASE_ROLE_MEMBER_CHANGE_GROUP|Esse evento é gerado sempre que um logon é adicionado ou removido de uma função de banco de dados. Essa classe de evento é usada com os procedimentos armazenados sp_addrolemember, sp_changegroup e sp_droprolemember. Equivalente à [Classe de evento Audit Add Member to DB Role](../../event-classes/audit-add-member-to-db-role-event-class.md)|  
|DBCC_GROUP|Esse evento é gerado sempre que uma entidade emite um comando DBCC. Equivalente a [Audit DBCC Event Class](../../event-classes/audit-dbcc-event-class.md).|  
|SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP|Indica que uma entidade tentou fazer logon em um banco de dados independente e obteve falha. Os eventos nessa classe são gerados por novas conexões ou por conexões reutilizadas de um pool de conexões. Esse evento é gerado.|  
|SCHEMA_OBJECT_ACCESS_GROUP|Esse evento é gerado sempre que uma permissão de objeto é usada no esquema. Equivalente a [Audit Schema Object Access Event Class](../../event-classes/audit-schema-object-access-event-class.md).|  
|SCHEMA_OBJECT_CHANGE_GROUP|Esse evento é gerado quando uma operação CREATE, ALTER ou DROP é executada em um esquema. Equivalente a [Audit Schema Object Management Event Class](../../event-classes/audit-schema-object-management-event-class.md).<br /><br /> Esse evento é gerado em objetos de esquema. Equivalente a [Audit Object Derived Permission Event Class](../../event-classes/audit-object-derived-permission-event-class.md). Também equivalente a [Audit Statement Permission Event Class](../../event-classes/audit-statement-permission-event-class.md).|  
|SCHEMA_OBJECT_OWNERSHIP_CHANGE_GROUP|Esse evento é gerado quando as permissões para alterar o proprietário do objeto de esquema, como uma tabela, um procedimento ou função é verificada. Isso ocorre quando a instrução ALTER AUTHORIZATION é usada para atribuir um proprietário a um objeto. Equivalente a [Audit Schema Object Take Ownership Event Class](../../event-classes/audit-schema-object-take-ownership-event-class.md).|  
|SCHEMA_OBJECT_PERMISSION_CHANGE_GROUP|Esse evento é gerado sempre que uma concessão, negação ou revogação é emitida para um objeto de esquema. Equivalente a [Audit Schema Object GDR Event Class](../../event-classes/audit-schema-object-gdr-event-class.md).|  
|SUCCESSFUL_DATABASE_AUTHENTICATION_GROUP|Indica que a entidade efetuou logon com êxito em um banco de dados independente. Equivalente à classe de evento Audit Successful Database Authentication.|  
|USER_CHANGE_PASSWORD_GROUP|Esse evento é gerado sempre que a senha de um usuário de banco de dados independente é alterada por meio da instrução ALTER USER.|  
|USER_DEFINED_AUDIT_GROUP|Este grupo monitora eventos gerados por meio de [sp_audit_write &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-audit-write-transact-sql).|  
  
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
|AUDIT_ CHANGE_GROUP|Esse evento é gerado sempre que um dos comandos a seguir é emitido:<br /><br /> -CRIAR AUDITORIA DE SERVIDOR<br />-ALTERAR AUDITORIA DO SERVIDOR<br />-REMOVER AUDITORIA DE SERVIDOR<br />-CRIAR ESPECIFICAÇÃO DE AUDITORIA DE SERVIDOR<br />-ALTERAR ESPECIFICAÇÃO DE AUDITORIA DE SERVIDOR<br />-DROP ESPECIFICAÇÃO DE AUDITORIA DE SERVIDOR<br />-CRIAR ESPECIFICAÇÃO DE AUDITORIA DE BANCO DE DADOS<br />-ESPECIFICAÇÃO DE AUDITORIA ALTER DATABASE<br />-REMOVER ESPECIFICAÇÃO DE AUDITORIA DE BANCO DE DADOS|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](create-a-server-audit-and-server-audit-specification.md)  
  
 [Criar uma especificação de auditoria de banco de dados e de servidor](create-a-server-audit-and-database-audit-specification.md)  
  
 [CREATE SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-transact-sql)  
  
 [ALTER SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-audit-specification-transact-sql)  
  
 [DROP SERVER AUDIT &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-server-audit-transact-sql)  
  
 [CREATE SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-server-audit-specification-transact-sql)  
  
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-audit-transact-sql)  
  
 [DROP SERVER AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-server-audit-specification-transact-sql)  
  
 [CREATE DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-audit-specification-transact-sql)  
  
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-audit-specification-transact-sql)  
  
 [DROP DATABASE AUDIT SPECIFICATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-encryption-key-transact-sql)  
  
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-authorization-transact-sql)  
  
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql)  
  
 [sys.server_audits &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-audits-transact-sql)  
  
 [sys.server_file_audits &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-file-audits-transact-sql)  
  
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql)  
  
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql)  
  
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql)  
  
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql)  
  
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql)  
  
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql)  
  
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql)  
  
  
