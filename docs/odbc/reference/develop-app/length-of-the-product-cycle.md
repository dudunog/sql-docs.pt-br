---
description: Comprimento do ciclo do produto
title: Comprimento do ciclo do produto | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], product cycle
- length of the product cycle [ODBC]
ms.assetid: 4d08d886-6d8b-40fd-8544-13032f4bf6c7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d1484079a09d10864e0563db95208e926a959d6d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476578"
---
# <a name="length-of-the-product-cycle"></a>Comprimento do ciclo do produto
A pergunta final sobre a interoperabilidade é o tempo. O desenvolvimento de um aplicativo interoperável geralmente demora mais do que desenvolver um noninteroperable. O motivo é que o aplicativo deve verificar os recursos do DBMS, executar as mesmas tarefas de forma diferente para DBMSs diferentes, contornar a funcionalidade com suporte de alguns DBMSs, mas não outros, e assim por diante.  
  
 Além do tempo de desenvolvimento, a vida útil do produto deve ser considerada. Se o aplicativo for projetado para ser usado uma vez, como um aplicativo que transfere dados ao migrar de um DBMS para outro, não há nenhum ponto de torná-lo interoperável. O aplicativo será usado uma vez e descartado.  
  
 Se o aplicativo existir por muito tempo, poderá ser mais fácil de manter como um aplicativo interoperável. Isso é verdadeiro mesmo para aplicativos personalizados que têm um único DBMS como um destino. O motivo é que o código interoperável usa um subconjunto limitado de recursos de banco de dados. O driver é necessário para manter esses recursos disponíveis, mesmo diante de alterações no DBMS subjacente. Portanto, o código interoperável pode mudar a carga de coping com alterações no DBMS do desenvolvedor de aplicativos para o desenvolvedor de driver.
