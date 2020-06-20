---
title: Solucionar problemas de trabalhos com multisservidor que usam proxies | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- proxies [SQL Server Agent], multiserver jobs
- jobs [SQL Server Agent], multiserver jobs using proxies
ms.assetid: fc579bd3-010c-4f72-8b5c-d0cc18a1f280
author: stevestein
ms.author: sstein
ms.openlocfilehash: 19de975ef5e1f22c93cec72a5014a01da5b03dd8
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067471"
---
# <a name="troubleshoot-multiserver-jobs-that-use-proxies"></a>Solucionar problemas de trabalhos multisservidor que usam proxies
  Trabalhos distribuídos cujas etapas estejam associadas a um proxy são executados no contexto da conta proxy no servidor de destino. Se as etapas de trabalho que usam contas proxy falharem ao serem baixadas do servidor mestre, verifique a coluna **error_message** da tabela **sysdownloadlist** no banco de dados **msdb** quanto às seguintes mensagens de erro:  
  
-   "A etapa do trabalho requer uma conta proxy. Entretanto, a verificação de proxy está desabilitada no servidor de destino."  
  
     Para resolver esse erro, defina o **\ HKEY_LOCAL_MACHINE \SOFTWARE\MICROSOFT\MICROSOFT SQL Server\MSSQL.** _ \<n_> **\SQLServerAgent\AllowDownloadedJobsToMatchProxyName** subchave do registro como **1 (true)**. Por padrão, essa subchave é definida como **0** ( `false` ). O valor de **MSSQL.**\<*n*> é o nome da instância; por exemplo, **MSSQL. 1** ou **MSSQL. 3**.  
  
-   "Proxy não localizado."  
  
     Para resolver este erro, verifique se existe uma conta proxy no servidor de destino com o mesmo nome da conta proxy do servidor mestre sob a qual a etapa de trabalho é executada.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../includes/ssnoteregistry-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Criar um ambiente multisservidor](create-a-multiserver-environment.md)  
  
  
