---
description: sp_help_fulltext_catalog_components (Transact-SQL)
title: sp_help_fulltext_catalog_components (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_catalog_components_TSQL
- sp_help_fulltext_catalog_components
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_catalog_components
ms.assetid: fbd6a3d4-6a4c-42a2-bff8-2a5eb0745e47
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2884cda986a99f23c88c71c8960d25a467de0663
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548013"
---
# <a name="sp_help_fulltext_catalog_components-transact-sql"></a>sp_help_fulltext_catalog_components (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna uma lista de todos os componentes (filtros, separadores de palavras e manipuladores de protocolo) usados em todos os catálogos de texto completo do banco de dados atual.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_fulltext_catalog_components  
```  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**nome do catálogo de texto completo**|**int**|Nome do catálogo de texto completo.|  
|**ID do catálogo de texto completo**|**sysname**|Identificação do catálogo de texto completo.|  
|**componenttype**|**sysname**|Tipo de componente. Um dos seguintes:<br /><br /> Filtrar<br /><br /> Manipulador de protocolo<br /><br /> Separador de palavras|  
|**ComponentName**|**sysname**|Nome do componente.|  
|**CLSID**|**uniqueidentifier**|Identificador de classe do componente.|  
|**FullPath**|**nvarchar(256)**|Caminho até a localização do componente.<br /><br /> NULL = o chamador não é um membro da função de servidor fixa **ServerAdmin** .|  
|**version**|**nvarchar(30)**|A versão do componente.|  
|**manufacturer**|**sysname**|Nome do fabricante do componente.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="see-also"></a>Consulte Também  
 [Os procedimentos armazenados de pesquisa de texto completo e de semântica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [sys.fulltext_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_help_fulltext_system_components ](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)   
 [Pesquisa de texto completo](../../relational-databases/search/full-text-search.md)  
  
  
