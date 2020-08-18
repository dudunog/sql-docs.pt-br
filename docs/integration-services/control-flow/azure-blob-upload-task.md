---
description: Tarefa de Carregamento de Blobs do Azure
title: Tarefa de Upload do Blob do Azure | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpblobuptask.f1
- sql14.dts.designer.afpblobuptask.f1
ms.assetid: 6ea068b0-4cd8-45b5-b89d-09b8f25040c0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 4fefa039f03e061c683c3df916a25087cb9a4e5c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88349962"
---
# <a name="azure-blob-upload-task"></a>Tarefa de Carregamento de Blobs do Azure

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


A **Tarefa de Upload de Blobs do Azure** permite que um pacote SSIS carregue arquivos para um armazenamento de blobs do Azure.
    
Para adicionar uma **Tarefa de Upload de Blobs do Azure**, arraste-a e solte-a no Designer SSIS, e clique duas vezes ou com o botão direito do mouse em **Editar** para ver a caixa de diálogo **Editor da Tarefa de Upload de Blobs do Azure** .  
  
 A **Tarefa de Upload de Blobs do Azure** é um componente do [SSIS (SQL Server Integration Services) Feature Pack para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).
  
 A tabela a seguir fornece descrições para os campos nessa caixa de diálogo.  

|**Campo**|**Descrição**|  
|---|---|  
|AzureStorageConnection|Especifique um Gerenciador de Conexão de Armazenamento do Azure existente ou crie um novo referindo-se a uma Conta de Armazenamento do Azure, que aponta para onde os arquivos de blob estão hospedados.|  
|BlobContainer|Especifica o nome do contêiner de blobs que contém os arquivos carregados como blobs.|  
|BlobDirectory|Especifica o diretório de blob em que o arquivo carregado é armazenado como um blob de blocos. O diretório de blob é uma estrutura hierárquica virtual. Se o blob já existir, ele será substituído.|  
|LocalDirectory|Especifique o diretório local que contém os arquivos a serem carregados.|  
|SearchRecursively|Especifique se é necessário pesquisar recursivamente dentro dos subdiretórios.|  
|FileName|Especifica um filtro de nome para selecionar arquivos com o padrão de nome especificado. Por exemplo, `MySheet*.xls\*` inclui arquivos como `MySheet001.xls` e `MySheetABC.xlsx`.|  
|TimeRangeFrom/TimeRangeTo|Especifica um filtro de intervalo de tempo. Arquivos modificados após **TimeRangeFrom** e antes de **TimeRangeTo** são incluídos.|  
