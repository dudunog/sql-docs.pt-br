---
title: azdata sql reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos sql de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: f8fa1ca8df7f4d72c6df9b252d639f8771dee30c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "74908744"
---
# <a name="azdata-sql"></a>azdata sql

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

O artigo a seguir fornece referência para os comandos `sql` na ferramenta `azdata`. Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata sql shell](#azdata-sql-shell) | A CLI do banco de dados SQL permite que o usuário interaja com o SQL Server por meio de T-SQL.
[azdata sql query](#azdata-sql-query) | O comando de consulta permite a execução de uma consulta T-SQL.
## <a name="azdata-sql-shell"></a>azdata sql shell
A CLI do banco de dados SQL permite que o usuário interaja com o SQL Server por meio de T-SQL.
```bash
azdata sql shell 
```
### <a name="examples"></a>Exemplos
Exemplo de linha de comando para iniciar a experiência interativa.
```bash
azdata sql shell
```
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-sql-query"></a>azdata sql query
O comando de consulta permite a execução de uma consulta T-SQL.
```bash
azdata sql query -q --database -d
```
### <a name="examples"></a>Exemplos
Selecionar a lista de nomes de tabelas.  O banco de dados usa o mestre como padrão.
```bash
azdata sql query -q 'SELECT name FROM SYS.TABLES'
```
### <a name="required-parameters"></a>Parâmetros obrigatórios
#### `--database -d`
Banco de dados nos quais executar a consulta.  O padrão é o mestre.
#### `-q`
A consulta de T-SQL a ser executada.
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org/) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md). Para obter mais informações sobre como instalar a ferramenta `azdata`, confira [Instalar azdata para gerenciar clusters de Big Data do SQL Server 2019](deploy-install-azdata.md).
