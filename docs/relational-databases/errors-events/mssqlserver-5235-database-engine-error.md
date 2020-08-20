---
description: MSSQLSERVER_5235
title: MSSQLSERVER_5235 | Microsoft Docs
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 5235 (Database Engine error)
ms.assetid: 1aa7e6a5-7ccb-43c8-a1fd-d50e92e0a798
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 9086a2ba077c776c0d36a6ab5e7e2cafc97a688f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88470979"
---
# <a name="mssqlserver_5235"></a>MSSQLSERVER_5235
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|5235|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|DBCC4_ERRORLOG_SUMMARY_PREMATURE_TERMINATION|  
|Texto da mensagem|[EMERGENCY] DBCC DBCC_COMMAND_DETAILS executado por USER_NAME foi encerrado de forma anormal devido ao estado de erro ERROR_STATE. Tempo decorrido: HOURS horas MINUTES minutos SECONDS segundos.|  
  
## <a name="explanation"></a>Explicação  
Essa é a mensagem de resumo que o DBCC grava no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando ocorre um encerramento inesperado durante a execução do comando. O estado de erro informado na mensagem define o tipo de encerramento inesperado.  
  
A tabela a seguir lista e define os estados de erro.  
  
|Estado de erro|Definição|  
|---------------|--------------|  
|Estado 1|A instrução foi encerrada devido a um dano fatal nos metadados. Essa mensagem é acompanhada por uma ou mais ocorrências do erro 8930.|  
|Estado 2|A instrução foi encerrada devido a uma falha de verificação interna. Essa mensagem é acompanhada por uma ou mais ocorrências do erro 8967.|  
|Estado 3|Falha nas verificações básicas de tabelas do sistema do mecanismo de armazenamento principal. Essa mensagem é acompanhada por uma ou mais instâncias do erro [7984](../../relational-databases/errors-events/mssqlserver-7984-database-engine-error.md), 7985, [7986](~/relational-databases/errors-events/mssqlserver-7986-database-engine-error.md), [7987](~/relational-databases/errors-events/mssqlserver-7987-database-engine-error.md) ou [7988](~/relational-databases/errors-events/mssqlserver-7988-database-engine-error.md).|  
|Estado 4|Ocorreu uma falha no reparo do modo de emergência DBCC porque não foi possível iniciar o banco de dados após a recriação do log de transações. Essa mensagem é acompanhada pelo erro 7909.|  
|Estado 5|Ocorreu uma falha de asserção ou uma violação de acesso durante a execução do comando.|  
|Estado 6|Ocorreu uma falha desconhecida que encerrou o comando DBCC inesperadamente.|  
|Estado 7|Um encerramento anormal devido ao erro na réplica (Sempre ativo).|  
  
## <a name="user-action"></a>Ação do usuário  
A tabela a seguir descreve a ação do usuário apropriada para o estado de erro especificado.  
  
|Estado de erro|Ação do usuário|  
|---------------|---------------|  
|Estado 1|Restaure do backup.|  
|Estado 2|Entre em contato com o Suporte e Atendimento ao Cliente [!INCLUDE[msCoName](../../includes/msconame-md.md)] (CSS).|  
|Estado 3|Restaure do backup.|  
|Estado 4|Restaure do backup.|  
|Estado 4|Entre em contato com o CSS.|  
|Estado 6|Execute o comando novamente. Se o problema persistir, entre em contato com o CSS.|  
  
## <a name="see-also"></a>Consulte Também  
[DBCC &#40;Transact-SQL&#41;](~/t-sql/database-console-commands/dbcc-transact-sql.md)  
  
