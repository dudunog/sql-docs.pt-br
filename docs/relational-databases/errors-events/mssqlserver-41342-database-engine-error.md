---
description: MSSQLSERVER_41342
title: MSSQLSERVER_41342 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 41342 (Database Engine error)
ms.assetid: 28270d98-c543-4e7d-b40c-2200e38dce1c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b236bbc02f7d3bd012d54c8481159e73e5a7adfc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428708"
---
# <a name="mssqlserver_41342"></a>MSSQLSERVER_41342
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|41342|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|HK_HW_NOT_SUPPORTED|  
|Texto da mensagem|O modelo do processador no sistema não dá suporte à criação de *construct*. Esse erro normalmente ocorre com processadores mais antigos.|  
  
## <a name="explanation"></a>Explicação  
As tabelas com otimização de memória exigem um modelo de processador que dá suporte a operações atômicas de comparar-e-trocar em valores de 128 bits, que exigem instrução de assembly CMPXCHG16B. Alguns modelos mais antigos de processadores AMD não dão suporte à instrução CMPXCHG16B. Além disso, alguns ambientes de virtualização não habilitam essa instrução por padrão.  
  
## <a name="user-action"></a>Ação do usuário  
Atualize o processador. Se o processador der suporte à instrução e você estiver executando o SQL Server em uma máquina virtual, altere a configuração para dar suporte à instrução CMPXCHG16B.  
  
## <a name="see-also"></a>Consulte Também  
[OLTP in-memory &#40;Otimização na memória&#41;](~/relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
