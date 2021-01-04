---
title: SqlPackage.exe
description: Saiba como automatizar tarefas de desenvolvimento de banco de dados com SqlPackage.exe. Veja exemplos e parâmetros, propriedades e variáveis SQLCMD disponíveis.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: 198198e2-7cf4-4a21-bda4-51b36cb4284b
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan; sstein
ms.date: 11/4/2020
ms.openlocfilehash: 16c4200b70647c08ddee6b531acc3227d2942ad2
ms.sourcegitcommit: 866554663ca3191748b6e4eb4d8d82fa58c4e426
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97577772"
---
# <a name="sqlpackageexe"></a>SqlPackage.exe

O **SqlPackage.exe** é um utilitário de linha de comando que automatiza as seguintes tarefas de desenvolvimento de banco de dados:  
  
- [Versão](#version): retorna o número de build do aplicativo SqlPackage.  Adicionada na versão 18.6.

- [Extrair](sqlpackage-extract.md): cria um arquivo (.dacpac) de instantâneo de um banco de dados do SQL Server dinâmico ou do Banco de Dados SQL do Azure.  
  
- [Publicar](sqlpackage-publish.md): atualiza um esquema de banco de dados incrementalmente para que corresponda ao esquema de um arquivo .dacpac de origem. Se o banco de dados não existir no servidor, a operação de publicação irá criá-lo. Caso contrário, um banco de dados existente é atualizado.  
  
- [Export](sqlpackage-export.md): exporta um banco de dados dinâmico – incluindo o esquema e os dados de usuário do banco de dados – do SQL Server ou do Banco de Dados SQL do Azure para um pacote BACPAC (arquivo .bacpac).  
  
- [Import](sqlpackage-import.md): importa os dados de esquema e tabela de um pacote BACPAC para um novo banco de dados do usuário em uma instância do SQL Server ou do Banco de Dados SQL do Azure.  
  
- [DeployReport](sqlpackage-deploy-drift-report.md): cria um relatório XML das alterações que teriam sido feitas por uma ação de publicação.  
  
- [DriftReport](sqlpackage-deploy-drift-report.md): cria um relatório XML das alterações que teriam sido feitas a um banco de dados registrado desde o último registro.  
  
- [Script](sqlpackage-script.md): cria um script de atualização incremental Transact-SQL que atualiza o esquema de um destino para que corresponda ao esquema de origem.  
  
A linha de comando do **SqlPackage.exe** permite que você especifique essas ações junto com parâmetros e propriedades específicos da ação.  

**[Baixe a versão mais recente](sqlpackage-download.md)** . Para obter detalhes sobre a versão mais recente, confira as [notas sobre a versão](release-notes-sqlpackage.md).
  
## <a name="command-line-syntax"></a>Sintaxe da linha de comando

O **SqlPackage.exe** inicia as ações especificadas usando os parâmetros, as propriedades e as variáveis SQLCMD especificados na linha de comando.  
  
```
SqlPackage {parameters}{properties}{SQLCMD Variables}  
```

### <a name="usage-examples"></a>Exemplos de uso

**Gerar uma comparação entre bancos de dados usando arquivos .dacpac com uma saída do script SQL**

Comece criando um arquivo .dacpac das alterações mais recentes do banco de dados:

```
sqlpackage.exe /TargetFile:"C:\sqlpackageoutput\output_current_version.dacpac" /Action:Extract /SourceServerName:"." /SourceDatabaseName:"Contoso.Database"
 ```
 
Crie um arquivo .dacpac do destino do banco de dados (que não tem alterações):

 ```
 sqlpackage.exe /TargetFile:"C:\sqlpackageoutput\output_target.dacpac" /Action:Extract /SourceServerName:"." /SourceDatabaseName:"Contoso.Database"
 ```

Crie um script SQL que gera as diferenças de dois arquivos .dacpac:

```
sqlpackage.exe /Action:Script /SourceFile:"C:\sqlpackageoutput\output_current_version.dacpac" /TargetFile:"C:\sqlpackageoutput\output_target.dacpac" /TargetDatabaseName:"Contoso.Database" /OutputPath:"C:\sqlpackageoutput\output.sql"
 ```


## <a name="version"></a>Versão

Exibe a versão do sqlpackage como um número de build.  Pode ser usada em prompts interativos, bem como em [pipelines automatizados](sqlpackage-pipelines.md).

```
sqlpackage.exe /Version
 ```


## <a name="exit-codes"></a>Códigos de saída

Comandos que retornam os seguintes códigos de saída:

- 0 = êxito
- diferente de zero = falha


## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre a [ação Extract do SqlPackage](sqlpackage-extract.md)
- Saiba mais sobre a [ação Publish do SqlPackage](sqlpackage-publish.md)
- Saiba mais sobre a [ação Export do SqlPackage](sqlpackage-export.md)
- Saiba mais sobre a [ação Import do SqlPackage](sqlpackage-import.md)
