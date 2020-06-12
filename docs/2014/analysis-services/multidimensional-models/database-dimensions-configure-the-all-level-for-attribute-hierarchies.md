---
title: Configurar o nível (All) para hierarquias de atributo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- All members
- IsAggregatable property
- topmost levels [Analysis Services]
- (All) levels
- AttributeAllMemberName property
- levels [Analysis Services]
- members [Analysis Services], All
- AllMemberName property
ms.assetid: 0cb35e6f-b10f-483d-b893-78f6ca3979fd
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9874a8c8a6861bc7d9e44271b089e8af3a4c0ae2
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547166"
---
# <a name="configure-the-all-level-for-attribute-hierarchies"></a>Configurar o nível (All) para hierarquias de atributo
  No [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , o nível (All) é um nível opcional gerado pelo sistema. Contém apenas um membro, cujo valor é a agregação de valores de todos os membros do nível imediatamente subordinado. Este membro é chamado de membro All. Trata-se de um membro gerado pelo sistema e que não é incluído na tabela de dimensões. Como o membro do nível (All) está no topo da hierarquia, seu valor é a agregação consolidada dos valores de todos os membros da hierarquia. Geralmente, o membro All funciona como membro padrão de uma hierarquia.  
  
 A existência de um nível (All) em uma hierarquia de atributos depende da configuração da propriedade `IsAggregatable` do atributo e a existência de um nível (All) na hierarquia definida pelo usuário depende da propriedade `IsAggregatable` do atributo em seu nível mais alto. Se a propriedade `IsAggregatable` for definida como `True`, existirá um nível (All). A hierarquia não terá um nível (All) se a propriedade `IsAggregatable` estiver configurada como `False`.  
  
## <a name="establishing-the-topmost-level"></a>Estabelecendo o nível mais alto  
 Se a propriedade `IsAggregatable` estiver configurada como `False` no atributo de origem de um nível da hierarquia, nenhum nível agregável pode aparecer acima dele na hierarquia. Um nível não agregável deve ser o nível mais alto de qualquer hierarquia ou a propriedade `IsAggregatable` dos atributos de origem de todos os níveis acima dele também deve ser configurada como `False`.  
  
## <a name="all-member-and-all-level"></a>Membro e nível (All)  
 O único membro do nível (All) é chamado de membro All. A `AttributeAllMemberName` propriedade em uma dimensão especifica o nome do membro All para atributos em uma dimensão. A propriedade `AllMemberName` em uma hierarquia especifica o nome do membro All para seus atributos.  
  
## <a name="see-also"></a>Consulte Também  
 [Definir um membro padrão](attribute-properties-define-a-default-member.md)  
  
  
