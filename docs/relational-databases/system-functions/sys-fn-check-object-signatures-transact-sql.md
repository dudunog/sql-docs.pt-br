---
description: sys.fn_check_object_signatures (Transact-SQL)
title: sys.fn_check_object_signatures (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_check_object_signatures_TSQL
- fn_check_object_signatures_TSQL
- fn_check_object_signatures
- sys.fn_check_object_signatures
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_check_object_signatures function
ms.assetid: 47509566-d3d7-46a9-89c1-91b4895d56b9
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4efb55bdeb3455c2c98278e8b90021c5cf194146
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98099648"
---
# <a name="sysfn_check_object_signatures-transact-sql"></a>sys.fn_check_object_signatures (Transact-SQL)
[!INCLUDE [sql-asdbmi-pdw](../../includes/applies-to-version/sql-asdbmi-pdw.md)]

  Retorna uma lista de todos os objetos assináveis e indica se um objeto foi assinado por um determinado certificado ou chave assimétrica. Se o objeto foi assinado pelo certificado ou pela chave assimétrica especificada, também indicará se a assinatura do objeto é válida.  
  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn_ check_object_signatures (   
    { '@class' } , { @thumbprint }   
  )   
```  
  
## <a name="arguments"></a>Argumentos  
 { '\@ *classe*'}  
 Identifica o tipo da impressão digital fornecida:  
  
-   'certificado'  
  
-   'chave assimétrica'  
  
 \@a *classe* é **sysname**.  
  
 { \@ *Thumbprint* }  
 O hash SHA-1 do certificado com o qual a chave é criptografada, ou o GUID da chave assimétrica com a qual a chave é criptografada. \@a *impressão digital* é **varbinary (20)**.  
  
## <a name="tables-returned"></a>Tabelas retornadas  
 A tabela a seguir lista as colunas que **fn_check_object_signatures** retorna.  
  
|Coluna|Type|Descrição|  
|------------|----------|-----------------|  
|type|**nvarchar(120)**|Retorna a descrição do tipo ou o assembly.|  
|entity_id|**int**|Retorna a id de objeto do objeto que está sendo avaliado.|  
|is_signed|**int**|Retorna 0 quando o objeto não foi assinado pela impressão digital fornecida. Retorna 1 quando o objeto foi assinado pela impressão digital fornecida.|  
|is_signature_valid|**int**|Quando o valor is_signed é 1, retorna 0 quando a assinatura não é válida. Retorna 1 quando a assinatura é válida.<br /><br /> Quando o valor is_signed é 0, sempre retorna 0.|  
  
## <a name="remarks"></a>Comentários  
 Use **fn_check_object_signatures** para confirmar que usuários mal-intencionados não violaram objetos.  
  
## <a name="permissions"></a>Permissões  
 Requer VIEW DEFINITION no certificado ou na chave assimétrica.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir detecta o certificado autenticado de esquema relativo ao banco de dados `master` e retorna o valor `is_signed` de 1 e o valor `is_signature_valid` de 1 para objetos que foram assinados pelo certificado autenticado de esquema e que têm assinaturas válidas.  
  
```  
USE master;  
-- Declare a variable to hold the thumbprint.  
DECLARE @thumbprint varbinary(20) ;  
-- Populate the thumbprint variable with the master database schema signing certificate.  
SELECT @thumbprint = thumbprint   
FROM sys.certificates   
WHERE name LIKE '%SchemaSigningCertificate%' ;  
-- Evaluates the objects signed by the schema signing certificate  
SELECT type, entity_id, OBJECT_NAME(entity_id) AS [object name], is_signed, is_signature_valid  
FROM sys.fn_check_object_signatures ('certificate', @thumbprint) ;  
GO  
  
```  
  
## <a name="see-also"></a>Consulte Também  
 [IS_OBJECTSIGNED &#40;Transact-SQL&#41;](../../t-sql/functions/is-objectsigned-transact-sql.md)  
  
  
