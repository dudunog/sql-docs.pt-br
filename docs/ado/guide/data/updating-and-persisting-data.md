---
description: Atualização e persistência de dados
title: Atualizando e mantendo dados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updating data [ADO]
- data updates [ADO]
- ADO, updating data
ms.assetid: 8dc27274-4f96-43d1-913c-4ff7d01b9a27
author: rothja
ms.author: jroth
ms.openlocfilehash: 05ca0196ef59df1f67d5f65f3abc52133b81869a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979167"
---
# <a name="updating-and-persisting-data"></a>Atualização e persistência de dados
Os capítulos anteriores discutiram como usar o ADO para obter dados em uma fonte de dados, como mover-se nos dados e até mesmo como editar os dados. É claro que, se o objetivo do seu aplicativo for permitir que os usuários façam alterações nos dados, você precisará entender como salvar essas alterações. Você pode persistir as alterações do **conjunto de registros** em um arquivo usando o método **Save** ou pode enviar as alterações de volta à fonte de dados para armazenamento usando os métodos **Update** ou **UpdateBatch** .  
  
 Nos capítulos anteriores, você alterou os dados em várias linhas do **conjunto de registros**. O ADO dá suporte a duas noções básicas relacionadas à adição, exclusão e modificação de linhas de dados.  
  
 A primeira noção é que as alterações não são feitas imediatamente no **conjunto de registros**; em vez disso, eles são feitos em um *buffer de cópia*interno. Se você decidir que não deseja as alterações, as modificações no buffer de cópia serão descartadas. Se você decidir manter as alterações, as alterações no buffer de cópia serão aplicadas ao conjunto de **registros**.  
  
 A segunda noção é que as alterações são propagadas para a fonte de dados assim que você declara o trabalho em uma linha concluída (ou seja, o modo *imediato* ) ou todas as alterações em um conjunto de linhas são coletadas até que você declare o trabalho para o conjunto concluído (ou seja, o modo de *lote* ). A propriedade **LockType** determina quando as alterações são feitas na fonte de dados subjacente. **adLockOptimistic** ou **adLockPessimistic** especifica o modo imediato, enquanto **adLockBatchOptimistic** especifica o modo de lote. A propriedade **CursorLocation** pode afetar quais configurações **LockType** estão disponíveis. Por exemplo, a configuração **adLockPessimistic** não terá suporte se a propriedade **CursorLocation** estiver definida como **adUseClient**.  
  
 No modo imediato, cada invocação do método **Update** propaga as alterações para a fonte de dados. No modo de lote, cada invocação de **atualização** ou movimento da posição de linha atual salva as alterações no buffer de cópia, mas somente o método **UpdateBatch** propaga as alterações para a fonte de dados.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Atualizando dados](../../../ado/guide/data/updating-data.md)  
  
-   [Persistência de dados](../../../ado/guide/data/persisting-data.md)
