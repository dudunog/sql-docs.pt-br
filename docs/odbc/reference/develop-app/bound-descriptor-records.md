---
description: Registros de descritor associados
title: Registros do descritor associado | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- bound descriptor records [ODBC]
- descriptors [ODBC], bound descriptor records
ms.assetid: 55d09344-6682-40f6-b634-036b134ff650
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fcf88374967b5a9d8426d16c9e92c06e4eef32cb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476798"
---
# <a name="bound-descriptor-records"></a>Registros de descritor associados
Quando o aplicativo define o SQL_DESC_DATA_PTR campo de um registro de descritor para que ele não contenha mais um valor nulo, o registro é considerado *associado*.  
  
 Se o descritor for um APD, cada registro vinculado constituirá um parâmetro associado. Para parâmetros de entrada, o aplicativo deve associar um parâmetro para cada marcador de parâmetro dinâmico na instrução SQL antes de executar a instrução. Para parâmetros de saída, o aplicativo não precisa associar o parâmetro.  
  
 Se o descritor for um ARD, que descreve uma linha de dados do banco de dado, cada registro associado constituirá uma coluna associada.
