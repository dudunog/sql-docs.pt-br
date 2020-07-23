---
title: Auditoria do SQL Server (Mecanismo de Banco de Dados) | Microsoft Docs
description: Saiba mais sobre as auditorias de servidor do Mecanismo de Banco de Dados do SQL Server ou de um banco de dados individual. As auditorias de servidor contêm as especificações de auditoria de servidor e de banco de dados.
ms.custom: ''
ms.date: 01/01/2020
ms.prod: sql
ms.prod_service: security
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
f1_keywords:
- audit
helpviewer_keywords:
- SQL Server Audit
- audits [SQL Server], SQL Server Audit
ms.assetid: 0c1fca2e-f22b-4fe8-806f-c87806664f00
author: davidtrigano
ms.author: datrigan
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: f37e26803ebc57479d0c70dcd69dc951881c119a
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923923"
---
# <a name="sql-server-audit-database-engine"></a>Auditoria do SQL Server (Mecanismo de Banco de Dados)
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]

  A*auditoria* de uma instância do [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] ou de um banco de dados individual envolve o controle e o registro em log dos eventos que ocorrem no [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. A auditoria do[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] permite criar auditorias de servidor, que podem conter especificações de auditoria de servidor para eventos no nível de servidor, além de especificações de auditoria de banco de dados para eventos no nível de banco de dados. Os eventos auditados podem ser gravados nos logs de eventos ou nos arquivos de auditoria.  
  
[!INCLUDE[ssMIlimitation](../../../includes/sql-db-mi-limitation.md)]
  
 Dependendo dos requisitos ou padrões governamentais de sua instalação, ha vários níveis de auditoria no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. A auditoria do[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornece as ferramentas e os processos necessários para habilitar, armazenar e exibir auditorias em vários objetos de servidor e de banco de dados.  
  
 É possível gravar grupos de ação de auditoria de servidor por instância, e grupos de ação de auditoria de banco de dados ou ações de auditoria de banco de dados por banco de dados. O evento de auditoria ocorrerá sempre que a ação auditável for encontrada.  
  
 Todas as edições do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] oferecem suporte a auditorias no nível do servidor. Todas as edições oferecem suporte a auditorias no nível do banco de dados a partir do [!INCLUDE[ssSQL15_md](../../../includes/sssql15-md.md)] SP1. Antes disso, a auditoria no nível de banco de dados se limitava às edições Enterprise, Developer e Evaluation. Para obter mais informações, consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
> [!NOTE]  
>  Este tópico aplica-se ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  Para [!INCLUDE[ssSDS](../../../includes/sssds-md.md)], confira [Introdução à auditoria de banco de dados SQL](https://azure.microsoft.com/documentation/articles/sql-database-auditing-get-started/).  
  
## <a name="sql-server-audit-components"></a>Componentes de auditoria do SQL Server  
 *Auditoria* é a combinação de vários elementos em um único pacote de um grupo específico de ações de servidor ou de banco de dados. Os componentes de auditoria do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] são combinados para produzir uma saída conhecida como auditoria, da mesma forma como uma definição de relatório combinada com elementos gráficos e de dados produz um relatório.  
  
 A auditoria do[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa *Eventos Estendidos* para ajudar a criar uma auditoria. Para obter mais informações sobre Eventos Estendidos, consulte [Eventos Estendidos](../../../relational-databases/extended-events/extended-events.md).  
  
### <a name="sql-server-audit"></a>Auditoria do SQL Server  
 O objeto *Auditoria do SQL Server* coleta uma instância única de ações no nível do servidor e/ou do banco de dados e grupos de ações a serem monitoradas. A auditoria está no nível de instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Você pode ter várias auditorias por instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Ao definir uma auditoria, especifique o local de saída dos resultados. Esse é o destino da auditoria. A auditoria é criada em um estado *desabilitado* e não audita automaticamente nenhuma ação. Após a habilitação da auditoria, o destino da auditoria recebe dados da auditoria.  
  
### <a name="server-audit-specification"></a>Especificação da Auditoria do Servidor  
 O objeto *Especificação da Auditoria do Servidor* pertence a uma auditoria. É possível criar uma especificação de auditoria de servidor por auditoria, já que ambas são criadas no escopo da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 A especificação da auditoria do servidor coleta muitos grupos de ação no nível do servidor gerados pelo recurso Eventos Estendidos. É possível incluir *grupos de ação de auditoria* em uma especificação da auditoria do servidor. Os grupos de ação de auditoria são grupos de ações predefinidos, que são eventos atômicos que ocorrem no [!INCLUDE[ssDE](../../../includes/ssde-md.md)]. Essas ações são enviadas à auditoria, que por sua vez os registra no destino.  
  
 Grupos de ação de auditoria no nível do servidor são descritos no tópico [Ações e grupos de ações de auditoria do SQL Server](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
### <a name="database-audit-specification"></a>Especificação da Auditoria do Banco de Dados  
 O objeto *Especificação da Auditoria do Banco de Dados* também pertence à auditoria do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . É possível criar uma especificação da auditoria do banco de Dados por banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] por auditoria.  
  
 Uma especificação da auditoria do banco de dados coleciona ações de auditoria no nível do banco de dados geradas pelo recurso Eventos Estendidos. É possível adicionar grupos de ações de auditoria ou de eventos de auditoria a uma especificação da auditoria do banco de dados. *Eventos de auditoria* são ações atômicas que podem ser examinadas pelo mecanismo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . *Grupos de ação de auditoria* são grupos de ações predefinidos. Ambos estão no escopo do banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Essas ações são enviadas à auditoria, que por sua vez os registra no destino. Não inclua objetos do escopo de servidor, como as exibições do sistema, em uma especificação de auditoria de banco de dados do usuário.  
  
 Grupos de ação de auditoria no nível do banco de dados e ações de auditoria são descritos no tópico [Ações e grupos de ações de auditoria do SQL Server](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md).  
  
### <a name="target"></a>Destino  
 Os resultados de uma auditoria são enviados a um destino que pode ser um arquivo, o log de eventos de Segurança do Windows ou o log de eventos de Aplicativo do Windows. É necessário verificar e arquivar os logs periodicamente para certificar-se de que o destino tenha espaço suficiente para gravar mais registros.  
  
> [!IMPORTANT]  
>  Qualquer usuário autenticado pode fazer a leitura ou gravação no log de eventos de Aplicativo do Windows. O log de eventos de Aplicativo requer menos permissões que o log de eventos de Segurança do Windows e é menos seguro.  
  
 Gravar no log de Segurança do Windows exige que a conta de serviço do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] seja adicionada à política **Gerar auditorias de segurança** . Por padrão, Sistema Local, Serviço Local e Serviço de Rede fazem parte dessa política. Esta configuração pode ser definida com o uso do snap-in de política de segurança (secpol.msc). Além disso, é necessário habilitar a política de segurança **Auditar acesso ao objeto** para **Êxito** e **Falha**. Esta configuração pode ser definida com o uso do snap-in de política de segurança (secpol.msc). No [!INCLUDE[wiprlhext](../../../includes/wiprlhext-md.md)] ou no Windows Server 2008, é possível definir a política mais detalhada de **aplicativo gerado** na linha de comando usando o programa de política de auditoria (**AuditPol.exe)** . Para obter mais informações sobre as etapas para habilitar a gravação no log de Segurança do Windows, consulte [Gravar eventos de auditoria do SQL Server no log de segurança](../../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md). Para obter mais informações sobre o programa Auditpol.exe, consulte o artigo 921469 [How to use Group Policy to configure detailed security auditing](https://support.microsoft.com/kb/921469/)da Base de Dados de Conhecimento. Os logs de eventos do Windows são globais ao sistema operacional Windows. Para obter mais informações sobre os logs de eventos do Windows, consulte [Event Viewer Overview](https://go.microsoft.com/fwlink/?LinkId=101455). Se você precisar de permissões mais exatas na auditoria, use o destino de arquivo binário.  
  
 Quando você está salvando informações de auditoria em um arquivo, para ajudar a impedir falsificação, você pode restringir o acesso ao local do arquivo das seguintes maneiras:  
  
-   A Conta de Serviço [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve ter permissão de Leitura e Gravação.  
  
-   Os Administradores de Auditoria geralmente requerem permissão de Leitura e Gravação. Isso pressupõe que os Administradores de Auditoria sejam contas do Windows para a administração de arquivos de auditoria, por exemplo, copiando-os em compartilhamentos diferentes, armazenando-os em backup e assim por diante.  
  
-   Os Leitores de Auditoria que são autorizados a ler os arquivos de auditoria precisam ter permissão de Leitura.  
  
 Mesmo quando o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] estiver gravando em um arquivo, outros usuários do Windows poderão ler o arquivo de auditoria se tiverem permissão. O [!INCLUDE[ssDE](../../../includes/ssde-md.md)] não possui um bloqueio exclusivo que impeça operações de leitura.  
  
 Como o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] pode acessar o arquivo, os logons do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que tiverem a permissão do CONTROL SERVER poderão usar o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para acessar os arquivos de auditoria. Para registrar qualquer usuário que esteja lendo o arquivo de auditoria, defina uma auditoria em master.sys.fn_get_audit_file. Isso registra os logons com permissão CONTROL SERVER que acessaram o arquivo de auditoria por meio do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Se um Administrador de Auditoria copiar o arquivo em um local diferente (para fins de arquivamento, entre outros), as ACLs no novo local deverão ter apenas as seguintes permissões:  
  
-   Administrador de Auditoria – Leitura/Gravação  
  
-   Leitor de Auditoria – Leitura  
  
 É recomendável gerar relatórios de auditoria de uma instância separada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], como uma instância do [!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)], a qual apenas Administradores de Auditoria ou Leitores de Auditoria tenham acesso. Ao usar uma instância separada do [!INCLUDE[ssDE](../../../includes/ssde-md.md)] para relatório, você pode ajudar a impedir que usuários não autorizados obtenham acesso ao registro de auditoria.  
  
 Você pode oferecer proteção adicional contra acesso não autorizado criptografando a pasta na qual o arquivo de auditoria é armazenado usando Criptografia de Unidade de Windows BitLocker ou Sistema de Arquivo do Windows Encrypting.  
  
 Para obter mais informações sobre os registros de auditoria gravados no destino, consulte [SQL Server Audit Records](../../../relational-databases/security/auditing/sql-server-audit-records.md).  
  
