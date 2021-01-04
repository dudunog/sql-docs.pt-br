---
title: Exportação do SqlPackage
description: Saiba como automatizar tarefas de desenvolvimento de banco de dados com a ação Export do SqlPackage.exe. Veja exemplos e parâmetros, propriedades e variáveis SQLCMD disponíveis.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 198198e2-7cf4-4a21-bda4-51b36cb4284b
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan; sstein
ms.date: 12/11/2020
ms.openlocfilehash: c0c3b1462fe165678e3826585f5ce82d5945de56
ms.sourcegitcommit: 866554663ca3191748b6e4eb4d8d82fa58c4e426
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97577778"
---
# <a name="sqlpackage-export-parameters-and-properties"></a>Propriedades e parâmetros da ação Export do SqlPackage
A ação Export do SqlPackage.exe exporta um banco de dados ativo do SQL Server ou do SQL do Azure para um pacote BACPAC (arquivo .bacpac). Por padrão, os dados de todas as tabelas serão incluídos no arquivo .bacpac. Como opção, você pode especificar apenas um subconjunto das tabelas para o qual exportará dados. A validação para a ação Exportar garante a compatibilidade do Banco de Dados SQL do Azure para o banco de dados de destino completo, mesmo que esteja especificado um subconjunto das tabelas para a exportação. 

## <a name="command-line-syntax"></a>Sintaxe da linha de comando

O **SqlPackage.exe** inicia as ações especificadas usando os parâmetros, as propriedades e as variáveis SQLCMD especificados na linha de comando.  
  
```bash
SqlPackage {parameters}{properties}{SQLCMD Variables}  
```

## <a name="parameters-for-the-export-action"></a>Parâmetros da ação Export

