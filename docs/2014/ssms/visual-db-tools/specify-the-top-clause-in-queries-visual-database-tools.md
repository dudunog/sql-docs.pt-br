---
title: Especificar a cláusula TOP em consultas (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- TOP clause, queries
- percentage of rows returned [SQL Server]
- number of rows
- search conditions [SQL Server], TOP clause
- restricting rows returned
- search criteria [SQL Server], limiting rows returned
- inspecting portion of results
- limiting rows returned
- search criteria [SQL Server], TOP clause
ms.assetid: ba7d7c10-9bb3-4d9b-90b0-5fa94ecae59b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7f9587a5e653d2df8cbe169fe5030542b86d8aaf
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63194967"
---
# <a name="specify-the-top-clause-in-queries-visual-database-tools"></a>Especificar a cláusula TOP em consultas (Visual Database Tools)
  A cláusula TOP retorna somente as primeiras linhas *n* ou *n percent* de uma consulta. A cláusula TOP é útil quando se pretende inspecionar uma parte de seus resultados para descobrir se sua consulta faz o esperado sem despender os recursos necessários para retornar todos os resultados da consulta.  
  
### <a name="to-specify-the-top-clause-in-queries"></a>Para especificar a cláusula TOP em consultas  
  
1.  Abra uma consulta no Gerenciador de Soluções ou crie uma consulta nova.  
  
2.  No menu **Exibir** , clique em **Janela Propriedades**.  
  
3.  Na **Janela de Propriedades**, localize e expanda a propriedade **Especificação Top** .  
  
4.  Clique na propriedade filho **(Top)** e defina-a como **Sim**.  
  
5.  Na propriedade filho **Expressão** , digite uma expressão com resultado numérico (por exemplo, "10" ou "2*5").  
  
6.  Clique na propriedade filho **Porcentagem** e indique se a propriedade **Expressão** deverá ser tratada como percentual de todas as linhas retornadas (Sim) ou como o número absoluto de linhas retornadas (Não).  
  
7.  Se sua consulta usar a cláusula ORDER BY, clique na propriedade filho **Com Ligações** e escolha **Sim** para exibir todas as linhas de um grupo se apenas parte do grupo estiver incluída ou escolha **Não** para truncar as linhas.  
  
 À medida que você trabalha com o procedimento precedente, observe que a cláusula TOP, exibida no painel SQL, altera-se para refletir as configurações atuais das propriedades.  
  
> [!NOTE]  
>  Além disso, você pode alterar os valores das propriedades filho de **Especificação Top** editando a cláusula TOP no painel SQL.  
  
## <a name="see-also"></a>Consulte Também  
 [Tópicos de instruções sobre como criar consultas e exibições &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [Propriedades de consulta &#40;Visual Database Tools&#41;](query-properties-visual-database-tools.md)  
  
  
