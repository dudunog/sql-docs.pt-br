---
description: dbo.syscategories (Transact-SQL)
title: Categorias de dbo.sys(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dbo.syscategories_TSQL
- syscategories
- syscategories_TSQL
- dbo.syscategories
dev_langs:
- TSQL
helpviewer_keywords:
- syscategories system table
ms.assetid: eb2cb75c-dc58-4a5b-b329-664e9fe20ce0
author: cawrites
ms.author: chadam
ms.openlocfilehash: af14c2f0eee78a52e54efebb78f7555c160befdb
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98094842"
---
# <a name="dbosyscategories-transact-sql"></a>dbo.syscategories (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contém as categorias usadas pelo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para organizar trabalhos, alertas e operadores. Essa tabela é armazenada no banco de dados **msdb** .  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**category_id**|**int**|ID da categoria|  
|**category_class**|**int**|Tipo de item na categoria:<br /><br /> **1** = trabalho<br /><br /> **2** = alerta<br /><br /> **3** = operador|  
|**category_type**|**tinyint**|Tipo de categoria:<br /><br /> **1** = local<br /><br /> **2** = multisservidor<br /><br /> **3** = nenhum|  
|**name**|**sysname**|Nome da categoria|  
  
  
