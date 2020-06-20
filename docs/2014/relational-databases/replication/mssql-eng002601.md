---
title: MSSQL_ENG002601 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG002601 error
ms.assetid: 657c3ae6-9e4b-4c60-becc-4caf7435c1dc
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: d8faca0230b77cb7ff37e9e936bcc68c1e715d90
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049329"
---
# <a name="mssql_eng002601"></a>MSSQL_ENG002601
    
## <a name="message-details"></a>Detalhes da mensagem  
  
|||  
|-|-|  
|Nome do Produto|SQL Server|  
|ID do evento|2601|  
|Origem do Evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbólico|N/D|  
|Texto da mensagem|Não é possível inserir uma linha de chave duplicada no objeto '%.*ls' com o índice exclusivo '%.\*ls'.|  
  
## <a name="explanation"></a>Explicação  
 Esse é um erro geral que pode ocorrer independentemente de um banco de dados ser ou não replicado. Nos bancos de dados replicados, esse erro geralmente ocorre porque as chaves primárias não foram gerenciadas corretamente na topologia. Em um ambiente distribuído, é essencial garantir que o mesmo valor não seja inserido em uma coluna de chave primária ou qualquer outra coluna exclusiva em mais de um nó. As causas possíveis podem ser:  
  
-   Inserções e atualizações em uma linha estão acontecendo em mais de um nó. A replicação de mesclagem e as assinaturas atualizáveis para replicação transacional oferecem detecção e resolução de conflitos, mas ainda é melhor inserir ou atualizar uma determinada linha apenas em um nó. O ponto a ponto transacional não oferece detecção e resolução de conflitos. Ele exige que as inserções e as atualizações sejam particionadas.  
  
-   Uma linha foi inserida em um Assinante que deveria ser somente leitura. Assinantes de publicações de instantâneo devem ser tratados como somente leitura, do mesmo modo que Assinantes de publicações transacionais, exceto se forem usadas assinaturas atualizáveis ou replicação transacional ponto a ponto.  
  
-   Uma tabela com uma coluna de identidade está sendo usada, mas a coluna não é gerenciada apropriadamente.  
  
-   Na replicação de mesclagem, esse erro também pode ocorrer durante uma inserção em uma tabela do sistema **MSmerge_contents**; o erro gerado é semelhante a: Não foi possível inserir uma linha de chave duplicada no objeto 'MSmerge_contents' com índice exclusivo 'ucl1SycContents'.  
  
## <a name="user-action"></a>Ação do usuário  
 A ação necessária depende do motivo que levou à ocorrência do erro:  
  
-   Inserções e atualizações em uma linha estão acontecendo em mais de um nó.  
  
     Independentemente do tipo de replicação usado, recomendamos o particionamento das atualizações e inserções sempre que possível para reduzir o processamento necessário para a detecção e a resolução de conflitos. Para a replicação transacional ponto a ponto, é necessário o particionamento de inserções e atualizações. Para obter mais informações, consulte [Peer-to-Peer Transactional Replication](transactional/peer-to-peer-transactional-replication.md).  
  
-   Uma linha foi inserida em um Assinante que deveria ser somente leitura.  
  
     Não insira ou atualize linhas no Assinante, exceto se estiver usando a replicação de mesclagem, a replicação transacional com assinaturas atualizáveis ou a replicação transacional ponto a ponto.  
  
-   Uma tabela com uma coluna de identidade está sendo usada, mas a coluna não é gerenciada apropriadamente.  
  
     Para replicação de mesclagem e replicação transacional com assinaturas atualizáveis, as colunas de identidade devem ser gerenciadas automaticamente por replicação. Para replicação transacional ponto a ponto, elas devem ser gerenciadas manualmente. Para obter mais informações, consulte [Replicar colunas de identidade](publish/replicate-identity-columns.md).  
  
-   O erro ocorre durante uma inserção na tabela do sistema **MSmerge_contents**.  
  
     O erro pode ocorrer devido a um valor incorreto para a propriedade de filtro de junção **join_unique_key**. Essa propriedade só deverá ser definida como TRUE se a coluna associada na tabela pai for exclusiva. Se a propriedade for definida como TRUE, mas a coluna não for exclusiva, esse erro será gerado. Para obter mais informações sobre como definir essa propriedade, consulte [Definir e modificar um filtro de junção entre artigos de mesclagem](publish/define-and-modify-a-join-filter-between-merge-articles.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de erros e eventos &#40;Replicação&#41;](errors-and-events-reference-replication.md)  
  
  
