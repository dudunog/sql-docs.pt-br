---
author: MikeRayMSFT
ms.prod: sql
ms.topic: include
ms.date: 01/07/2020
ms.author: mikeray
ms.openlocfilehash: 0c15fb58bb076724402ab72f81e58ce46c8b7b1e
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257386"
---
### <a name="pythonpip-installation"></a>Instalação do Python/Pip

Você pode instalar a [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)] no Linux com o yum, o apt ou o zypper ou, no MacOS, com gerenciadores de pacotes de instalação do Homebrew. Antes desses gerenciadores de pacotes estarem disponíveis, a instalação exigia o Python e o pip.

>[!IMPORTANT]
>Antes de prosseguir, você precisa remover todas as instalações do `azdata` que foram instaladas no sistema global Python. Os novos instaladores ou pacotes nativos adicionam `azdata` ao seu caminho e é impossível saber qual é o primeiro.
Se você tiver um `azdata` instalado no Python do sistema global, remova-o antes de continuar.

Para exibir a instalação atual, execute o seguinte comando:

```bash
$ pip list --format columns
```

Se `azdata` for instalado pelo pip, ele retornará o pacote e a versão. Por exemplo:

```
 Package             Version
------------------- ----------
azdata-cli          15.0.X
azdata-cli-app      15.0.X
azdata-cli-cluster  15.0.X
azdata-cli-core     15.0.X
azdata-cli-hdfs     15.0.X
azdata-cli-notebook 15.0.X
azdata-cli-profile  15.0.X
azdata-cli-spark    15.0.X
azdata-cli-sql      15.0.X
```

O exemplo a seguir remove uma instalação do pip do `azdata`.

```bash
$ pip freeze | grep azdata-* | xargs pip uninstall -y
```

Depois de verificar se você removeu qualquer instalação do `azdata` que foi instalado com o Pip, continue com sua instalação.