|Parâmetro|Forma abreviada|Valor|Descrição|
|---|---|---|---|
|**/Action:**|**/a**|Exportação|Especifica a ação a ser executada. |
|**/AccessToken:**|**/at**|{string}| Especifica o token de acesso da autenticação com base em token a ser utilizado quando se conectar ao banco de dados de destino. |
|**/Diagnostics:**|**/d**|{True&#124;False}|Especifica se o log de diagnósticos é emitido como saída para o console. Usa False como padrão. |
|**/DiagnosticsFile:**|**/df**|{string}|Especifica um arquivo para armazenar logs de diagnóstico. |
|**/MaxParallelism:**|**/mp**|{int}| Especifica o grau de paralelismo para operações simultâneas que são executadas em um banco de dados. O valor padrão é 8. |
|**/OverwriteFiles:**|**/of**|{True&#124;False}|Especifica se sqlpackage.exe deverá sobrescrever os arquivos existentes. Especificar false fará com que sqlpackage.exe anule a ação se um arquivo existente for encontrado. O valor padrão é True. |
|**/Properties:**|**/p**|{PropertyName}={Value}|Especifica um par nome-valor para uma propriedade específica da ação;{NomeDaPropriedade}={Valor}. Consulte a ajuda para obter uma ação específica para ver os nomes das propriedades dessa ação. Exemplo: sqlpackage.exe /Action:Export /?.|
|**/Quiet:**|**/q**|{True&#124;False}|Especifica se os comentários detalhados serão suprimidos. Usa False como padrão.|
|**/SourceConnectionString:**|**/scs**|{string}|Especifica uma cadeia de conexão válida do SQL Server/SQL Azure para o banco de dados de origem. Se esse parâmetro for especificado, ele deverá ser usado exclusivamente entre todos os outros parâmetros de origem. |
|**/SourceDatabaseName:**|**/sdn**|{string}|Define o nome do banco de dados de origem. |
|**/SourceEncryptConnection:**|**/sec**|{True&#124;False}|Especifica se a criptografia SQL deve ser usada para a conexão do banco de dados de origem. |
|**/SourcePassword:**|**/sp**|{string}|Para cenários de autenticação do SQL Server, define a senha a ser usada para acessar o banco de dados de origem. |
|**/SourceServerName:**|**/ssn**|{string}|Define o nome do servidor que hospeda o banco de dados de origem. |
|**/SourceTimeout:**|**/st**|{int}|Especifica o tempo limite para estabelecer uma conexão com o banco de dados de origem em segundos. |
|**/SourceTrustServerCertificate:**|**/stsc**|{True&#124;False}|Especifica se o protocolo TLS será usado para criptografar a conexão de banco de dados de origem e ignorar a verificação da cadeia de certificados para validar a confiança. |
|**/SourceUser:**|**/su**|{string}|Para cenários de autenticação do SQL Server, define o usuário do SQL Server a ser utilizado para acessar o banco de dados de origem. |
|**/TargetFile:**|**/tf**|{string}| Especifica um arquivo de destino (ou seja, um arquivo .dacpac) a ser usado como destino da ação em vez de um banco de dados. Se esse parâmetro for usado, nenhum outro parâmetro de destino será válido. Esse parâmetro será inválido para ações que dão suporte apenas a destinos de banco de dados.|
|**/TenantId:**|**/tid**|{string}|Representa o nome de domínio ou a ID do locatário do Azure AD. Essa opção é necessária para dar suporte a usuários convidados ou importados do Azure AD e a contas Microsoft, como outlook.com, hotmail.com ou live.com. Se esse parâmetro for omitido, a ID de locatário padrão do Azure AD será usada, supondo que o usuário autenticado seja um usuário nativo desse AD. No entanto, nesse caso, não há suporte para usuários convidados ou importados e/ou contas da Microsoft hospedadas nesse Azure AD, e a operação falhará. <br/> Para saber mais sobre autenticação universal do Active Directory, confira [Autenticação universal com Banco de Dados SQL e Azure Synapse Analytics (suporte do SSMS para MFA)](/azure/sql-database/sql-database-ssms-mfa-authentication).|
|**/UniversalAuthentication:**|**/ua**|{True&#124;False}|Especifica se a autenticação universal deve ser usada. Quando definido como True, o protocolo de autenticação interativo é ativado para dar suporte a MFA (autenticação multifator). Essa opção também pode ser usada para autenticação do Azure AD sem MFA, usando um protocolo interativo que exige que o usuário digite seu nome de usuário e senha ou autenticação integrada (credenciais do Windows). Quando /UniversalAuthentication está definido como True, nenhuma autenticação do Azure AD pode ser especificada em SourceConnectionString (/scs). Quando /UniversalAuthentication está definido como False, a autenticação do Azure AD deve ser especificada em SourceConnectionString (/scs). <br/> Para saber mais sobre autenticação universal do Active Directory, confira [Autenticação universal com Banco de Dados SQL e Azure Synapse Analytics (suporte do SSMS para MFA)](/azure/sql-database/sql-database-ssms-mfa-authentication).|

## <a name="properties-specific-to-the-export-action"></a>Propriedades específicas da ação Exportar

|Propriedade|Valor|Descrição|
|---|---|---|
|**/p:**|CommandTimeout=(INT32 '60')|Especifica o tempo limite do comando em segundos ao executar consultas com relação ao SQL Server.|
|**/p:**|DatabaseLockTimeout=(INT32 '60')| Especifica o tempo limite de bloqueio do banco de dados em segundos ao executar consultas em SQL Server. Use -1 para esperar indefinidamente.|
|**/p:**|LongRunningCommandTimeout=(INT32)| Especifica o tempo limite do comando de execução prolongada em segundos ao executar consultas com relação ao SQL Server. Use 0 para esperar indefinidamente.|
|**/p:**|Storage=({File&#124;Memory} 'File')|Especifica o tipo de armazenamento de backup para o modelo de esquema usado durante a extração.|
|**/p:**|TableData=(STRING)|Indica a tabela a partir da qual os dados serão extraídos. Especifique o nome da tabela com ou sem os colchetes ao redor das partes do nome no seguinte formato: nome_esquema.identificador_tabela. Essa opção pode ser especificada várias vezes.|
|**/p:**|TempDirectoryForTableData=(STRING)|Especifica o diretório temporário usado para armazenar em buffer os dados da tabela antes de serem gravados no arquivo do pacote.|
|**/p:**|TargetEngineVersion=({Default&#124;Latest&#124;V11&#124;V12} 'Latest')|Especifica qual é a versão esperada do mecanismo de destino. Isso afeta se os objetos que têm suporte dos servidores de Banco de Dados SQL do Azure com recursos da V12, como tabelas com otimização de memória, são permitidos no bacpac gerado.|
|**/p:**|VerifyFullTextDocumentTypesSupported=(BOOLEAN)|Especifica se os tipos de documento de texto completo compatíveis com o Banco de Dados SQL do Microsoft Azure versão 12 devem ser verificados.|

## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre o [sqlpackage](sqlpackage.md)