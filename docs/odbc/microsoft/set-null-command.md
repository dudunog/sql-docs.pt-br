---
description: Comando SET NULL
title: Definir comando nulo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set nullSET NULL
ms.assetid: 410c5a6e-e957-4ecc-9e2d-e591cbc0bc4f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e98037838325a0bfe56b51cdcfec7df8539facd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421840"
---
# <a name="set-null-command"></a>Comando SET NULL
Determina como os valores nulos são suportados pelos comandos ALTER TABLE-SQL, CREATE TABLE-SQL e INSERT-SQL.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
SET NULL ON | OFF  
```  
  
## <a name="arguments"></a>Argumentos  
 ATIVADO  
 (O padrão para o driver; o padrão para o Visual FoxPro é desativado.) Especifica que todas as colunas em uma tabela criada com ALTER TABLE e CREATE TABLE permitirão valores nulos. Você pode substituir o suporte a valor nulo para colunas na tabela, incluindo a cláusula NOT NULL nas definições das colunas.  
  
 Também especifica que INSERT-SQL irá inserir valores nulos em todas as colunas não incluídas na cláusula INSERT-SQL VALUE. INSERT-SQL irá inserir valores nulos somente em colunas que permitem valores nulos.  
  
 OFF  
 Especifica que todas as colunas em uma tabela criada com ALTER TABLE e CREATE TABLE não permitirão valores nulos. Você pode designar o suporte a valor nulo para colunas em ALTER TABLE e CREATE TABLE incluindo a cláusula NULL nas definições das colunas.  
  
 Também especifica que INSERT-SQL irá inserir valores em branco em todas as colunas não incluídas na cláusula INSERT-SQL VALUE.  
  
## <a name="remarks"></a>Comentários  
 SET NULL afeta apenas a forma como os valores nulos são suportados por ALTER TABLE, CREATE TABLE e INSERT-SQL. Outros comandos não são afetados por SET NULL.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER TABLE-comando SQL](../../odbc/microsoft/alter-table-sql-command.md)   
 [Comando CREATE TABLE-SQL](../../odbc/microsoft/create-table-sql-command.md)   
 [INSERT – comando SQL](../../odbc/microsoft/insert-sql-command.md)
