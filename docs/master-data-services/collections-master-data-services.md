---
title: Coleções
ms.custom: ''
ms.date: 04/01/2016
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- collections [Master Data Services]
- collections [Master Data Services], about collections
ms.assetid: 5aa1d1e0-b4e5-4897-8e74-01dcf418df73
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 19a9d925b07b83e5ed26b73484cea955773364c6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73728608"
---
# <a name="collections-master-data-services"></a>Coleções (Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  Uma coleção é um grupo de membros folha e consolidados de uma única entidade. Use coleções quando não precisar de uma hierarquia completa e desejar exibir agrupamentos diferentes de membros para relatório ou análise, ou quando precisar criar uma taxonomia.  
  
> [!NOTE]  
>  A coleção é preterida.  
  
## <a name="what-collections-contain"></a>O que as coleções contêm  
 Coleções não limitam o número ou o tipo de membros que podem ser incluídos, desde que os membros estejam dentro da mesma entidade. Uma coleção pode conter membros folha e consolidados de várias hierarquias explícitas obrigatórias e não obrigatórias.  
  
 Quando você cria uma coleção, não está criando uma estrutura hierárquica; você está criando uma lista simples de membros. Quando você seleciona um nó de uma hierarquia e adiciona-o à coleção, o membro consolidado selecionado é o único membro acrescentado à coleção.  
  
 Uma coleção também pode conter outras coleções. É possível usar coleções de coleções para criar taxonomias.  
  
 Quando cria uma coleção, você é listado automaticamente como o proprietário. Se você for um administrador, poderá criar outros atributos para a coleção conforme necessário.  
  
## <a name="subscription-views-for-collections"></a>Exibições de assinatura para coleções  
 Há dois tipos de exibições de assinatura que mostram coleções. O formato **Atributos da coleção** mostra uma lista de coleções e todos os atributos relacionados às coleções (como descrição ou proprietário). O formato **Coleções** mostra todos os membros em todas as coleções, bem como cada peso de membros e a ordem de classificação. Para obter mais informações, consulte [Visão geral: Exportando dados &#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md).  
  
 Se você definir valores de peso para membros específicos em uma coleção, estes valores estarão disponíveis em exibições de assinatura relacionadas.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Criar uma nova coleção.|[Criar uma coleção &#40;Master Data Services&#41;](../master-data-services/create-a-collection-master-data-services.md)|  
|Adicionar membros a uma coleção existente.|[Adicionar membros a uma coleção &#40;Master Data Services&#41;](../master-data-services/add-members-to-a-collection-master-data-services.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Hierarquias explícitas &#40;Master Data Services&#41;](../master-data-services/explicit-hierarchies-master-data-services.md)  
  
-   [Visão geral: Exportando dados &#40;Master Data Services&#41;](../master-data-services/overview-exporting-data-master-data-services.md)  
  
  