## <a name="overview-of-using-sql-server-audit"></a>Visão geral do uso de auditoria do SQL Server  
 É possível usar o [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../../includes/tsql-md.md)] para definir uma auditoria. Após a criação e habilitação da auditoria, o destino receberá entradas.  
  
 É possível ler os logs de eventos do Windows usando o utilitário **Visualizador de Eventos** do Windows. Para destinos de arquivo, é possível usar o **Visualizador do Arquivo de Log** no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou a função [fn_get_audit_file](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md) para ler o arquivo de destino.  
  
 O processo geral para criar e usar uma auditoria do é o seguinte.  
  
1.  Crie uma auditoria e defina o destino.  
  
2.  Crie uma especificação da auditoria do servidor ou especificação da auditoria do banco de dados que mapeie para a auditoria. Habilite a especificação de auditoria.  
  
3.  Habilite a auditoria.  
  
4.  Leia os eventos de auditoria usando o recurso **Visualizador de Eventos**do Windows, o **Visualizador do Arquivo de Log**ou a função fn_get_audit_file.  

 Para obter mais informações, consulte [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md) e [Criar uma especificação de auditoria de banco de dados e de servidor](../../../relational-databases/security/auditing/create-a-server-audit-and-database-audit-specification.md).  
  
## <a name="considerations"></a>Considerações  
 No caso de falha durante o início da auditoria, o servidor não será iniciado. Nesse caso, é possível iniciar o servidor usando a opção **-f** na linha de comando.  
  
 Quando uma falha na auditoria faz com que o servidor seja desligado ou não seja iniciado devido à especificação de ON_FAILURE=SHUTDOWN para a auditoria, o evento MSG_AUDIT_FORCED_SHUTDOWN é gravado no log. Como o desligamento ocorrerá quando configuração for encontrada pela primeira vez, o evento será gravado uma vez. Esse evento será gravado após a mensagem de falha da auditoria provocar o desligamento. Um administrador pode ignorar os desligamentos induzidos por auditoria iniciando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no modo de usuário único usando o sinalizador **-m**. Se você iniciar no modo de Usuário Único, desatualizará qualquer auditoria em que ON_FAILURE=SHUTDOWN estiver especificado para execução naquela sessão como ON_FAILURE=CONTINUE. Quando o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] for iniciado pelo sinalizador **-m**, a mensagem MSG_AUDIT_SHUTDOWN_BYPASSED será gravada no log de erros.  
  
 Para obter mais informações sobre as opções de inicialização do serviço, consulte [Opções de inicialização do serviço Mecanismo de Banco de Dados](../../../database-engine/configure-windows/database-engine-service-startup-options.md).  
  
