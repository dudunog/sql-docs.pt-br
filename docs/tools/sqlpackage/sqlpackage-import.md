---
title: Importação do SqlPackage
description: Saiba como automatizar tarefas de desenvolvimento de banco de dados com a ação Import do SqlPackage.exe. Veja exemplos e parâmetros, propriedades e variáveis SQLCMD disponíveis.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 198198e2-7cf4-4a21-bda4-51b36cb4284b
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan; sstein
ms.date: 12/11/2020
ms.openlocfilehash: 0e9acab737de04b002debf9d8c1b230a5cb01b14
ms.sourcegitcommit: 866554663ca3191748b6e4eb4d8d82fa58c4e426
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97577776"
---
# <a name="sqlpackage-import-parameters-and-properties"></a>Propriedades e parâmetros da ação Import do SqlPackage
A ação Import do SqlPackage.exe importa os dados do esquema e da tabela de um pacote BACPAC (arquivo .bacpac) para um banco de dados novo ou vazio no SQL Server ou no Banco de Dados SQL do Azure. No momento da operação de importação para um banco de dados existente, o banco de dados de destino não pode conter nenhum objeto de esquema definido pelo usuário.  

## <a name="command-line-syntax"></a>Sintaxe da linha de comando

O **SqlPackage.exe** inicia as ações especificadas usando os parâmetros, as propriedades e as variáveis SQLCMD especificados na linha de comando.  
  
```bash
SqlPackage {parameters}{properties}{SQLCMD Variables}  
```

## <a name="parameters-for-the-import-action"></a>Parâmetros da ação Import

