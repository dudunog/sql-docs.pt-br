---
title: azdata app template reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos azdata app template.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: seanw
ms.date: 09/22/2020
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e56de1b76dc456a57f721378518d2942822cec20
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92358834"
---
# <a name="azdata-app-template"></a>azdata app template

Aplica-se ao [!INCLUDE [azure-data-cli-azdata](../../includes/azure-data-cli-azdata.md)]

O artigo a seguir fornece referência para os comandos **sql** na ferramenta **azdata**. Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos

|Comando|Descrição|
| --- | --- |
[azdata app template list](#azdata-app-template-list) | Buscar modelos com suporte.
[azdata app template pull](#azdata-app-template-pull) | Baixar modelos com suporte.
## <a name="azdata-app-template-list"></a>azdata app template list
Buscar modelos com suporte no repositório GitHub [URL] especificado.
```bash
azdata app template list [--url -u] 
                         
```
### <a name="examples"></a>Exemplos
Buscar todos os modelos na localização do repositório de modelos padrão.
```bash
azdata app template list
```
Buscar todos os modelos em uma localização de repositório diferente.
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--url -u`
Especificar uma localização de repositório de modelos diferente. Padrão: https://github.com/Microsoft/SQLBDC-AppDeploy.git
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.
## <a name="azdata-app-template-pull"></a>azdata app template pull
Baixar modelos com suporte no repositório GitHub [URL] especificado.
```bash
azdata app template pull [--name -n] 
                         [--url -u]  
                         
[--destination -d]
```
### <a name="examples"></a>Exemplos
Baixar todos os modelos na localização do repositório de modelos padrão.
```bash
azdata app template pull
```
Baixar todos os modelos em uma localização de repositório diferente.
```bash
azdata app template list --url https://github.com/diffrent/templates.git
```
Baixar modelo individual por nome.
```bash
azdata app template pull --name ssis            
```
### <a name="optional-parameters"></a>Parâmetros opcionais
#### `--name -n`
Nome do modelo. Para obter uma lista completa de nomes de modelos com suporte, execute `azdata app template list`
#### `--url -u`
Especificar uma localização de repositório de modelos diferente. Padrão: https://github.com/Microsoft/SQLBDC-AppDeploy.git
#### `--destination -d`
Onde posicionar o modelo do esqueleto do aplicativo.
`./templates`
### <a name="global-arguments"></a>Argumentos globais
#### `--debug`
Aumente o detalhamento do log para mostrar todos os logs de depuração.
#### `--help -h`
Mostrar esta mensagem de ajuda e sair.
#### `--output -o`
Formato de saída.  Valores permitidos: json, jsonc, table, tsv.  Padrão: json.
#### `--query -q`
Cadeia de caracteres de consulta JMESPath. Confira [http://jmespath.org/](http://jmespath.org) para obter mais informações e exemplos.
#### `--verbose`
Aumentar o detalhamento do log. Use --debug para logs de depuração completos.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre outros comandos de **azdata**, confira [referência de azdata](reference-azdata.md). 

Para obter mais informações sobre como instalar a ferramenta **azdata**, confira [Instalar azdata](..\install\deploy-install-azdata.md).

