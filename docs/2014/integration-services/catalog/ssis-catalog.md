---
title: Catálogo do SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 24bd987e-164a-48fd-b4f2-cbe16a3cd95e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d4657bf58a7160f075759a265fef883c92fee0c9
ms.sourcegitcommit: 37a3e2c022c578fc3a54ebee66d9957ff7476922
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/07/2020
ms.locfileid: "82921711"
---
# <a name="ssis-catalog"></a>Catálogo do SSIS
  O `SSISDB` catálogo é o ponto central para trabalhar com [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] projetos do (SSIS) que você implantou no [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] servidor. Por exemplo, você define parâmetros de projeto e pacote, configura ambientes para especificar valores de runtime para pacotes, executa e soluciona problemas de pacotes, e gerencia as operações de servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Os objetos armazenados no `SSISDB` Catálogo incluem projetos, pacotes, parâmetros, ambientes e histórico operacional.  
  
 Você inspeciona objetos, configurações e dados operacionais que são armazenados no `SSISDB` catálogo, consultando as exibições no `SSISDB` banco de dados. Você gerencia os objetos chamando procedimentos armazenados no banco de `SSISDB` dados ou usando a interface do usuário do `SSISDB` catálogo. Em muitos casos, a mesma tarefa pode ser executada na interface de usuário ou chamando um procedimento armazenado.  
  
 Para manter o banco de dados `SSISDB`, é recomendado que você aplique políticas empresariais padrão para gerenciar os bancos de dados de usuários. Para obter informações sobre como criar planos de manutenção, consulte [Maintenance Plans](../../relational-databases/maintenance-plans/maintenance-plans.md).  
  
 O `SSISDB` catálogo e o `SSISDB` banco de dados dão suporte ao Windows PowerShell. Para obter mais informações sobre como usar o SQL Server com Windows PowerShell, consulte [SQL Server PowerShell](../../powershell/sql-server-powershell.md). Para obter exemplos de como usar o Windows PowerShell para concluir tarefas como implantar um projeto, consultar a entrada de blog, [SSIS e PowerShell no SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=242539)em blogs.msdn.com.  
  
 Para obter mais informações sobre como exibir dados de operações, consulte [monitorando execuções de pacote e outras operações](../performance/monitor-running-packages-and-other-operations.md).  
  
 Você acessa o `SSISDB` catálogo no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] conectando-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mecanismo de banco de dados e, em seguida, expandindo o nó **catálogos de Integration Services** no Pesquisador de objetos. Você acessa o `SSISDB` banco de dados no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] expandindo o nó Databases no Pesquisador de objetos.  
  
> [!NOTE]  
>  Você não pode renomear o `SSISDB` banco de dados.  
  
> [!NOTE]  
>  Se a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância à qual o `SSISDB` banco de dados está anexado, parar ou não responder, o processo ISServerExec. exe terminará. Uma mensagem é gravada em um log de Eventos do Windows.  
>   
>  Se os recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] realizarem failover como parte de um failover de cluster, os pacotes de execução não serão reiniciados. Você pode usar pontos de verificação para reiniciar pacotes. Para saber mais, confira [Restart Packages by Using Checkpoints](../packages/restart-packages-by-using-checkpoints.md).  
  
