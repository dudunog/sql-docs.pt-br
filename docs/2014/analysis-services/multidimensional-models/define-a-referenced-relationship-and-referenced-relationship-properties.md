---
title: Definir uma relação referenciada e propriedades de relação referenciadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- referenced dimension relationship
- relationships [Analysis Services], referenced dimensions
ms.assetid: 5bb44b41-635b-4398-8fe9-0bfbb142553e
author: minewiskan
ms.author: owend
ms.openlocfilehash: a84cf2ed95ab3660c5a6b3c039dc58351dc43264
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547060"
---
# <a name="define-a-referenced-relationship-and-referenced-relationship-properties"></a>Definir uma relação referenciada e as propriedades da relação referenciada
  Uma relação de dimensão de referência é definida na guia **Uso da Dimensão** do Designer de Cubo. A relação de dimensão de referência é definida especificando-se o seguinte:  
  
-   A dimensão intermediária à qual se unir. Pode ser uma dimensão regular ou outra dimensão de referência.  
  
-   Um atributo da dimensão de referência que define o nível mais baixo para o qual a dimensão está disponível para agregação com relação ao grupo de medida.  
  
-   O atributo (chave estrangeira) da dimensão intermediária que corresponde ao atributo da dimensão de referência.  
  
 Observe que a coluna que vincula a dimensão de referência à tabela de fatos, que geralmente é o atributo principal da dimensão de referência, também deve ser definida como um atributo da dimensão intermediária. Ao criar uma cadeia de dimensões de referência, comece criando a relação regular entre a primeira dimensão da cadeia e o grupo de medidas. Em seguida, crie cada relação de referência adicional na ordem. A relação de referência pode ser criada apenas para uma dimensão que possui uma relação com o grupo de medidas.  
  
 Quando você cria uma relação de dimensão de referência, o vínculo do atributo da dimensão é materializado por padrão. A materialização do atributo da dimensão faz com que o valor do vínculo entre a tabela de fatos e a dimensão de referência de cada linha seja materializado, ou armazenado, na estrutura MOLAP da dimensão durante o processamento. Isso terá um efeito secundário no desempenho do processamento e nos requisitos de armazenamento, mas melhorará o desempenho da consulta.  
  
 Em uma dimensão de referência, a granularidade é especificada pela identificação do atributo que define a relação entre uma dimensão de referência e o grupo de medidas correspondente à tabela principal da dimensão. Quando várias dimensões de referência são encadeadas, as referências definem a relação entre a dimensão externa e o grupo de medidas.  
  
  
