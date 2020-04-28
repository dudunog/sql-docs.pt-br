---
title: Tabela de preparo da relação
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- relationships staging table [Master Data Services]
- database [Master Data Services], relationships table
ms.assetid: e19b6002-67bd-4e7d-9f19-ecb455522b1a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: dff1ab73713aed3bfb635c0399028f0c9a1a8c86
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73727912"
---
# <a name="relationship-staging-table-master-data-services"></a>Tabela de preparo de relações (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Use a tabela de preparo de relação (stg.name_Relationship) no banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para alterar o local dos membros em uma hierarquia explícita, com base na relação que os membros têm entre si.  
  
##  <a name="table-columns"></a><a name="TableColumns"></a>Colunas da tabela  
 A tabela a seguir explica para o que cada um dos campos da tabela de preparo Relação é usado.  
  
|Nome da coluna|Descrição|Valor|  
|-----------------|-----------------|-----------|  
|**ID**|Um identificador atribuído automaticamente.|Não insira um valor nesse campo. Se o lote não tiver sido processado, esse campo estará em branco.|  
|**RelationshipType**|Necessária<br /><br /> O tipo de relação que está sendo definido.|Os valores possíveis são:<br /><br /> **1**: pai<br /><br /> **2**: irmão (no mesmo nível)|  
|**ImportStatus_ID**|Necessária<br /><br /> O status do processo de importação.|Os valores possíveis são:<br /><br /> **0**, que você especifica para indicar que o registro está pronto para preparação.<br /><br /> **1**, que é atribuído automaticamente e indica que o processo de preparação do registro teve êxito.<br /><br /> **2**, que é atribuído automaticamente e indica que ocorreu uma falha no processo de preparação do registro.|  
|**Batch_ID**|Necessário apenas pelo serviço Web<br /><br /> Um identificador atribuído automaticamente que agrupa registros para preparo.<br /><br /> Se o lote não tiver sido processado, esse campo estará em branco.|Todos os membros do lote recebem esse identificador, que é exibido na interface do usuário do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , na coluna **ID** .|  
|**BatchTag**|Necessário, exceto pelo serviço Web<br /><br /> Um nome exclusivo para o lote, de até 50 caracteres.||  
|**HierarchyName**|Necessária<br /><br /> O nome da hierarquia explícita. Cada membro consolidado pode pertencer a apenas uma hierarquia.||  
|**ParentCode**|Necessária<br /><br /> Para relações pai-filho, o código do membro consolidado que será o pai da folha filho ou do membro consolidado.<br /><br /> Para relações de irmão, o código de um dos irmãos.||  
|**ChildCode**|Necessária<br /><br /> Para relações pai-filho, o código do membro consolidado ou folha que será o filho.<br /><br /> Para relações de irmão, o código de um dos irmãos.||  
|**Ordem de classificação**|Opcional<br /><br /> Um inteiro que indica a ordem do membro em relação aos outros membros sob o pai. Cada membro filho deve ter um identificador exclusivo.||  
|**ErrorCode**|Exibe um código de erro. Para todos os registros com um **ImportStatus_ID** de **2**, consulte [Erros de processo de preparo &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md).||  
  
## <a name="see-also"></a>Consulte Também  
 [Visão geral: importando dados de tabelas &#40;Master Data Services&#41;](../master-data-services/overview-importing-data-from-tables-master-data-services.md)   
 [Exibir erros que ocorrem durante o preparo &#40;Master Data Services&#41;](../master-data-services/view-errors-that-occur-during-staging-master-data-services.md)   
 [Erros de processo de preparo &#40;Master Data Services&#41;](../master-data-services/staging-process-errors-master-data-services.md)  
  
  
