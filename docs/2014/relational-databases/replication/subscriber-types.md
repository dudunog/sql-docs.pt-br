---
title: Tipos de assinante | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.newpubwizard.subscribertypes.f1
ms.assetid: a70656cb-21c9-4489-be77-ccd396747e3b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b9445c7b366a43253da4accabaf98d9c5b7f8d92
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62630631"
---
# <a name="subscriber-types"></a>Tipos de Assinantes
  A replicação de mesclagem permite especificar a que tipos de Assinantes uma publicação deve dar suporte. A seleção dos tipos de Assinantes define o *nível de compatibilidade da publicação*, que determina quais recursos podem ser usados por uma publicação.  
  
 Depois que um instantâneo de publicação é criado, o nível de compatibilidade da publicação pode ser aumentado (tornado mais restrito) na página **Geral** da caixa de diálogo **Propriedades de Publicação** ; o nível de compatibilidade não pode ser diminuído.  
  
## <a name="options"></a>Opções  
 Selecione cada tipo de Assinante a que esta publicação deve dar suporte.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 A publicação pode usar todos os recursos.  
  
 [!INCLUDE[ssEW](../../includes/ssew-md.md)]  
 A publicação exige que os arquivos de instantâneo estejam no formato de caractere (isto é tratado automaticamente pelo Agente de Instantâneo). O[!INCLUDE[ssEW](../../includes/ssew-md.md)] também tem várias restrições não relacionadas ao nível de compatibilidade.  
  
 Se essa opção for selecionada, a opção de sincronização da Web estará habilitada para a publicação. Para obter mais informações sobre a sincronização da Web, consulte [Web Synchronization for Merge Replication](web-synchronization-for-merge-replication.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Publicar dados e objetos de banco de dados](publish/publish-data-and-database-objects.md)   
 [Create a Publication](publish/create-a-publication.md)   
 [Exibir e modificar propriedades de Publicador e Distribuidor](view-and-modify-distributor-and-publisher-properties.md)   

  
