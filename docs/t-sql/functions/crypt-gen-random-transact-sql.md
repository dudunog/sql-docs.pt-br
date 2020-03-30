---
title: CRYPT_GEN_RANDOM (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CRYPT_GEN_RANDOM_TSQL
- CRYPT_GEN_RANDOM
dev_langs:
- TSQL
helpviewer_keywords:
- CRYPT_GEN_RANDOM function
ms.assetid: b74bd9d4-758e-4b94-89a0-76dcda6d8c42
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 70df8f06eb1561dd186d5be643a5863ffab5981a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68026458"
---
# <a name="crypt_gen_random-transact-sql"></a>CRYPT_GEN_RANDOM (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Essa função retorna um número criptográfico gerado aleatoriamente pela API de criptografia (CAPI). O `CRYPT_GEN_RANDOM` retorna um número hexadecimal com um comprimento de um número especificado de bytes.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CRYPT_GEN_RANDOM ( length [ , seed ] )   
```  
  
## <a name="arguments"></a>Argumentos  
*length*  
O comprimento, em bytes, do número que `CRYPT_GEN_RANDOM` criará. O argumento *length* tem um tipo de dados **int** e um intervalo de valores entre 1 e 8000. O `CRYPT_GEN_RANDOM` retorna NULL para um valor **int** fora desse intervalo. 
  
*seed*  
Um número hexadecimal opcional, para uso como um valor de semente aleatório. O comprimento de *seed* deve corresponder ao valor do argumento *length*. O argumento *seed* tem um tipo de dados **varbinary (8000)** .
  
## <a name="returned-types"></a>Tipos retornados  
**varbinary(8000)**
  
## <a name="permissions"></a>Permissões  
Esta função é pública e não requer permissões especiais.
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-generating-a-random-number"></a>a. Gerando um número aleatório  
Este exemplo gera um número aleatório de comprimento de 50 bytes:
  
```sql
SELECT CRYPT_GEN_RANDOM(50) ;  
```  
  
Este exemplo gera um número aleatório de comprimento de 4 bytes, usando uma semente de 4 bytes:
  
```sql
SELECT CRYPT_GEN_RANDOM(4, 0x25F18060) ;  
```  
  
## <a name="see-also"></a>Confira também
[RAND &#40;Transact-SQL&#41;](../../t-sql/functions/rand-transact-sql.md)
  
  
