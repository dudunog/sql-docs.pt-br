---
description: 'Visão geral: exportando dados [Master Data Services]'
title: Exporting Data
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- exporting data [Master Data Services]
- subscription views [Master Data Services]
- subscription views [Master Data Services], about subscription views
ms.assetid: 8b74409a-ea70-45f8-84c7-da6905e4901a
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: f477249f9f65b85598a11e40da268aa3a15b35a3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88342932"
---
# <a name="overview-exporting-data-master-data-services"></a>Visão geral: exportando dados [Master Data Services]

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Este artigo apresenta os tipos de formatos de exibição de assinatura e como determinar quando as exibições precisam ser editadas devido a alterações em objetos de modelo.  
  
 Você cria uma exibição de assinatura para exportar dados do [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] para um sistema de assinatura, como [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Você usa o sistema de assinatura para exibir os dados no banco de dados [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .  Para obter informações sobre como criar a exibição de assinatura, consulte [Criar uma exibição de assinatura para exportar dados &#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)  
  
 Para obter mais informações sobre modos de exibição, consulte [Modos de exibição](../relational-databases/views/views.md).  
  
## <a name="subscription-view-formats"></a>Formatos de exibição da assinatura  
 Ao criar uma exibição do [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], você faz escolhas em um conjunto de formatos de exibição padrão fornecido pelo [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Esses formatos podem ser usados para criar exibições que mostram:  
  
-   Todos os membros da folha e seus atributos.  
  
-   Todos os membros da folha consolidados e seus atributos.  
  
-   Todas as coleções e seus atributos.  
  
-   Os membros explicitamente adicionados a uma coleção.  
  
-   Os membros de uma hierarquia derivada, em formato pai-filho ou de nível.  
  
-   Os membros de todas as hierarquias explícitas de uma entidade, em formato pai-filho ou de nível.  
  
## <a name="subscription-views-can-become-out-of-date"></a>Exibições de assinatura podem se tornar desatualizadas  
 Depois de criar uma exibição de assinatura para uma entidade ou hierarquia, as alterações nos objetos modelo associados não são refletidas automaticamente na exibição. Talvez seja necessário gerar novamente uma exibição de assinatura no [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] para refletir as alterações nos objetos modelo. A coluna **Alterado** na página **Exportação** é atualizada para **True** quando objetos do modelo forem alterados. **True** indica que você deve editar e salvar a exibição de assinatura, o que gera novamente a exibição.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Criar uma exibição de assinatura de seus dados mestre.|[Criar uma exibição de assinatura para exportar dados &#40;Master Data Services&#41;](../master-data-services/create-a-subscription-view-to-export-data-master-data-services.md)|  
|Excluir uma exibição de assinatura existente.|[Excluir uma exibição de assinatura &#40;Master Data Services&#41;](../master-data-services/delete-a-subscription-view-master-data-services.md)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   [Formatos de exibição de assinatura &#40;Master Data Services&#41;](../master-data-services/subscription-view-formats-master-data-services.md)  
  
-   [Exibições](../relational-databases/views/views.md)  
  
  
