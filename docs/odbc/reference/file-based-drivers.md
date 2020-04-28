---
title: Drivers baseados em arquivo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based drivers [ODBC]
- ODBC architecture [ODBC], drivers
- drivers [ODBC], file-based drivers
ms.assetid: d92e0c5c-d176-4282-bbe1-d449e2223d50
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 223bd838754f1d656ac71ae37926389097af3ea1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306659"
---
# <a name="file-based-drivers"></a>Drivers baseados em arquivo
Os drivers baseados em arquivo são usados com fontes de dados, como o dBASE, que não fornecem um mecanismo de banco de dados autônomo para o driver usar. Esses drivers acessam os dados físicos diretamente e devem implementar um mecanismo de banco de dados para processar instruções SQL. Como uma prática padrão, os mecanismos de banco de dados em drivers baseados em arquivo implementam o subconjunto de ODBC SQL definido pelo nível de conformidade mínimo do SQL; para obter uma lista das instruções SQL nesse nível de conformidade, consulte o [Apêndice C: gramática SQL](../../odbc/reference/appendixes/appendix-c-sql-grammar.md).  
  
 Ao comparar os drivers baseados em arquivo e DBMS, os drivers baseados em arquivo são mais difíceis de escrever devido ao componente do mecanismo de banco de dados, menos complicados de configurar porque não há partes de rede e menos eficientes porque poucas pessoas têm tempo para escrever mecanismos de banco de dados tão eficientes quanto os produzidos por empresas de banco de dados.  
  
 A ilustração a seguir mostra duas configurações diferentes de drivers baseados em arquivo, uma na qual os dados residem localmente e a outra na qual reside em um servidor de arquivos de rede.  
  
 ![Duas configurações de drivers baseados em&#45;de arquivo](../../odbc/reference/media/pr06.gif "pr06")