## <a name="catalog-object-identifiers"></a>Identificadores do objeto de catálogo  
 Quando você cria um novo objeto no catálogo, atribua um nome ao objeto. O nome do objeto é um identificador. O[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define regras que estabelecem que os caracteres podem ser usados em um identificador. Os nomes destes objetos devem seguir as regras de identificador.  
  
-   Pasta  
  
-   Project  
  
-   Ambiente  
  
-   Parâmetro  
  
-   Variável de ambiente  
  
### <a name="folder-project-environment"></a>Pasta, projeto, ambiente  
 Considere as seguintes regras ao renomear uma pasta, um projeto ou um ambiente.  
  
-   Os caracteres inválidos incluem caracteres ASCII/Unicode de 1 a 31, aspas ("), menor que (\<), maior que (>), barra vertical (|), Backspace (\b), nulo (\0) e Tab (\t).  
  
-   O nome não pode conter espaços à esquerda ou à direita.  
  
-   Não é permitido usar \@ como o primeiro caractere, mas \@ pode ser usado nos caracteres posteriores.  
  
-   O comprimento do nome deve ser maior ou igual a 0 e menor ou igual a 128.  
  
### <a name="parameter"></a>Parâmetro  
 Considere as seguintes regras ao nomear um parâmetro.  
  
-   O primeiro caractere do nome deve ser uma letra, conforme definido no Unicode Standard 2.0, ou um caractere de sublinhado (_).  
  
-   Os caracteres subsequentes podem ser letras ou números, conforme definido no Unicode Standard 2.0, ou um caractere de sublinhado (_).  
  
### <a name="environment-variable"></a>Variável de ambiente  
 Considere as seguintes regras ao nomear uma variável de ambiente.  
  
-   Os caracteres inválidos incluem caracteres ASCII/Unicode de 1 a 31, aspas ("), menor que (\<), maior que (>), barra vertical (|), Backspace (\b), nulo (\0) e Tab (\t).  
  
-   O nome não pode conter espaços à esquerda ou à direita.  
  
-   Não é permitido usar \@ como o primeiro caractere, mas \@ pode ser usado nos caracteres posteriores.  
  
-   O comprimento do nome deve ser maior ou igual a 0 e menor ou igual a 128.  
  
-   O primeiro caractere do nome deve ser uma letra, conforme definido no Unicode Standard 2.0, ou um caractere de sublinhado (_).  
  
-   Os caracteres subsequentes podem ser letras ou números, conforme definido no Unicode Standard 2.0, ou um caractere de sublinhado (_).  
  
## <a name="catalog-configuration"></a>Configuração do catálogo  
 Você ajusta como o catálogo se comporta ajustando as propriedades do catálogo. As propriedades do catálogo definem como os dados confidenciais serão criptografados, e como as operações e os dados de controle de versão de projeto serão retidos. Para definir as propriedades do catálogo, use a caixa de diálogo **Propriedades do Catálogo** ou chame o procedimento armazenado [catalog.configure_catalog &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database). Para exibir as propriedades, use a caixa de diálogo ou consulte [catalog.catalog_properties &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database). Acesse a caixa de diálogo clicando com o botão direito do mouse em `SSISDB` no Pesquisador de Objetos.  
  
### <a name="operations-and-project-version-cleanup"></a>Operações e limpeza de versão do projeto  
 Os dados de status de muitas operações no catálogo são armazenados nas tabelas de banco de dados internas. Por exemplo, o catálogo rastreia o status das execuções de pacote e das implantações de projeto. Para manter o tamanho dos dados de operações, o **Trabalho de Manutenção do Servidor SSIS** no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] é usado para remover dados antigos. Este trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent é criado quando [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é instalado.  
  
 Você pode atualizar ou reimplantar um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] implantando-o com o mesmo nome na mesma pasta do catálogo. Por padrão, cada vez que você reimplanta um projeto, o `SSISDB` Catálogo retém a versão anterior do projeto. Para manter o tamanho dos dados de operações, o **Trabalho de Manutenção do Servidor SSIS** é usado para remover versões antigas de projetos.  
  
 As propriedades do catálogo a seguir `SSISDB` definem como esse [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabalho do Agent se comporta. Você pode exibir e modificar as propriedades usando a caixa de diálogo **Propriedades do Catálogo** ou usando [catalog.catalog_properties &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database) e [catalog.configure_catalog &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database).  
  
 **Limpar Logs Periodicamente**  
 A etapa de trabalho para limpeza de operações é executada quando esta propriedade é definida como `True`.  
  
 **Período de Retenção (dias)**  
 Define a idade máxima dos dados de operações permitidos (em dias). Os dados mais antigos são removidos.  
  
 O valor mínimo é um dia. O valor máximo é limitado apenas pelo valor máximo dos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `int` dados. Para obter informações sobre esse tipo de dados, consulte [int, bigint, smallint e tinyint &#40;Transact-SQL&#41;](/sql/t-sql/data-types/int-bigint-smallint-and-tinyint-transact-sql).  
  
 **Remover Periodicamente Versões Antigas**  
 A etapa de trabalho para limpeza de versão de projeto é executada quando esta propriedade é definida como `True`.  
  
 **Número Máximo de Versões por Projeto**  
 Define quantas versões de um projeto são armazenadas no catálogo. As versões de projetos mais antigas são removidas.  
  
### <a name="encryption-algorithm"></a>Algoritmo de Criptografia  
 A propriedade **Algoritmo de Criptografia** especifica o tipo de criptografia usado para criptografar valores de parâmetro confidenciais. Você pode escolher entre os seguintes tipos de criptografia.  
  
-   AES_256 (padrão)  
  
-   AES_192  
  
-   AES_128  
  
-   DESX  
  
-   TRIPLE_DES_3KEY  
  
-   TRIPLE_DES  
  
-   DES  
  
 Quando você implantar um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para o servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], o catálogo criptografará automaticamente os dados do pacote e os valores confidenciais. O catálogo também descriptografa automaticamente os dados quando você recupera-os. O catálogo SSISDB usa o nível de proteção `ServerStorage`. Para obter mais informações, consulte [Access Control for Sensitive Data in Packages](../security/access-control-for-sensitive-data-in-packages.md).  
  
 Alterar o algoritmo de criptografia é uma operação demorada. Primeiro, o servidor tem que usar o algoritmo previamente especificado para descriptografar todos os valores de configuração. Em seguida, o servidor tem que usar o novo algoritmo para criptografar novamente os valores. Durante este momento, não pode haver outras operações do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no servidor. Assim, para permitir que operações do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] continuem ininterruptas, o algoritmo de criptografia deverá ser um valor somente leitura na caixa de diálogo no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 Para alterar a configuração de propriedade **algoritmo de criptografia** , defina o `SSISDB` banco de dados para o modo de usuário único e, em seguida, chame o procedimento armazenado Catalog. configure_catalog. Use ENCRYPTION_ALGORITHM para o argumento *property_name* . Para os valores de propriedade com suporte, consulte [catalog.catalog_properties &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-catalog-properties-ssisdb-database). Para obter mais informações sobre o procedimento armazenado, consulte [catalog.configure_catalog &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-configure-catalog-ssisdb-database).  
  
 Para obter mais informações sobre o modo de usuário único, veja [Definir um banco de dados como modo de usuário único](../../relational-databases/databases/set-a-database-to-single-user-mode.md). Para obter informações sobre criptografia e algoritmos de criptografia no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte os tópicos na seção [Criptografia do SQL Server](../../relational-databases/security/encryption/sql-server-encryption.md).  
  
 Uma chave mestra de banco de dados é usada para a criptografia. A chave é criada quando você cria o catálogo. Para obter mais informações, consulte [Criar o catálogo SSIS](ssis-catalog.md).  
  
 A tabela a seguir lista os nomes de propriedade mostrados na caixa de diálogo **Propriedades do Catálogo** e as propriedades correspondentes na exibição de banco de dados.  
  
|Nome da propriedade (caixa de diálogo**Propriedades do catálogo** )|Nome da Propriedade (exibição de banco de dados)|  
|---------------------------------------------------------|-------------------------------------|  
|Nome do Algoritmo de Criptografia|ENCRYPTION_ALGORITHM|  
|Limpar Logs Periodicamente|OPERATION_CLEANUP_ENABLED|  
|Período de Retenção (dias)|RETENTION_WINDOW|  
|Remover Periodicamente Versões Antigas|VERSION_CLEANUP_ENABLED|  
|Número Máximo de Versões por Projeto|MAX_PROJECT_VERSIONS|  
|Nível de Log Padrão em Todo o Servidor|SERVER_LOGGING_LEVEL|  
  
## <a name="permissions"></a>Permissões  
 Os projetos, ambientes e pacotes são armazenados em pastas, que são objetos protegíveis. Você pode conceder permissões a uma pasta, incluindo a permissão MANAGE_OBJECT_PERMISSIONS. MANAGE_OBJECT_PERMISSIONS permite delegar a administração do conteúdo da pasta a um usuário sem precisar conceder a associação do usuário à função ssis_admin. Você também pode conceder permissões para projetos, ambientes e operações. As operações incluem inicializar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , implantar projetos, criar e iniciar execuções, validar projetos e pacotes e configurar o `SSISDB` catálogo.  
  
 Para obter mais informações sobre as funções de banco de dados, veja [Funções no nível de banco de dados](../../relational-databases/security/authentication-access/database-level-roles.md).  
  
 O catálogo SSISDB usa um gatilho DDL, ddl_cleanup_object_permissions, para impor a integridade das informações de permissões para elementos protegíveis do SSIS. O gatilho é acionado quando uma entidade de segurança de banco de dados, como um usuário de banco de dados, função de banco de dados ou função de aplicativo de banco de dados, é removida do banco de dados SSISDB.  
  
 Se a entidade de segurança tiver concedido ou negado permissões a outras entidades de segurança, revogue as permissões dadas pelo concessor, para que a entidade de segurança possa ser removida. Caso contrário, uma mensagem de erro será retornada quando o sistema tentar remover a entidade de segurança. O gatilho removerá todos os registros de permissão em que a entidade de segurança de banco de dados é um usuário autorizado.  
  
 É recomendável que o gatilho não seja desabilitado porque garante que não haja registros de permissão órfãos depois que uma entidade de segurança do banco de dados for removida do `SSISDB` banco de dados.  
  
### <a name="managing-permissions"></a>Gerenciando permissões  
 Você pode gerenciar permissões usando a interface do usuário do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , procedimentos armazenados e o namespace <xref:Microsoft.SqlServer.Management.IntegrationServices> .  
  
 Para gerenciar permissões usando a interface de usuário do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , use as seguintes caixas de diálogo:  
  
-   Para uma pasta, use a página **Permissões** da [Folder Properties Dialog Box](folder-properties-dialog-box.md).  
  
-   Para um projeto, use a página **Permissões** na [Project Properties Dialog Box](project-properties-dialog-box.md).  
  
 Para gerenciar permissões usando o Transact-SQL, chame [catalog.grant_permission &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-grant-permission-ssisdb-database), [catalog.deny_permission &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-deny-permission-ssisdb-database) e [catalog.revoke_permission &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-revoke-permission-ssisdb-database). Para exibir permissões efetivas para a entidade de segurança atual para todos os objetos, consulte [catalog.effective_object_permissions &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-effective-object-permissions-ssisdb-database). Este tópico fornece descrições dos diferentes tipos de permissões. Para exibir as permissões atribuídas explicitamente ao usuário, consulte [catalog.explicit_object_permissions &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-explicit-object-permissions-ssisdb-database).  
  
## <a name="folders"></a>Pastas  
 Uma pasta contém um ou mais projetos e ambientes no `SSISDB` catálogo. Você pode usar a exibição [catalog.folders &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-folders-ssisdb-database) para acessar informações sobre pastas no catálogo. Você pode usar os procedimentos armazenados a seguir para gerenciar pastas.  
  
-   [catalog.create_folder &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-folder-ssisdb-database)  
  
-   [catalog.delete_folder &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-folder-ssisdb-database)  
  
-   [catalog.rename_folder &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-rename-folder-ssisdb-database)  
  
-   [catalog.set_folder_description &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-folder-description-ssisdb-database)  
  
## <a name="projects-and-packages"></a>Projetos e pacotes  
 Cada projeto pode conter vários pacotes. Os projetos e pacotes podem conter parâmetros e referências a ambientes. Você pode acessar os parâmetros e referências de ambiente usando a [Configure Dialog Box](configure-dialog-box.md).  
  
 Você pode executar outras tarefas de projeto chamando os seguintes procedimentos armazenados.  
  
-   [catalog.delete_project &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-project-ssisdb-database)  
  
-   [catalog.deploy_project &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-deploy-project-ssisdb-database)  
  
-   [catalog.get_project &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-get-project-ssisdb-database)  
  
-   [catalog.move_project &#40;&#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-move-project-ssisdb-database)  
  
-   [catalog.restore_project &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database)  
  
 Estas exibições fornecem detalhes sobre pacotes, projetos e versões de projeto.  
  
-   [catalog.projects &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-projects-ssisdb-database)  
  
-   [catalog.packages &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-packages-ssisdb-database)  
  
-   [catalog.object_versions &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-object-versions-ssisdb-database)  
  
## <a name="parameters"></a>Parâmetros  
 Use os parâmetros para atribuir valores às propriedades de pacote no tempo de execução do pacote. Para definir o valor de um pacote ou parâmetro de projeto e limpar o valor, chame [catalog.set_object_parameter_value &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database) e [catalog.clear_object_parameter_value &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database). Para definir o valor de um parâmetro para uma instância de execução, chame [catalog.set_execution_parameter_value &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database). Você pode recuperar valores de parâmetro padrão chamando [catalog.get_parameter_values &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-get-parameter-values-ssisdb-database).  
  
 Estas exibições mostram os parâmetros de todos os pacotes e projetos, e os valores de parâmetro usados para uma instância de execução.  
  
-   [catalog.object_parameters &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database)  
  
-   [catalog.execution_parameter_values &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-execution-parameter-values-ssisdb-database)  
  
## <a name="server-environments-server-variables-and-server-environment-references"></a>Ambientes de servidor, variáveis de servidor e referências de ambiente de servidor  
 Os ambientes de servidor contêm variáveis de servidor. Os valores variáveis podem ser usados quando um pacote é executado ou validado no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 Os procedimentos armazenados a seguir permitem executar muitas outras tarefas de gerenciamento para ambientes e variáveis.  
  
-   [catalog.create_environment &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-environment-ssisdb-database)  
  
-   [catalog.delete_environment &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-environment-ssisdb-database)  
  
-   [catalog.move_environment &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-move-environment-ssisdb-database)  
  
-   [catalog.rename_environment &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-rename-environment-ssisdb-database)  
  
-   [catalog.set_environment_property &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-property-ssisdb-database)  
  
-   [catalog.create_environment_variable &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-environment-variable-ssisdb-database)  
  
-   [catalog.delete_environment_variable &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-environment-variable-ssisdb-database)  
  
-   [catalog.set_environment_variable_property &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-variable-property-ssisdb-database)  
  
-   [catalog.set_environment_variable_value &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-variable-value-ssisdb-database)  
  
 Ao chamar o procedimento armazenado [catalog.set_environment_variable_protection &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-variable-protection-ssisdb-database), você pode definir o bit de sensibilidade de uma variável.  
  
 Para usar o valor de uma variável de servidor, especifique a referência entre o projeto e o ambiente de servidor. Você pode usar os procedimentos armazenados para criar e excluir referências. Você também pode indicar se o ambiente pode estar localizado na mesma pasta que o projeto ou em uma pasta diferente.  
  
-   [catalog.create_environment_reference &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-environment-reference-ssisdb-database)  
  
-   [catalog.delete_environment_reference &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-delete-environment-reference-ssisdb-database)  
  
-   [catalog.set_environment_reference_type &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-environment-reference-type-ssisdb-database)  
  
 Para obter mais detalhes sobre ambientes e variáveis, consulte estas exibições.  
  
-   [catalog.environments &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-environments-ssisdb-database)  
  
-   [catalog.environment_variables &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-environment-variables-ssisdb-database)  
  
-   [catalog.environment_references &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-environment-references-ssisdb-database)  
  
## <a name="executions-and-validations"></a>Execuções e validações  
 Uma execução é uma instância de uma execução de pacote. Chame [catalog.create_execution &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database) e [catalog.start_execution &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database) para criar e iniciar uma execução. Para interromper a execução ou uma validação de pacote/projeto, chame [catalog.stop_operation &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database).  
  
 Para fazer com que um pacote em execução pause ou crie um arquivo de despejo, chame o procedimento armazenado catalog.create_execution_dump. Um arquivo de despejo fornece informações sobre a execução de um pacote que pode ajudar a solucionar problemas de execução. Para obter mais informações sobre como gerar e configurar arquivos de despejo, consulte [Generating Dump Files for Package Execution](../troubleshooting/generating-dump-files-for-package-execution.md).  
  
 Para obter detalhes sobre execuções, validações, mensagens que são registradas em log durante operações, e informações contextuais relacionadas a erros, consulte estas exibições.  
  
-   [catalog.executions &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database)  
  
-   [catalog.operations &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database)  
  
-   [catalog.operation_messages &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-operation-messages-ssisdb-database)  
  
-   [catalog.extended_operation_info &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-views/catalog-extended-operation-info-ssisdb-database)  
  
-   [catalog.event_messages](/sql/integration-services/system-views/catalog-event-messages)  
  
-   [catalog.event_message_context](/sql/integration-services/system-views/catalog-event-message-context)  
  
 Você pode validar projetos e pacotes chamando os procedimentos armazenados [catalog.validate_project &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-validate-project-ssisdb-database) e [catalog.validate_package &#40;Banco de dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-validate-package-ssisdb-database). A exibição [catalog.validations &amp;#40;Banco de dados SSISDB&amp;#41;](/sql/integration-services/system-views/catalog-validations-ssisdb-database) fornece detalhes sobre validações, como as referências de ambiente de servidor consideradas na validação, se é uma validação de dependência ou uma validação completa e se o runtime de 32 ou 64 bits é usado para executar o pacote.  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Criar o catálogo do SSIS](ssis-catalog.md)  
  
-   [Fazer backup, restaurar e mover o catálogo do SSIS](../backup-restore-and-move-the-ssis-catalog.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Entrada de blog, [SSIS e PowerShell no SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=242539), em blogs.msdn.com.  
  
-   Entrada de blog, [Digas de controle de acesso ao catálogo do SSIS](https://go.microsoft.com/fwlink/?LinkId=246669), em blogs.msdn.com.  
  
-   Entrada do blog [Prévia do modelo do objeto gerenciado do catálogo do SSIS](https://techcommunity.microsoft.com/t5/sql-server-integration-services/a-glimpse-of-the-ssis-catalog-managed-object-model/ba-p/387892)em blogs.msdn.com.  
  
  
