---
title: Acessando tipos definidos pelo usuário em ADO.NET | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- UDTs [CLR integration], ADO.NET
- user-defined types [CLR integration], ADO.NET
ms.assetid: 4b0d876c-8066-490e-8e18-327c0e942b19
author: rothja
ms.author: jroth
ms.openlocfilehash: a94e333ad743ed07dff6b973ebfe227312a1cab2
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970756"
---
# <a name="accessing-user-defined-types-in-adonet"></a>Acessando tipos definidos pelo usuário no ADO.NET
  Os tipos definidos pelo usuário (UDTs) são escritos usando qualquer um dos idiomas compatíveis com o [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework Common Language Runtime (CLR) que produz código verificável. Isso inclui o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# e o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic. Os UDTs permitem armazenar objetos e estruturas de dados personalizadas em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os dados são expostos como membros públicos de uma classe ou estrutura do .NET Framework e os comportamentos são definidos pelos métodos da classe ou estrutura. Um UDT pode ser usado como definição de coluna de uma tabela, como uma variável em um lote [!INCLUDE[tsql](../../includes/tsql-md.md)], ou como um argumento de uma função [!INCLUDE[tsql](../../includes/tsql-md.md)] ou um procedimento armazenado.  
  
 No ADO.NET, o provedor `System.Data.SqlClient` expõe UDTs dos seguintes modos:  
  
-   Por meio do `System.Data.SqlClient.SqlDataReader` como um objeto.  
  
-   Por meio do `SqlDataReader` como bytes brutos.  
  
-   Como um parâmetro de um objeto `System.Data.SqlClient.SqlParameter`.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Recuperando dados UDT](accessing-user-defined-types-retrieving-udt-data.md)  
 Descreve como recuperar dados UDT e como especificar parâmetros.  
  
 [Atualizando colunas UDT com DataAdapters](accessing-user-defined-types-updating-udt-columns-with-dataadapters.md)  
 Descreve como trabalhar com UDTs em `DataSets` e como atualizar dados UDT usando `DataAdapters`.  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos CLR definidos pelo usuário](clr-user-defined-types.md)  
  
  
