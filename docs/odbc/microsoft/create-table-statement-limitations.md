---
title: CRIAR LIMITAÇÕES DE DECLARAÇÃO DE TABELA | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE TABLE statement limitations [ODBC]
- ODBC SQL grammar, CREATE TABLE statement limitations
ms.assetid: c5067855-20c9-456f-8d63-f375b4297f2e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a83acb061cf8192dff1c6adede349f49a0b0bbdb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280867"
---
# <a name="create-table-statement-limitations"></a>Limitações da instrução CREATE TABLE
Quando o Microsoft Access, Microsoft Excel ou Paradoxdriver for usado e o comprimento de um texto ou coluna binária não for especificado (ou especificado como 0), o comprimento da coluna será definido como 255.  
  
 Quando o driver dBASE é usado e o comprimento de um texto ou coluna binária não é especificado (ou é especificado como 0), o comprimento da coluna será definido como 254.  
  
 Um máximo de 255 colunas é suportado.  
  
 Quando o driver do Microsoft Excel é usado em uma fonte de dados microsoftexcel 5.0, 7.0 ou 97, uma planilha não pode ser criada com o mesmo nome de uma planilha que foi descartada anteriormente. Quando o driver do Microsoft Excel é usado para acessar uma planilha da versão 5.0, 7.0 ou 97, uma declaração DROP TABLE limpa a planilha, mas não exclui o nome da planilha.  
  
 Quando o driver Paradoxé é usado, as colunas não podem ser adicionadas uma vez que um índice tenha sido definido em uma tabela. Se a primeira coluna da lista de argumentos de uma declaração CREATE TABLE criar um índice, uma segunda coluna não poderá ser incluída na lista de argumentos.