### <a name="attaching-a-database-with-an-audit-defined"></a>Anexando um banco de dados a uma auditoria definida  
 Anexar um banco de dados que tenha uma especificação de auditoria e especifica um GUID inexistente ao servidor gerará uma especificação de auditoria *órfã* . Como não existe uma auditoria com um GUID correspondente na instância do servidor, nenhum evento de auditoria será gravado. Para corrigir isso, use o comando ALTER DATABASE AUDIT SPECIFICATION para conectar a especificação de auditoria órfã a uma auditoria de servidor existente. Ou use o comando CREATE SERVER AUDIT para criar uma nova auditoria de servidor com o GUID especificado.  
  
 É possível anexar um banco de dados que tenha uma especificação de auditoria definida a outra edição do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que não dê suporte à auditoria do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , como o [!INCLUDE[ssExpress](../../../includes/ssexpress-md.md)] , mas os eventos de auditoria não serão gravados.  
  
### <a name="database-mirroring-and-sql-server-audit"></a>Espelhamento de Banco de Dados e o SQL Server Audit  
 Um banco de dados com uma especificação de auditoria de banco de dados definida e que usa espelhamento de banco de dados incluirá a especificação de auditoria de banco de dados. Para funcionar corretamente na instância de SQL espelhada, é necessário configurar os seguintes itens:  
  
