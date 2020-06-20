---
title: MSSQLSERVER_7711 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 7711 (Database Engine error)
ms.assetid: a5c7cd6e-18d6-47ef-902b-db9dd64bba34
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 24aed847621d485321483c76973d3ab49ba5b906
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85053755"
---
# <a name="mssqlserver_7711"></a>MSSQLSERVER_7711
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|7711|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PRT_RANGE_OVERLAP|  
|Texto da mensagem|A opção DATA_COMPRESSION foi especificada mais de uma vez para a tabela ou o índice ou para uma de suas partições.|  
  
## <a name="explanation"></a>Explicação  
 Ocorreu um erro na opção DATA_COMPRESSION em uma das seguintes instruções:  
  
-   CREATE TABLE  
  
-   ALTER TABLE  
  
-   CREATE INDEX  
  
-   ALTER INDEX  
  
 Se a tabela ou o índice citado for particionado, a opção DATA_COMPRESSION foi listada mais de uma vez para pelo menos uma das partições. Se a tabela ou o índice não for particionado, a opção DATA_COMPRESSION foi citada mais de uma vez.  
  
## <a name="user-action"></a>Ação do usuário  
 Para uma tabela ou um índice particionado, verifique se a opção DATA_COMPRESSION está especificada somente uma vez para cada partição. Para uma tabela ou um índice não particionado, use a opção DATA_COMPRESSION somente uma vez na instrução.  
  
  
