---
title: Funções CLR definidas pelo usuário | Microsoft Docs
description: SQL Server integração CLR permite que você crie funções de agregação, valores de tabela e valores de escala definidos pelo usuário em qualquer linguagem de programação de .NET Framework.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- building database objects [CLR integration], user-defined functions
- functions [CLR integration]
- common language runtime [SQL Server], user-defined functions
- database objects [CLR integration], user-defined functions
- user-defined functions [CLR integration]
ms.assetid: 6f7491f1-9a46-4146-ae09-056248634de2
author: rothja
ms.author: jroth
ms.openlocfilehash: 0da524de3a21a97daf6e3b2d2e0277631a4467c0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81488255"
---
# <a name="clr-user-defined-functions"></a>Funções CLR definidas pelo usuário
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  As funções definidas pelo usuário são rotinas que podem obter parâmetros, executar cálculos ou outras ações e retornar um resultado. A partir do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], é possível escrever funções definidas pelo usuário em qualquer linguagem de programação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework, como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic .NET ou o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#.  
  
 Há dois tipos de funções: escalar, que retorna um único valor, e com valor de tabela, que retorna um conjunto de linhas.  
  
 A tabela a seguir lista os tópicos desta seção.  
  
 [Funções de valor escalar CLR](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-scalar-valued-functions.md)  
 Abrange requisitos de implementação e exemplos de funções com valor escalar.  
  
 [Funções com valor de tabela CLR](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-table-valued-functions.md)  
 Aborda como implementar e usar funções com valor de tabela (TVFs), além das diferenças entre TVFs CLR e [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 [Agregações CLR definidas pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-functions/clr-user-defined-aggregates.md)  
 Descreve como implementar e usar agregações definidas pelo usuário.  
  
## <a name="see-also"></a>Consulte Também  
 [Funções definidas pelo usuário](../../relational-databases/user-defined-functions/user-defined-functions.md)  
  
  
