---
title: Opção de configuração de servidor transform noise words | Microsoft Docs
description: Saiba mais sobre a opção "transformar palavras de ruído". Veja como ela pode ser útil em algumas consultas de texto completo do SQL Server que incluem palavras de ruído (palavras irrelevantes).
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- full-text queries [SQL Server], performance
- transform noise words option
- noise words [full-text search]
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 69bd388e-a86c-4de4-b5d5-d093424d9c57
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 401637b4c23ddbcd2918f4d0d3cf5ff224bea8cc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85763965"
---
# <a name="transform-noise-words-server-configuration-option"></a>Opção de configuração de servidor para transformar palavras de ruído
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Use a opção de configuração de servidor **transformar palavras de ruído** para suprimir uma mensagem de erro se palavras de ruído, ou seja, [palavras irrelevantes](../../relational-databases/search/configure-and-manage-stopwords-and-stoplists-for-full-text-search.md), levarem uma operação booliana em uma consulta de texto completo a retornar zero linhas. Essa opção é útil para consultas de texto completo que usam o predicado CONTAINS em que as operações boolianas ou operações NEAR incluem palavras de ruído. Os valores possíveis são descritos na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|0|As palavras de ruído (ou palavras irrelevantes) não são transformadas. Quando uma consulta de texto completo contiver palavras de ruído, a consulta não retornará nenhuma linha e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerará um aviso. Esse é o comportamento padrão.<br /><br /> Observação: o aviso é um aviso em tempo de execução. Portanto, se a cláusula de texto completo na consulta não for executada, o aviso não será gerado. Para uma consulta local, apenas um aviso é gerado, mesmo quando há várias cláusulas de consulta de texto completo. Para uma consulta remota, o servidor vinculado pode não retransmitir o erro; portanto, o aviso pode não ser gerado.|  
|1|As palavras de ruído (ou palavras irrelevantes) são transformadas. Elas são ignoradas e o resto da consulta é avaliado.<br /><br /> Se forem especificadas palavras de ruído em uma condição de proximidade, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] as removerá. Por exemplo, a palavra de ruído `is` é removida de `CONTAINS(<column_name>, 'NEAR (hello,is,goodbye)')`, transformando a consulta de pesquisa em `CONTAINS(<column_name>, 'NEAR(hello,goodbye)')`. Observe que `CONTAINS(<column_name>, 'NEAR(hello,is)')` seria transformada simplesmente em `CONTAINS(<column_name>, hello)` porque há apenas um termo de pesquisa válido.|  
  
## <a name="effects-of-the-transform-noise-words-setting"></a>Efeitos da Configuração transformar palavras de ruído  
 Esta seção ilustra o comportamento de consultas que contêm uma palavra de ruído, “`the`”, nas configurações alternativas de **transformar palavras de ruído**.  Parte-se do pressuposto de que as cadeias de consulta de texto completo de exemplo são executadas em uma linha de tabela que contém os seguintes dados: `[1, "The black cat"]`.  
  
> [!NOTE]  
>  Todos esses cenários podem gerar um aviso de palavra de ruído.  
  
-   Com transformar palavras de ruído definido como 0:  
  
    |Cadeia de consulta|Result|  
    |------------------|------------|  
    |"`cat`" AND "`the`"|Nenhum resultado (O comportamento é o mesmo para "`the`" AND "`cat`".)|  
    |"`cat`" NEAR "`the`"|Nenhum resultado (O comportamento é o mesmo para "`the`" NEAR "`cat`".)|  
    |"`the`" AND NOT "`black`"|Nenhum resultado|  
    |"`black`" AND NOT "`the`"|Nenhum resultado|  
  
-   Com transformar palavras de ruído definido como 1:  
  
    |Cadeia de consulta|Result|  
    |------------------|------------|  
    |"`cat`" AND "`the`"|Ocorrência da linha com ID 1|  
    |"`cat`" NEAR "`the`"|Ocorrência da linha com ID 1|  
    |"`the`" AND NOT "`black`"|Nenhum resultado|  
    |"`black`" AND NOT "`the`"|Ocorrência da linha com ID 1|  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir define **transformar palavras de ruído** como `1`.  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
GO  
sp_configure 'transform noise words', 1;  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [CONTAINS &#40;Transact-SQL&#41;](../../t-sql/queries/contains-transact-sql.md)  
  
  
