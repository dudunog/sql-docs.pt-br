---
title: Gerenciando transações (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, transactions
- XMLA, transactions
- explicit transactions [XMLA]
- implicit transactions
- transactions [XML for Analysis]
- rolling back transactions, XMLA
- reference counts [XML for Analysis]
- committing transactions
- starting transactions
ms.assetid: f5112e01-82f8-4870-bfb7-caa00182c999
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ad8a77d1d8552dc811c1232afb53c142452658db
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62727185"
---
# <a name="managing-transactions-xmla"></a>Gerenciando transações (XMLA)
  Cada comando XML for Analysis (XMLA) enviado para uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é executado dentro do contexto de uma transação na sessão implícita ou explícita atual. Para gerenciar cada uma dessas transações, use os comandos [BeginTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/begintransaction-element-xmla), [CommitTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/committransaction-element-xmla)e [RollbackTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/rollbacktransaction-element-xmla) . Ao usar esses comandos, você poderá criar transações implícitas ou explícitas, alterar a contagem de referência de transação, além de iniciar, confirmar ou reverter transações.  
  
## <a name="implicit-and-explicit-transactions"></a>Transações implícitas e explícitas  
 Uma transação é implícita ou explícita:  
  
 **Transação implícita**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Cria uma transação *implícita* para um comando XMLA se o `BeginTransaction` comando não especificar o início de uma transação. O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sempre confirma uma transação implícita se o comando é bem-sucedido, e reverte uma transação implícita se o comando falha.  
  
 **Transação explícita**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]Cria uma transação *explícita* se o `BeginTransaction` comando iniciar uma transação. No entanto, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] também confirmará uma transação explícita se um comando `CommitTransaction` for enviado e reverterá uma transação explícita se um comando `RollbackTransaction` for enviado.  
  
 Além disso, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] reverterá transações implícitas e explícitas se a sessão atual terminar antes da conclusão da transação ativa.  
  
## <a name="transactions-and-reference-counts"></a>Transações e contagens de referência  
 O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mantém uma contagem de referência de transação para cada sessão. No entanto, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não dá suporte a transações aninhadas já que somente uma transação ativa é mantida por sessão. Se a sessão atual não tiver uma transação ativa, a contagem de referência de transação será definida como zero.  
  
 Em outras palavras, cada comando `BeginTransaction` incrementa a contagem de referência em um, enquanto cada comando `CommitTransaction` diminui a contagem de referência em um. Se um comando `CommitTransaction` definir a contagem de transação como zero, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] confirmará a transação.  
  
 No entanto, o comando `RollbackTransaction` reverte a transação ativa a despeito do valor atual da contagem de referência de transação. Em outras palavras, um único comando `RollbackTransaction` reverte a transação ativa, não importando quantos comandos `BeginTransaction` ou comandos `CommitTransaction` tenham sido enviados e define a contagem de referência de transação como zero.  
  
## <a name="beginning-a-transaction"></a>Iniciando uma transação  
 O comando `BeginTransaction` inicia uma transação explícita na sessão atual e incrementa a contagem de referência de transação para a sessão atual em um. Todos os comandos subsequentes serão considerados como da transação ativa, até que comandos `CommitTransaction` suficientes sejam enviados para a confirmação da transação ativa ou até que um único comando `RollbackTransaction` seja enviado para reverter a transação ativa.  
  
## <a name="committing-a-transaction"></a>Confirmando uma transação  
 O comando `CommitTransaction` comando confirma os resultados de comandos executados após a execução do comando `BeginTransaction` na sessão atual. Cada comando `CommitTransaction` diminui a contagem de referência para transações ativas em uma sessão. Se um comando `CommitTransaction` definir a contagem de referência como zero, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] confirmará a transação ativa. Se não houver transação ativa (em outras palavras, se a contagem de referência de transação da sessão atual já tiver sido definida como zero), um comando `CommitTransaction` resultará em um erro.  
  
## <a name="rolling-back-a-transaction"></a>Revertendo uma transação  
 O comando `RollbackTransaction` comando reverte os resultados de comandos executados após a execução do comando `BeginTransaction` na sessão atual. O comando `RollbackTransaction` reverte a transação ativa, a despeito da contagem de referência de transação atual, e define a contagem de referência de transação como zero. Se não houver transação ativa (em outras palavras, se a contagem de referência de transação da sessão atual já tiver sido definida como zero), um comando `RollbackTransaction` resultará em um erro.  
  
## <a name="see-also"></a>Consulte Também  
 [Desenvolvendo com XMLA no Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
