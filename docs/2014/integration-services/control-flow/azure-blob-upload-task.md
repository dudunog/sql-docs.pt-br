---
title: Tarefa de Upload do Blob do Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpblobuptask.f1
- sql11.dts.designer.afpblobuptask.f1
ms.assetid: 6ea068b0-4cd8-45b5-b89d-09b8f25040c0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 392fcbf3a46b48b2032b5792321e9a22b3027341
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62832770"
---
# <a name="azure-blob-upload-task"></a>Tarefa de Carregamento de Blobs do Azure
  A Tarefa de Carregamento de Blobs do Azure permite que um pacote SSIS carregue arquivos para um armazenamento de blobs do Azure.   
Para adicionar uma **Tarefa de Upload de Blobs do Azure**, arraste-a e solte-a no Designer SSIS, e clique duas vezes ou com o botão direito do mouse em **Editar** para ver a caixa de diálogo **Editor da Tarefa de Upload de Blobs do Azure** .  
  
 A tabela a seguir fornece descrições para os campos nessa caixa de diálogo.  
  
|||  
|-|-|  
|**Campo**|**Descrição**|  
|AzureStorageConnection|Especifique um Gerenciador de Conexão de Armazenamento do Azure existente ou crie um novo referindo-se a uma Conta de Armazenamento do Azure, que aponta para onde os arquivos de blob estão hospedados.|  
|BlobContainer|Especifica o nome do contêiner de blobs que conterá os arquivos carregados como blobs.|  
|BlobDirectory|Especifica o diretório de blob onde o arquivo carregado será armazenado como um blob de blocos. O diretório de blob é uma estrutura hierárquica virtual. Se o blob já existir, ele será substituído.|  
|LocalDirectory|Especifique o diretório local que contém os arquivos a serem carregados.|  
|FileName|Especifica um filtro de nome para selecionar arquivos com o padrão de nome especificado. Por ex.: MySheet*.xls\* inclui arquivos como MySheet001.xls e MySheetABC.xlsx.|  
|TimeRangeFrom/TimeRangeTo|Especifica um filtro de intervalo de tempo. Arquivos modificados após **TimeRangeFrom** e antes de **TimeRangeTo** serão incluídos.|  
  
  
