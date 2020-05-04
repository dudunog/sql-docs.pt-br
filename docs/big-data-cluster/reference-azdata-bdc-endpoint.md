---
title: azdata bdc endpoint reference
titleSuffix: SQL Server big data clusters
description: Artigo de referência para comandos bdc endpoint de azdata.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 71f52b8312518cf669751d50dcc857c3d892bd98
ms.sourcegitcommit: db1b6153f0bc2d221ba1ce15543ecc83e1045453
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/30/2020
ms.locfileid: "82588067"
---
# <a name="azdata-bdc-endpoint"></a>azdata bdc endpoint

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]  

O artigo a seguir fornece referência para o comando `bdc endpoint` na ferramenta `azdata`. Para obter mais informações sobre outros comandos `azdata`, confira [referência de azdata](reference-azdata.md)

## <a name="commands"></a>Comandos
|     |     |
| --- | --- |
[azdata bdc endpoint list](#azdata-bdc-endpoint-list) | Lista os pontos de extremidade para o cluster de Big Data.
## <a name="azdata-bdc-endpoint-list"></a>azdata bdc endpoint list
Lista os pontos de extremidade para o cluster de Big Data.

```bash
azdata bdc endpoint list [--endpoint-name -e] 
```

### <a name="optional-parameters"></a>Parâmetros opcionais

#### `--endpoint-name -e`

Nome do ponto de extremidade do cluster de Big Data.

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