-   É necessário que o servidor espelho tenha uma auditoria com o mesmo GUID para habilitar a especificação de auditoria de banco de dados para gravar registros de auditoria. Isso pode ser configurado usando o comando CREATE AUDIT WITH GUID **=** _\<GUID from source Server Audit_>.  
  
-   Para destinos de arquivos binários, é necessário que a conta do serviço de servidor espelho tenha as permissões apropriadas onde a trilha de auditoria começou a ser gravada.  
  
-   Para destinos de log de eventos do Windows, a política de segurança no computador em que se encontra o servidor espelho deve permitir o acesso de conta de serviço ao log de eventos de aplicativo ou de segurança.  
  
### <a name="auditing-administrators"></a>Administradores de auditoria  
 Os membros da função de servidor fixa **sysadmin** são identificados como o usuário **dbo** em cada banco de dados. Para auditar as ações dos administradores, audite as ações do usuário **dbo** .  
  
## <a name="creating-and-managing-audits-with-transact-sql"></a>Criando e gerenciando auditorias com o Transact-SQL  
 É possível usar instruções DDL, funções e exibições de gerenciamento dinâmico e exibições do catálogo para implementar todos os aspectos da Auditoria do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
### <a name="data-definition-language-statements"></a>Instruções de linguagem de definição de dados  
 É possível usar as seguintes instruções DDL para criar, alterar e remover especificações de auditoria:  
  
