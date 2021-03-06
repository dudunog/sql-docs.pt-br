---
description: SET TEXTSIZE (Transact-SQL)
title: SET TEXTSIZE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TEXTSIZE_TSQL
- TEXTSIZE
- SET_TEXTSIZE_TSQL
- SET TEXTSIZE
dev_langs:
- TSQL
helpviewer_keywords:
- SET TEXTSIZE statement
- SELECT statement [SQL Server], text size returned
- size [SQL Server], text and image data
- TEXTSIZE option
- text size returned [SQL Server]
ms.assetid: 787154a6-39a6-4dd6-a6d0-67b4364f95d5
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0d7800e643010a9a4064ca1b113e7c7b84e12742
ms.sourcegitcommit: e40e75055c1435c5e3f9b6e3246be55526807b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/13/2021
ms.locfileid: "98151317"
---
# <a name="set-textsize-transact-sql"></a>SET TEXTSIZE (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Especifica o tamanho, em bytes, dos dados **varchar(max)** , **nvarchar(max)** , **varbinary(max)** , **text**, **ntext** e **image** retornados ao cliente por uma instrução SELECT.  
  
> [!IMPORTANT]
>  Os tipos de dados **ntext**, **text** e **image** serão removidos em uma versão futura do [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Evite usar esses tipos de dados em novos trabalhos de desenvolvimento e planeje modificar os aplicativos que os utilizam atualmente. Em vez disso, use **nvarchar(max)**, **varchar(max)** e **varbinary(max)** .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
SET TEXTSIZE { number }   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *number*  
 É o tamanho dos dados **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, **text**, **ntext** ou **image** em bytes. *number* é um inteiro com um valor máximo de 2147483647 (2 GB).  Um valor -1 indica um tamanho ilimitado. Um valor 0 redefine o tamanho para o valor padrão de 4 KB.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (10.0 e superior) e o Driver ODBC para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificam automaticamente `-1` (ilimitado) durante a conexão.  
  
 **Drivers anteriores ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008:** o driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client e o Provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client (versão 9) para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definem TEXTSIZE automaticamente como 2147483647 durante a conexão.  
  
## <a name="remarks"></a>Comentários  
 A definição de SET TEXTSIZE afeta a função @@TEXTSIZE.  
  
 A configuração de TEXTSIZE é definida na execução ou em tempo de execução, e não no momento de análise.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="see-also"></a>Consulte Também  
 [@@TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/functions/textsize-transact-sql.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
