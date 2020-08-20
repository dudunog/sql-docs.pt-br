---
description: Configurar campos de descritor
title: Configurando campos de descritor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], retrieving or setting field values
ms.assetid: d735dc64-370f-48ab-a59f-6cef9bc4e1e8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6625db69709098f3a3db1a1d40f9ab583eee4030
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476428"
---
# <a name="setting-descriptor-fields"></a>Configurar campos de descritor
Para modificar os campos de um descritor, um aplicativo pode chamar **SQLSetDescField**. Alguns campos são somente leitura e não podem ser definidos. (Consulte a descrição da função [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) .)  
  
 Os campos de registro de descritor são definidos com um número de registro (*RecNumber*) de 1 ou superior, enquanto os campos de cabeçalho do descritor são definidos com um número de registro de 0. Um número de registro de 0 também é usado para definir campos de indicador, de acordo com a Convenção em que os indicadores estão contidos na coluna 0. Isso pode deixar a impressão de que os campos de indicador estão contidos no cabeçalho do descritor, mas esse não é o caso. Os campos de indicador são diferentes dos campos de cabeçalho.  
  
 Ao definir os campos individualmente, o aplicativo deve seguir a sequência definida em [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Definir alguns campos faz com que o driver defina outros campos. Isso garante que o descritor esteja sempre pronto para uso quando o aplicativo tiver especificado um tipo de dados. Quando o aplicativo define o campo SQL_DESC_TYPE, o driver verifica se outros campos que especificam o tipo são válidos e consistentes.  
  
 Se uma chamada de função que define um campo de descritor falhar, o conteúdo do campo de descritor será indefinido após a chamada de função com falha.
