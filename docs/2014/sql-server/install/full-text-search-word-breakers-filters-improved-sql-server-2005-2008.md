---
title: Os separadores de palavras de pesquisa de texto completo e os filtros melhoraram significativamente no SQL Server 2005 e SQL Server 2008 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- filters [Full-Text Search]
- word breakers [Full-Text Search]
ms.assetid: 8d06bda9-0bbf-4baa-b270-07b1c1f640eb
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: d2e7d3b8da56b407d3937b05cd980c3f8a4eb0c3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85036806"
---
# <a name="full-text-search-word-breakers-and-filters-significantly-improved-in-sql-server-2005-and-sql-server-2008"></a>Significativa melhora nos separadores de palavras e filtros da Pesquisa de Texto Completo no SQL Server 2005 e SQL Server 2008
  Os separadores de palavras e os filtros foram alterados significativamente. Foram implementadas outras melhorias nos separadores de palavras, incluindo aperfeiçoamento com relação à abrangência do idioma e à confiabilidade.  
  
## <a name="description"></a>Descrição  
 Separadores de palavras e filtros usados pela Pesquisa de Texto Completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foram aperfeiçoados com relação à funcionalidade e à confiabilidade. Em alguns casos específicos, alterações em separadores de palavras podem impactar na geração de tokens de alguns dados. Os tokens criados no [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] podem ser diferentes dos tokens criados no [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] ou [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 Para obter informações sobre separadores de palavras, consulte [configurar e gerenciar separadores de palavras e lematizadores para pesquisa](../../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhando com o Supervisor de Atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
