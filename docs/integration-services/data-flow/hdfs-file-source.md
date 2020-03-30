---
title: Origem do arquivo HDFS | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hdfsfilesrc.f1
ms.assetid: f8cda200-c389-4a2e-8ee9-5d59b326aac1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8a06374e2803a5e482e6d5a7a665756e38cb7f2f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71292441"
---
# <a name="hdfs-file-source"></a>Origem do arquivo HDFS

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  O componente de origem do arquivo HDFS permite que um pacote do SSIS leia dados de um arquivo HDFS. Os formatos de arquivo com suporte são texto e Avro. (Não há suporte para fontes de dados ORC.)  
  
 Para configurar a origem do arquivo HDFS, arraste e solte o arquivo de origem HDFS no designer de fluxo de dados e clique duas vezes no componente para abrir o editor.  
  
 ![Editor de Origem do Arquivo do HDFS](../../integration-services/data-flow/media/hdfs-file-source.png "Editor de Origem do Arquivo do HDFS")  
  
## <a name="options"></a>Opções  
 Configure as seguintes opções na guia **Geral** da caixa de diálogo **Editor de Origem de Arquivo Hadoop** .  
  
|Campo|DESCRIÇÃO|  
|-----------|-----------------|  
|**Conexão do Hadoop**|Especifique um gerenciador de conexões do Hadoop existente ou crie um novo. Esse gerenciador de conexões indica onde os arquivos HDFS estão hospedados.|  
|**Caminho do Arquivo**|Especifique o nome do arquivo HDFS.|  
|**Formato de arquivo**|Especifique o formato do arquivo HDFS. As opções disponíveis são Texto e Avro. (Não há suporte para fontes de dados ORC.)|  
|**Caractere delimitador de coluna**|Se você selecionar o formato Texto, especifique o caractere delimitador de coluna.|  
|**Nomes de coluna na primeira linha de dados**|Se você selecionar o formato Texto, indique se a primeira linha no arquivo conterá nomes de coluna.|  
  
 Depois de configurar essas opções, selecione a guia **Colunas** para mapear colunas de origem para colunas de destino no fluxo de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciador de conexões do Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [Destino de Arquivo HDFS](../../integration-services/data-flow/hdfs-file-destination.md)  
  
  
