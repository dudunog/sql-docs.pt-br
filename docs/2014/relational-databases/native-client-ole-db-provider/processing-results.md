---
title: Processar resultados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, results processing
- OLE DB, processing results
- rowsets [SQL Server], results processing
- results [SQL Server Native Client]
ms.assetid: 20887ac4-f649-4e7f-92e6-f929e2e70952
author: rothja
ms.author: jroth
ms.openlocfilehash: b9e5bf00b4d2e554536c9f2ba1a328390b93a8a6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056014"
---
# <a name="processing-results"></a>Processando resultados
  Caso um objeto de conjunto de linhas seja produzido pela execução de um comando ou pela geração direta de um objeto de conjunto de linhas no provedor, o consumidor precisa recuperar e acessar dados no conjunto de linhas.  
  
 Conjuntos de linhas são os objetos centrais que permitem ao provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client expor dados em forma tabular. Conceitualmente, um conjunto de linhas é um conjunto de linhas em que cada linha tem dados de coluna. Um objeto de conjunto de linhas expõe interfaces como **IRowset** (contém métodos para buscar linhas no conjunto sequencialmente), **IAccessor** (permite a definição de um grupo de associações de coluna que descrevem a forma como dados tabulares são associados a variáveis de programa do consumidor), **IColumnsInfo** (fornece informações sobre colunas no conjunto de linhas) e **IRowsetInfo** (fornece informações sobre o conjunto de linhas).  
  
 Um consumidor pode chamar o método **IRowset::GetData** para recuperar uma linha de dados do conjunto de linhas em um buffer. Antes de **GetData** ser chamado, o consumidor descreve o buffer usando um conjunto de estruturas DBBINDING. Cada associação descreve como uma coluna em um conjunto de linhas é armazenada em um buffer de consumidor e contém o seguinte:  
  
-   Ordinal da coluna (ou parâmetro) a que a associação se aplica.  
  
-   Informações sobre a associação (por exemplo, valor de dados, comprimento dos dados e o status da associação).  
  
-   Informações sobre o que é deslocado no buffer para cada uma das partes.  
  
-   Comprimento e tipo dos valores de dados como se apresentam no buffer de consumidor.  
  
 Ao obter os dados, o provedor usa informações de cada associação para determinar onde e como recuperar dados do buffer de consumidor. Ao definir dados no buffer de consumidor, o provedor usa informações de cada associação para determinar onde e como retornar dados no buffer.  
  
 Depois que as estruturas DBBINDING são especificadas, um acessador é criado (**IAccessor::CreateAccessor**). Um acessador é uma coleção de associações, sendo usado para obter ou definir os dados no buffer de consumidor.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando um aplicativo de provedor de OLE DB de SQL Server Native Client](creating-a-sql-server-native-client-ole-db-provider-application.md)   
 [Tópicos de instruções do OLE DB](../native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
