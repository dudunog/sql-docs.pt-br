---
title: SQLPrimaryKeys | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bf00ecd74b64b3910ba19365920baf914f86939c
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705894"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
  Uma tabela pode ter uma coluna ou colunas que podem servir como identificadores de linha exclusivos, e tabelas criadas sem uma restrição de chave primária retornam um conjunto de resultados vazio para SQLPrimaryKeys. A função ODBC [SQLSpecialColumns](sqlspecialcolumns.md) relata candidatos de identificador de linha para tabelas sem chaves primárias.  
  
 SQLPrimaryKeys retorna SQL_SUCCESS se os valores existem ou não para os parâmetros *CatalogName*, *schemas*ou *TableName* . SQLFetch retorna SQL_NO_DATA quando são usados valores inválidos nesses parâmetros.  
  
 SQLPrimaryKeys pode ser executado em um cursor de servidor estático. Uma tentativa de executar SQLPrimaryKeys em um cursor atualizável (dinâmico ou de conjunto de chaves) retornará SQL_SUCCESS_WITH_INFO indicando que o tipo de cursor foi alterado.  
  
 O driver ODBC do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client dá suporte ao relatório de informações de tabelas em servidores vinculados, aceitando um nome de duas partes para o parâmetro *CatalogName* : *Linked_Server_Name.Catalog_Name*.  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys e parâmetros com valor de tabela  
 Se o atributo de instrução SQL_SOPT_SS_NAME_SCOPE tiver o valor SQL_SS_NAME_SCOPE_TABLE_TYPE, em vez de seu valor padrão de SQL_SS_NAME_SCOPE_TABLE, SQLPrimaryKeys retornará informações sobre as colunas de chave primária dos tipos de tabela. Para obter mais informações sobre SQL_SOPT_SS_NAME_SCOPE, consulte [SQLSetStmtAttr](sqlsetstmtattr.md).  
  
 Para obter mais informações sobre parâmetros com valor de tabela, consulte [parâmetros com valor de tabela &#40;&#41;ODBC ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLPrimaryKeys](https://go.microsoft.com/fwlink/?LinkId=59361)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
