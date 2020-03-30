---
title: Read (Mecanismo de Banco de Dados) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Read_TSQL
- Read
dev_langs:
- TSQL
helpviewer_keywords:
- Read [Database Engine]
ms.assetid: f2b8207c-b69f-4327-a874-100b3a1f27d8
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 9fb69a5c4e9d303ab0e3a7a3e2edeeeeed228391
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68000608"
---
# <a name="read-database-engine"></a>Read (Mecanismo de Banco de Dados)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

O método Read lê a representação binária de **SqlHierarchyId** do **BinaryReader** passado e define o objeto **SqlHierarchyId** com esse valor. Não é possível chamar Read usando [!INCLUDE[tsql](../../includes/tsql-md.md)]. Em seu lugar, use CAST ou CONVERT.
  
## <a name="syntax"></a>Sintaxe  
  
```sql
void Read( BinaryReader r )   
```  
  
## <a name="arguments"></a>Argumentos  
*r*  
 O objeto **BinaryReader** que produz um fluxo binário correspondente a uma representação binária de um nó **hierarchyid**.  
  
## <a name="return-types"></a>Tipos de retorno
 **Tipo de retorno do CLR: nulo**  
  
## <a name="remarks"></a>Comentários  
 O método Read não valida sua entrada. Se uma entrada binária inválida for fornecida, Read poderá gerar uma exceção. Ou poderá ser bem-sucedido e produzir um objeto **SqlHierarchyId** inválido cujos métodos podem gerar resultados imprevisíveis ou uma exceção.  
  
 O método Read pode ser chamado apenas em um objeto **SqlHierarchyId** recém-criado.  
  
 Read é usado internamente por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando necessário, como ao gravar dados na coluna **hierarchyid**. Read também é chamado internamente quando é feita uma conversão entre **varbinary** e **hierarchyid**.  
  
## <a name="examples"></a>Exemplos  
  
```sql
Byte[] encoding = new byte[] { 0x58 };  
MemoryStream stream = new MemoryStream(encoding, false /*not writable*/);  
BinaryReader br = new BinaryReader(stream);  
SqlHierarchyId hid = new SqlHierarchyId();  
hid.Read(br);   
```  
  
## <a name="see-also"></a>Consulte Também  
[Write &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/write-database-engine.md)  
[ToString &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/tostring-database-engine.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Referência de método de tipo de dados hierarchyid](https://msdn.microsoft.com/library/01a050f5-7580-4d5f-807c-7f11423cbb06)
  
  
