---
description: MSSQLSERVER_9532
title: MSSQLSERVER_9532 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 9532 (Database Engine error)
ms.assetid: ab95cce8-4f97-4aea-a746-a73eea7c9aab
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4843631d2e387818b40520e0076cc22b32b10bc9
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491104"
---
# <a name="mssqlserver_9532"></a>MSSQLSERVER_9532
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|9532|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|XMLERR_COLUMNSET_CANNOT_CONVERT_FROM_TO|  
|Texto da mensagem|Na operação de consulta/DML envolvendo o conjunto de colunas '%.*ls', houve falha na conversão ao converter do tipo de dados '%ls' no tipo de dados '%ls' da coluna '%.\*ls'.|  
  
## <a name="explanation"></a>Explicação  
Um conjunto de colunas é uma representação em XML sem-tipo que combina algumas das colunas de uma tabela em uma saída estruturada. Ao inserir ou atualizar valores de coluna esparsos no conjunto de colunas XML, os valores inseridos nas colunas esparsas subjacentes são convertidos implicitamente do tipo de dados **xml**. O valor fornecido não pode ser convertido ao tipo de dados da coluna.  
  
## <a name="user-action"></a>Ação do usuário  
Como não foi possível converter implicitamente o valor fornecido, talvez seja uma entrada inválida. Corrija o erro e tente novamente. Se o valor estiver correto, modifique a instrução para usar as colunas individuais em vez do conjunto de colunas. Isso permitirá que você converta o valor explicitamente no tipo de dados correto.  
  