|Parâmetro|Forma abreviada|Valor|Descrição|
|---|---|---|---|
|**/Action:**|**/a**|Importar|Especifica a ação a ser executada. |
|**/AccessToken:**|**/at**|{string}| Especifica o token de acesso da autenticação com base em token a ser utilizado quando se conectar ao banco de dados de destino. |
|**/Diagnostics:**|**/d**|{True&#124;False}|Especifica se o log de diagnósticos é emitido como saída para o console. Usa False como padrão. |
|**/DiagnosticsFile:**|**/df**|{string}|Especifica um arquivo para armazenar logs de diagnóstico. |
|**/MaxParallelism:**|**/mp**|{int}| Especifica o grau de paralelismo para operações simultâneas que são executadas em um banco de dados. O valor padrão é 8. |
|**/Properties:**|**/p**|{PropertyName}={Value}|Especifica um par nome-valor para uma propriedade específica da ação;{NomeDaPropriedade}={Valor}. Consulte a ajuda para obter uma ação específica para ver os nomes das propriedades dessa ação. Exemplo: sqlpackage.exe /Action:Import /?.|
|**/Quiet:**|**/q**|{True&#124;False}|Especifica se os comentários detalhados serão suprimidos. Usa False como padrão.|
|**/SourceFile:**|**/sf**|{string}|Especifica um arquivo de origem a ser usado como a origem da ação. Se esse parâmetro for usado, nenhum outro parâmetro de origem deverá ser válido. |
|**/TargetConnectionString:**|**/tcs**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de destino. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de destino. |
|**/TargetDatabaseName:**|**/tdn**|{string}|Especifica uma substituição do nome do banco de dados que é o destino da Ação sqlpackage.exe. |
|**/TargetEncryptConnection:**|**/tec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão de banco de dados de destino. |
|**/TargetPassword:**|**/tp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de destino. |
|**/TargetServerName:**|**/tsn**|{string}|Define o nome do servidor que hospeda o banco de dados de destino. |
|**/TargetTimeout:**|**/tt**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de destino em segundos. No Azure AD, recomendamos que esse valor seja maior ou igual a 30 segundos.|
|**/TargetTrustServerCertificate:**|**/ttsc**|{True&#124;False}|Especifica se o protocolo TLS será usado para criptografar a conexão de banco de dados de destino e ignorar a verificação da cadeia de certificados para validar a confiança. |
|**/TargetUser:**|**/tu**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de destino. |
|**/TenantId:**|**/tid**|{string}|Representa o nome de domínio ou a ID do locatário do Azure AD. Essa opção é necessária para dar suporte a usuários convidados ou importados do Azure AD e a contas Microsoft, como outlook.com, hotmail.com ou live.com. Se esse parâmetro for omitido, a ID de locatário padrão do Azure AD será usada, supondo que o usuário autenticado seja um usuário nativo desse AD. No entanto, nesse caso, não há suporte para usuários convidados ou importados e/ou contas da Microsoft hospedadas nesse Azure AD, e a operação falhará. <br/> Para saber mais sobre autenticação universal do Active Directory, confira [Autenticação universal com Banco de Dados SQL e Azure Synapse Analytics (suporte do SSMS para MFA)](/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|Especifica se a autenticação universal deve ser usada. Quando definido como True, o protocolo de autenticação interativo é ativado para dar suporte a MFA (autenticação multifator). Essa opção também pode ser usada para autenticação do Azure AD sem MFA, usando um protocolo interativo que exige que o usuário digite seu nome de usuário e senha ou autenticação integrada (credenciais do Windows). Quando /UniversalAuthentication está definido como True, nenhuma autenticação do Azure AD pode ser especificada em SourceConnectionString (/scs). Quando /UniversalAuthentication está definido como False, a autenticação do Azure AD deve ser especificada em SourceConnectionString (/scs). <br/> Para saber mais sobre autenticação universal do Active Directory, confira [Autenticação universal com Banco de Dados SQL e Azure Synapse Analytics (suporte do SSMS para MFA)](/azure/sql-database/sql-database-ssms-mfa-authentication).|

## <a name="properties-specific-to-the-import-action"></a>Propriedades específicas da ação Import

|Propriedade|Valor|Descrição|
|---|---|---|
|**/p:**|CommandTimeout=(INT32 '60')|Especifica o tempo limite do comando em segundos ao executar consultas com relação ao SQL Server.|
|**/p:**|DatabaseEdition=({Basic&#124;Standard&#124;Premium&#124;DataWarehouse&#124;GeneralPurpose&#124;BusinessCritical&#124;Hyperscale&#124;Default} 'Default')|Define a edição de um Banco de Dados SQL do Azure.|
|**/p:**|DatabaseLockTimeout=(INT32 '60')| Especifica o tempo limite de bloqueio do banco de dados em segundos ao executar consultas em SQL Server. Use -1 para esperar indefinidamente.|
|**/p:**|DatabaseMaximumSize=(INT32)|Define o tamanho máximo, em GB, de um Banco de Dados SQL do Azure.|
|**/p:**|DatabaseServiceObjective=(STRING)|Define o nível de desempenho de um Banco de Dados SQL do Azure, como "P0" ou "S1".|
|**/p:**|ImportContributorArguments=(STRING)|Especifica argumentos de colaborador de implantação para os colaboradores de implantação. Eles devem ser em formato de lista de valores delimitada por ponto e vírgula.|
|**/p:**|ImportContributors=(STRING)|Especifica que colaboradores da implantação devem ser executados quando o bacpac for importado. Ele deve ser em formato de lista delimitada por ponto e vírgula com os IDs ou nomes totalmente qualificados do colaborador de compilação.|
|**/p:**|ImportContributorPaths=(STRING)|Especifica caminhos para carregar colaboradores de implantação adicionais. Eles devem ser em formato de lista de valores delimitada por ponto e vírgula. |
|**/p:**|LongRunningCommandTimeout=(INT32)| Especifica o tempo limite do comando de execução prolongada em segundos ao executar consultas com relação ao SQL Server. Use 0 para esperar indefinidamente.|
|**/p:**|Storage=({File&#124;Memory})|Especifica como os elementos são armazenados ao criar o modelo de banco de dados. Por razões de desempenho, o padrão é InMemory. Para bancos de dados grandes, é necessário realizar armazenamento de backup de arquivos.|
  

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre o [sqlpackage](sqlpackage.md)