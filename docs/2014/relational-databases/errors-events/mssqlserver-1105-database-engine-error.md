---
title: MSSQLSERVER_1105 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1105 (Database Engine error)
ms.assetid: e7f4ad02-8c7f-4bb9-9781-2c86253f2138
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5ee98c0144d492b74e8ddc2785b21b76a363eb92
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62915930"
---
# <a name="mssqlserver_1105"></a>MSSQLSERVER_1105
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|1105|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|NO_MORE_SPACE_IN_FG|  
|Texto da mensagem|Não foi possível alocar espaço ao objeto '%.*ls'%.\*ls no banco de dados '%.\*ls' porque o grupo de arquivos '%.\*ls' está cheio. Crie espaço em disco excluindo arquivos desnecessários, descartando objetos no grupo de arquivos, adicionando arquivos ao grupo de arquivos ou definindo o aumento automático para arquivos existentes no grupo de arquivos.|  
  
## <a name="explanation"></a>Explicação  
 Não há espaço disponível em disco em um grupo de arquivos.  
  
## <a name="user-action"></a>Ação do usuário  
 As seguintes ações podem criar espaço disponível no grupo de arquivos:  
  
-   Ative o aumento automático.  
  
-   Adicione mais arquivos ao grupo de arquivos.  
  
-   Libere espaço em disco descartando índices ou tabelas que não sejam mais necessários.  
  
-   Para obter mais informações, consulte “Solucionando problemas de espaço de dados insuficiente no disco” nos Manuais Online do SQL Server.  
  
> [!NOTE]  
>  Quando um índice encontra-se em vários arquivos, o `ALTER INDEX REORGANIZE` pode retornar um erro 1105 quando um desses arquivos estiver cheio. O processo de reorganização é bloqueado quando o processo tenta mover as linhas para o arquivo cheio. Como alternativa a esta limitação, execute um `ALTER INDEX REBUILD` em vez de `ALTER INDEX REORGANIZE` ou aumente o limite de crescimento dos arquivos cheios.  
  
  