|Instruções DDL|Descrição| 
|-|-|  
|[ALTER AUTHORIZATION](../../../t-sql/statements/alter-authorization-transact-sql.md)|Altera a propriedade de um protegível.|  
|[ALTER DATABASE AUDIT SPECIFICATION](../../../t-sql/statements/alter-database-audit-specification-transact-sql.md)|Altera o objeto de especificação de auditoria do banco de dados usando o recurso Auditoria do SQL Server.|  
|[ALTERAR AUDITORIA DE SERVIDOR](../../../t-sql/statements/alter-server-audit-transact-sql.md)|Altera um objeto de auditoria do servidor usando o recurso Auditoria do SQL Server.|  
|[ALTER SERVER AUDIT SPECIFICATION](../../../t-sql/statements/alter-server-audit-specification-transact-sql.md)|Altera o objeto de especificação de auditoria do servidor usando o recurso Auditoria do SQL Server.|  
|[CREATE DATABASE AUDIT SPECIFICATION](../../../t-sql/statements/create-database-audit-specification-transact-sql.md)|Cria um objeto de especificação de auditoria do banco de dados usando o recurso de auditoria do SQL Server.|  
|[CRIAR AUDITORIA DE SERVIDOR](../../../t-sql/statements/create-server-audit-transact-sql.md)|Cria um objeto de auditoria do servidor usando a Auditoria do SQL Server.|  
|[CREATE SERVER AUDIT SPECIFICATION](../../../t-sql/statements/create-server-audit-specification-transact-sql.md)|Cria um objeto de especificação de auditoria do servidor usando o recurso Auditoria do SQL Server.|  
|[DROP DATABASE AUDIT SPECIFICATION](../../../t-sql/statements/drop-database-audit-specification-transact-sql.md)|Descarta o objeto de especificação de auditoria do banco de dados usando o recurso Auditoria do SQL Server.|  
|[DROP SERVER AUDIT](../../../t-sql/statements/drop-server-audit-transact-sql.md)|Descarta um objeto de auditoria de servidor usando o recurso SQL Server Audit.|  
|[DROP SERVER AUDIT SPECIFICATION](../../../t-sql/statements/drop-server-audit-specification-transact-sql.md)|Descarta um objeto de especificação de auditoria do servidor usando o recurso Auditoria do SQL Server.|  
  
### <a name="dynamic-views-and-functions"></a>Exibições e funções dinâmicas  
 A tabela a seguir lista as exibições e funções dinâmicas que podem ser usadas na auditoria do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
|Exibições e funções dinâmicas|Descrição|  
|---------------------------------|-----------------|  
|[sys.dm_audit_actions](../../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)|Retorna uma linha para cada ação de auditoria que pode ser reportada no log de auditoria e para cada grupo de ação de auditoria que pode ser configurado como parte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Audit.|  
|[sys.dm_server_audit_status](../../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)|Fornece informações sobre o estado atual da auditoria.|  
|[sys.dm_audit_class_type_map](../../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)|Retorna uma tabela que mapeia o campo class_type do log de auditoria para o campo class_desc em sys.dm_audit_actions.|  
|[fn_get_audit_file](../../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)|Retorna informações de um arquivo de auditoria criado por uma auditoria de servidor.|  
  
### <a name="catalog-views"></a>Exibições do catálogo  
 A tabela a seguir lista as exibições do catálogo que podem ser usadas para auditoria do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
|Exibições do catálogo|Descrição|  
|-------------------|-----------------|  
|[sys.database_audit_specifications](../../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)|Contém informações sobre as especificações de auditoria do banco de dados de uma auditoria do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em uma instância de servidor.|  
|[sys.database_audit_specification_details](../../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)|Contém informações sobre as especificações de auditoria de banco de dados em uma auditoria do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em uma instância de servidor para todos os bancos de dados.|  
|[sys.server_audits](../../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)|Contém uma linha para cada auditoria do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em uma instância de servidor.|  
|[sys.server_audit_specifications](../../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)|Contém informações sobre as especificações de auditoria do servidor em uma auditoria do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em uma instância do servidor.|  
|[sys.server_audit_specifications_details](../../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)|Contém informações sobre os detalhes (ações) de especificação de auditoria de servidor em uma auditoria do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em uma instância de servidor.|  
|[sys.server_file_audits](../../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)|Contém informações estendidas de repositórios sobre o tipo de auditoria de arquivo em uma auditoria do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , em uma instância do servidor.|  
  
