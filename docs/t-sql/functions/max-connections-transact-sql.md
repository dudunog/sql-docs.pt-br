---
title: '@@MAX_CONNECTIONS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@MAX_CONNECTIONS'
- '@@MAX_CONNECTIONS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- simultaneous connections [SQL Server]
- maximum number of simultaneous user connections
- '@@MAX_CONNECTIONS function'
- connections [SQL Server], simultaneous
- number of simultaneous user connections
ms.assetid: 57eb9f4b-548f-4212-9684-a11d831c4732
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 77b3acdd0ca96286d626d7b2d1b69514853c5b78
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82822663"
---
# <a name="x40x40max_connections-transact-sql"></a>&#x40;&#x40;MAX_CONNECTIONS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o número de máximo de conexões de usuário simultâneas permitidas em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O número retornado não é necessariamente o número configurado no momento.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
@@MAX_CONNECTIONS  
```  
  
## <a name="return-types"></a>Tipos de retorno  
 **inteiro**  
  
## <a name="remarks"></a>Comentários  
 O número atual de conexões de usuário permitidas depende também da versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que está instalada e dos limites de seus aplicativos e hardware.  
  
 Para reconfigurar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para menos conexões, use **sp_configure**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir aparece retornando o número de máximo de conexões de usuário em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O exemplo presume que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não foi reconfigurado para menos conexões de usuário.  
  
```  
SELECT @@MAX_CONNECTIONS AS 'Max Connections';  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Max Connections  
---------------  
32767            
```  
  
## <a name="see-also"></a>Consulte Também  
 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [Funções de configuração](../../t-sql/functions/configuration-functions-transact-sql.md)   
 [Configurar a opção user connections de configuração do servidor](../../database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md)  
  
  
