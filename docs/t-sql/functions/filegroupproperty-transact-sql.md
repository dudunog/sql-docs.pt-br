---
title: FILEGROUPPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILEGROUPPROPERTY_TSQL
- FILEGROUPPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- filegroups [SQL Server], property values
- FILEGROUPPROPERTY function
- viewing filegroup properties
- displaying filegroup properties
ms.assetid: b3a930e6-df05-4034-929c-f681f5f6fc6e
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 5563c65352713f3557e4c412607d1944f28f3a3f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68071435"
---
# <a name="filegroupproperty-transact-sql"></a>FILEGROUPPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Essa função retorna o valor da propriedade do grupo de arquivos para um nome especificado e o valor do grupo de arquivos.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
FILEGROUPPROPERTY ( filegroup_name, property )  
```  
  
## <a name="arguments"></a>Argumentos  
 *filegroup_name*  
Uma expressão do tipo **sysname** que representa o nome do grupo de arquivos para o qual `FILEGROUPPROPERTY` retorna as informações de propriedade nomeada.  
  
 *property*  
Uma expressão do tipo **varchar(128)** que retorna o nome da propriedade de um grupo de arquivos. *Property* pode retornar um destes valores:  
  
|Valor|DESCRIÇÃO|Valor retornado|  
|-----------|-----------------|--------------------|  
|**IsReadOnly**|O grupo de arquivos é somente leitura.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada inválida.|  
|**IsUserDefinedFG**|O grupo de arquivos é um grupo de arquivos definido pelo usuário.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada inválida.|  
|**IsDefault**|O grupo de arquivos é o grupo de arquivos padrão.|1 = TRUE<br /><br /> 0 = FALSE<br /><br /> NULL = Entrada inválida.|  
  
## <a name="return-types"></a>Tipos de retorno  
**int**  
  
## <a name="remarks"></a>Comentários  
*filegroup_name* corresponde à coluna **nome** da exibição de catálogo **sys.filegroups**.  
  
## <a name="examples"></a>Exemplos  
Este exemplo retorna a configuração para a propriedade `IsDefault` para o grupo de arquivos primário no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
SELECT FILEGROUPPROPERTY('PRIMARY', 'IsDefault') AS 'Default Filegroup';  
GO  
```  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Default Filegroup   
---------------------   
1  
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [FILEGROUP_ID &#40;Transact-SQL&#41;](../../t-sql/functions/filegroup-id-transact-sql.md)   
 [FILEGROUP_NAME &#40;Transact-SQL&#41;](../../t-sql/functions/filegroup-name-transact-sql.md)   
 [Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [sys.filegroups &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)  
  
  
