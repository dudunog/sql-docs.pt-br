---
title: MSSQLSERVER_9955 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 9955 (Database Engine error)
ms.assetid: 77f30570-7790-4747-b372-eac71c036e19
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a092a7228f5ec70247e38cf39073d946de0e56ea
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62761632"
---
# <a name="mssqlserver_9955"></a>MSSQLSERVER_9955
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|9955|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|FTXT2_MSSEARCHACCESSDENY|  
|Texto da mensagem|Falha no SQL Server ao criar o pipe nomeado '%ls' para se comunicar com o daemon de filtro de texto completo (erro do Windows: %d). Já existe um pipe nomeado para um processo de host do daemon de filtro, o sistema tem recursos insuficientes ou ocorreu uma falha na pesquisa de SID (número de identificação de segurança) referente ao grupo de contas do daemon de filtro. Para resolver esse erro, encerre quaisquer processos do daemon de filtro de texto completo e, se necessário, reconfigure a conta de serviço iniciador de daemon de texto completo.|  
  
## <a name="explanation"></a>Explicação  
 Essa mensagem é exibida porque o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não conseguiu criar um pipe nomeado para se comunicar com o daemon de filtro de texto completo. Já existe um pipe nomeado para um processo de host do daemon de filtro, o sistema tem recursos insuficientes ou ocorreu uma falha na pesquisa de SID (número de identificação de segurança) referente ao grupo de contas do daemon de filtro.  
  
## <a name="user-action"></a>Ação do usuário  
 Para corrigir esse erro, encerre todos os processos do daemon de filtro de texto completo em execução e, se necessário, reconfigure a conta de host do daemon de texto completo usando o SQL Server Configuration Manager.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Configuration Manager](../sql-server-configuration-manager.md)   
 [Definir a conta de serviço para o iniciador do daemon de filtro de texto completo](../search/set-the-service-account-for-the-full-text-filter-daemon-launcher.md)   
 [Pesquisa de texto completo](../search/full-text-search.md)  
  
  
