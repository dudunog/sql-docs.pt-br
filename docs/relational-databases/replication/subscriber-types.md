---
description: Tipos de Assinantes
title: Tipos de assinante | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.subscribertypes.f1
ms.assetid: a70656cb-21c9-4489-be77-ccd396747e3b
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-current||>=sql-server-2016
ms.openlocfilehash: 0f6ba4369e2ac2da9058621108f310e1b3f8e953
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480957"
---
# <a name="subscriber-types"></a>Tipos de Assinantes
[!INCLUDE[sql-asdb](../../includes/applies-to-version/sql-asdb.md)]
  A replicação de mesclagem permite especificar a que tipos de Assinantes uma publicação deve dar suporte. A seleção dos tipos de Assinantes define o *nível de compatibilidade da publicação*, que determina quais recursos podem ser usados por uma publicação.  
  
 Depois que um instantâneo de publicação é criado, o nível de compatibilidade da publicação pode ser aumentado (tornado mais restrito) na página **Geral** da caixa de diálogo **Propriedades de Publicação** ; o nível de compatibilidade não pode ser diminuído.  

[!INCLUDE[azure-sql-db-replication-supportability-note](../../includes/azure-sql-db-replication-supportability-note.md)]
  
## <a name="options"></a>Opções  
 Selecione cada tipo de Assinante a que esta publicação deve dar suporte.  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 A publicação pode usar todos os recursos.  
  
 [!INCLUDE[ssEW](../../includes/ssew-md.md)]  
 A publicação exige que os arquivos de instantâneo estejam no formato de caractere (isto é tratado automaticamente pelo Agente de Instantâneo). O[!INCLUDE[ssEW](../../includes/ssew-md.md)] também tem várias restrições não relacionadas ao nível de compatibilidade.  
  
 Se essa opção for selecionada, a opção de sincronização da Web estará habilitada para a publicação. Para obter mais informações sobre a sincronização da Web, consulte [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Publicar dados e objetos de banco de dados](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [Exibir e modificar propriedades de Publicador e Distribuidor](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
  
  
