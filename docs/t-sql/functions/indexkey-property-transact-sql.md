---
description: INDEXKEY_PROPERTY (Transact-SQL)
title: INDEXKEY_PROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- INDEXKEY_PROPERTY_TSQL
- INDEXKEY_PROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- index keys [SQL Server]
- INDEXKEY_PROPERTY function
- viewing index keys
- displaying index keys
- keys [SQL Server], index
ms.assetid: 87c0c385-6b2d-4716-ac8c-a3ce6e8d89e9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 60247a9c2dcdc038f17edc9637805c62e02fe0d0
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91115445"
---
# <a name="indexkey_property-transact-sql"></a>INDEXKEY_PROPERTY (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre a chave de índice. Retorna NULL para índices XML.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
INDEXKEY_PROPERTY ( object_ID ,index_ID ,key_ID ,property )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *object_ID*  
 É o número de identificação do objeto da tabela ou exibição indexada. *object_ID* é **int**.  
  
 *index_ID*  
 É o número de identificação do índice. *index_ID* é **int**.  
  
 *key_ID*  
 É a posição da coluna de chave do índice. *key_ID* é **int**.  
  
 *property*  
 O nome do arquivo da propriedade para o qual as informações serão retornadas. *property* é uma cadeia de caracteres e pode ter um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**ColumnId**|ID de Coluna na posição *key_ID* do índice.|  
|**IsDescending**|Ordem na qual a coluna de índice é armazenada.<br /><br /> 1 = Descendente 0 = Ascendente|  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="exceptions"></a>Exceções  
 Retornará NULL em caso de erro ou se um chamador não tiver permissão para exibir o objeto.  
  
 Um usuário só pode exibir metadados de protegíveis de sua propriedade ou para os quais recebeu permissão. Isso significa que as funções internas emissoras de metadados, como INDEXKEY_PROPERTY, podem retornar NULL se o usuário não tiver permissão no objeto. Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="examples"></a>Exemplos  
 No exemplo a seguir, são retornadas ambas as propriedades para ID de índice `1`, coluna de chave `1` na tabela `Production.Location`.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT   
    INDEXKEY_PROPERTY(OBJECT_ID('Production.Location', 'U'),  
        1,1,'ColumnId') AS [Column ID],  
    INDEXKEY_PROPERTY(OBJECT_ID('Production.Location', 'U'),  
        1,1,'IsDescending') AS [Asc or Desc order];  
```  
  
 Este é o conjunto de resultados:  
  
```  
Column ID   Asc or Desc order   
----------- -----------------   
1           0  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [INDEX_COL &#40;Transact-SQL&#41;](../../t-sql/functions/index-col-transact-sql.md)   
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)  
  
  
