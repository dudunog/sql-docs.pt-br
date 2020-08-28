---
description: Cursores de somente avanço
title: Cursores de somente avanço | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], forward-only
- forward-only cursors [ADO]
ms.assetid: 2b1e062f-3294-4a6f-8241-a17045c4df18
author: rothja
ms.author: jroth
ms.openlocfilehash: 1ccf9d679d158b6f89ef6842b427c315078b99f6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991237"
---
# <a name="forward-only-cursors"></a>Cursores de somente avanço
O tipo de cursor padrão típico, chamado de cursor somente encaminhamento (ou não rolável), pode ser movido apenas para frente pelo conjunto de resultados. Um cursor de somente avanço não dá suporte à rolagem (a capacidade de avançar e retroceder no conjunto de resultados); Ele dá suporte apenas à busca de linhas desde o início até o fim do conjunto de resultados. Com alguns cursores de somente avanço (como com a biblioteca de cursores SQL Server), todas as instruções INSERT, Update e Delete feitas pelo usuário atual (ou confirmadas por outros usuários) que afetam as linhas no conjunto de resultados ficam visíveis à medida que as linhas são buscadas. Porém, como o cursor não podem ser revertido, as alterações feitas nas linhas no banco de dados depois que a linha foi buscada não são visíveis pelo cursor.  
  
 Depois que os dados da linha atual são processados, o cursor de somente avanço libera os recursos que foram usados para manter esses dados. Cursores somente de avanço são dinâmicos por padrão, o que significa que todas as alterações são detectadas conforme a linha atual é processada. Isso permite uma abertura do cursor mais rápida e que o conjunto de resultados exiba as atualizações feitas nas tabelas subjacentes.  
  
 Embora os cursores de somente avanço não ofereçam suporte à rolagem regressiva, seu aplicativo pode retornar ao início do conjunto de resultados fechando e reabrendo o cursor. Essa é uma maneira eficaz de trabalhar com pequenas quantidades de dados. Como alternativa, seu aplicativo pode ler o conjunto de resultados uma vez, armazenar os dados em cache localmente e, em seguida, procurar o cache de dados local.  
  
 Se seu aplicativo não exigir a rolagem pelo conjunto de resultados, o cursor de somente avanço será a melhor maneira de recuperar dados rapidamente com a menor quantidade de sobrecarga. Use o **AdOpenForwardOnly CursorTypeEnum** para indicar que você deseja usar um cursor de somente avanço no ADO.  
  
## <a name="see-also"></a>Consulte Também  
 [Cursores estáticos](./static-cursors.md)   
 [Cursores do conjunto de chaves](./keyset-cursors.md)   
 [Cursores dinâmicos](./dynamic-cursors.md)