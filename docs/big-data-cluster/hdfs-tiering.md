---
title: Configurar a camada do HDFS
titleSuffix: SQL Server big data clusters
description: Este artigo explica como configurar a camada do HDFS para montar um sistema de arquivos externo do Azure Data Lake Storage no HDFS em um cluster de Big Data do SQL Server 2019.
author: nelgson
ms.author: negust
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 60aa2f27f83b4b3e91f22e54cb85fa0794a5355f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85730643"
---
# <a name="configure-hdfs-tiering-on-big-data-clusters-2019"></a>Configurar as camadas do HDFS no [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

A camada do HDFS fornece a capacidade de montar um sistema de arquivos externo e compatível com HDFS no HDFS. Este artigo explica como configurar as camadas do HDFS para Clusters de Big Data do SQL Server. No momento, damos suporte à conexão com o Azure Data Lake Storage Gen2 e ao Amazon S3. 

## <a name="hdfs-tiering-overview"></a>Visão geral da camada do HDFS

Com a camada, os aplicativos podem acessar diretamente os dados em uma variedade de armazenamentos externos, como se os dados residissem no HDFS local. A montagem é uma operação de metadados, em que os metadados que descrevem o namespace no sistema de arquivos externo são copiados para o HDFS local. Esses metadados incluem informações sobre os diretórios e os arquivos externos junto com as permissões e as ACLs deles. Os dados correspondentes só são copiados sob demanda, quando os próprios dados são acessados por meio de uma consulta, por exemplo. Os dados do sistema de arquivos externos agora podem ser acessados por meio do cluster de Big Data do SQL Server. Você pode executar trabalhos do Spark e consultas SQL nesses dados da mesma forma que os executaria em dados locais armazenados no HDFS no cluster.

Este vídeo de sete minutos mostra uma visão geral das camadas do HDFS:

> [!VIDEO https://channel9.msdn.com/Shows/Data-Exposed/Unify-your-data-lakes-with-HDFS-tiering/player?WT.mc_id=dataexposed-c9-niner]


### <a name="caching"></a>Cache
Hoje, por padrão, 1% do armazenamento total do HDFS será reservado para o cache de dados montados. O cache é uma configuração global em montagens.

> [!NOTE]
> A camada do HDFS é um recurso desenvolvido pela Microsoft e uma versão anterior dele foi lançada como parte da distribuição do Apache Hadoop 3.1. Para obter mais informações, confira [https://issues.apache.org/jira/browse/HDFS-9806](https://issues.apache.org/jira/browse/HDFS-9806) para obter detalhes.

As seções a seguir fornecem um exemplo de como configurar a camada do HDFS com uma fonte de dados do Azure Data Lake Storage Gen2.

## <a name="refresh"></a>Atualizar

A camada do HDFS dá suporte à atualização. Atualize uma montagem existente para o instantâneo mais recente dos dados remotos.

## <a name="prerequisites"></a>Pré-requisitos

- [Cluster de Big Data implantado](deployment-guidance.md)
- [Ferramentas de Big Data](deploy-big-data-tools.md)
  - **azdata**
  - **kubectl**

## <a name="mounting-instructions"></a>Instruções de montagem

Damos suporte à conexão com o Azure Data Lake Storage Gen2 e o Amazon S3. Encontre as instruções sobre como realizar a montagem nesses tipos de armazenamento nos seguintes artigos:

- [Como montar o ADLS Gen2 para a camada do HDFS em um cluster de Big Data](hdfs-tiering-mount-adlsgen2.md)
- [Como montar o S3 para a camada do HDFS em um cluster de Big Data](hdfs-tiering-mount-s3.md)

## <a name="known-issues-and-limitations"></a><a id="issues"></a> Problemas conhecidos e limitações

A seguinte lista fornece os problemas conhecidos e as limitações atuais ao usar as camadas do HDFS no [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]:

- Se a montagem estiver travada em um estado `CREATING` por muito tempo, provavelmente, ela terá falhado. Nessa situação, cancele o comando e exclua a montagem, se necessário. Verifique se os parâmetros e as credenciais estão corretos antes de repetir a operação.

- Não é possível criar montagens em diretórios existentes.

- Não é possível criar montagens em montagens existentes.

- Se um dos ancestrais do ponto de montagem não existir, ele será criado com as permissões que usam r-xr-xr-x (555) como padrão.

- A criação da montagem pode levar algum tempo, dependendo do número e do tamanho dos arquivos que estão sendo montados. Durante esse processo, os arquivos da montagem não ficam visíveis para os usuários. Enquanto a montagem é criada, todos os arquivos serão adicionados a um caminho temporário, que usa `/_temporary/_mounts/<mount-location>` como padrão.

- O comando de criação da montagem é assíncrono. Depois que o comando é executado, o status de montagem pode ser verificado para entender o estado da montagem.

- Ao criar a montagem, o argumento usado para **--mount-path** é essencialmente um identificador exclusivo da montagem. A mesma cadeia de caracteres (incluindo a "/" no final, se presente) precisa ser usada nos comandos seguintes.

- As montagens são somente leitura. Não é possível criar diretórios nem arquivos em uma montagem.

- Não recomendamos a montagem de diretórios e arquivos que possam ser alterados. Após a criação da montagem, qualquer alteração ou atualização na localização remota não será refletida na montagem no HDFS. Se ocorrerem alterações na localização remota, você poderá optar por excluir e recriar a montagem para que ela reflita o estado atualizado.

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)], confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