## <a name="permissions"></a>Permissões  
 Cada recurso e comando de Auditoria do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tem requisitos de permissão individuais.  
  
 Para criar, alterar ou descartar uma Auditoria de Servidor ou uma Especificação de Auditoria de Servidor, as entidades de segurança exigem a permissão ALTER ANY SERVER AUDIT ou a permissão CONTROL SERVER. Para criar, alterar ou descartar uma Especificação de Auditoria de Banco de Dados, as entidades de segurança de banco de dados exigem a permissão DATABASE AUDIT ou ALTER ou CONTROL no banco de dados. Além disso, as entidades de segurança devem ter permissão para se conectar ao banco de dados ou à permissão ALTER ANY SERVER AUDIT ou CONTROL SERVER.  
  
 A permissão VIEW ANY DEFINITION fornece acesso para exibir os modos de exibição de auditoria no nível de servidor e VIEW DEFINITION fornece acesso para exibir os modos de exibição de auditoria no nível de banco de dados. A negação dessas permissões substitui a capacidade de exibir os modos de exibição de catálogo, mesmo que a entidade de segurança tenha as permissões ALTER ANY SERVER AUDIT ou ALTER ANY DATABASE AUDIT.  
  
 Para obter mais informações sobre como conceder direitos e permissões, consulte [GRANT &#40;Transact-SQL&#41;](../../../t-sql/statements/grant-transact-sql.md).  
  
> [!CAUTION]  
>  Entidades na função sysadmin podem violar qualquer componente de auditoria e aqueles na função db_owner podem violar quaisquer especificações em um banco de dados. A auditoria do[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] valida esse logon que cria ou altera uma especificação de auditoria que tenha pelo menos a permissão ALTER ANY DATABASE AUDIT. No entanto, ela não faz nenhuma validação quando você anexa um banco de dados. Você deve considerar que todas as Especificações de Auditoria de Banco de Dados são seguras somente para as entidades nas funções sysadmin ou db_owner.  
  
## <a name="related-tasks"></a>Related Tasks  
 [Criar uma auditoria de servidor e uma especificação de auditoria de servidor](../../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
 [Criar uma especificação de auditoria de banco de dados e de servidor](../../../relational-databases/security/auditing/create-a-server-audit-and-database-audit-specification.md)  
  
 [Exibir um log auditoria do SQL Server](../../../relational-databases/security/auditing/view-a-sql-server-audit-log.md)  
  
 [Gravar eventos de auditoria do SQL Server no log de segurança](../../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md)  
  
## <a name="topics-closely-related-to-auditing"></a>Tópicos estreitamente relacionados à auditoria  
 [Propriedades do Servidor &#40;Página Segurança&#41;](../../../database-engine/configure-windows/server-properties-security-page.md)  
 Explica como ativar a auditoria de logon para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os registros de auditoria são armazenados no log do aplicativo do Windows.  
  
 [Opção de configuração do servidor do modo de auditoria de c2](../../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md)  
 Explica o modo de auditoria de conformidade de segurança de C2 no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 [Categoria de evento de Auditoria de Segurança &#40;SQL Server Profiler&#41;](../../../relational-databases/event-classes/security-audit-event-category-sql-server-profiler.md)  
 Explica os eventos de auditoria que podem ser usados no [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]. Para saber mais, confira [SQL Server Profiler](../../../tools/sql-server-profiler/sql-server-profiler.md).  
  
 [Rastreamento do SQL](../../../relational-databases/sql-trace/sql-trace.md)  
 Explica como o Rastreamento do SQL pode ser usado nos seus próprios aplicativos para criar rastreamentos manualmente em vez de usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Profiler.  
  
 [Gatilhos DDL](../../../relational-databases/triggers/ddl-triggers.md)  
 Explica como os gatilhos DDL (linguagem de definição de dados) podem ser usados para controlar alterações nos bancos de dados.  
  
 [Microsoft TechNet: SQL Server TechCenter: Proteção e Segurança do SQL Server 2005](https://go.microsoft.com/fwlink/?LinkId=101152)  
 Fornece informações atualizadas sobre a segurança do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte Também  
 [Ações e grupos de ações de auditoria do SQL Server](../../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)   
 [Registros de auditoria do SQL Server](../../../relational-databases/security/auditing/sql-server-audit-records.md)  
  
  

