---
title: SQLForeignKeys | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLForeignKeys function
ms.assetid: 6c01ce0d-30d7-4c86-8705-3ab254d8a845
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 865bd792c073688491ef53ed6730667c6fcdb472
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706103"
---
# <a name="sqlforeignkeys"></a>SQLForeignKeys
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a atualizações e exclusões em cascata por meio do mecanismo de restrição de chave estrangeira. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará SQL_CASCADE para as colunas UPDATE_RULE e/ou DELETE_RULE se a opção CASCADE estiver especificada na cláusula ON UPDATE e/ou ON DELETE das restrições FOREIGN KEY. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará SQL_NO_ACTION para as colunas UPDATE_RULE e/ou DELETE_RULE se a opção NO ACTION estiver especificada na cláusula ON UPDATE e/ou ON DELETE das restrições FOREIGN KEY.  
  
 Quando valores inválidos estão presentes em qualquer parâmetro **SQLForeignKeys** , **SQLForeignKeys** retorna SQL_SUCCESS na execução. **SQLFetch** retorna SQL_NO_DATA quando são usados valores inválidos nesses parâmetros.  
  
 **SQLForeignKeys** pode ser executado em um cursor de servidor estático. Uma tentativa de executar **SQLForeignKeys** em um cursor atualizável (dinâmico ou de conjunto de chaves) retorna SQL_SUCCESS_WITH_INFO indicando que o tipo de cursor foi alterado.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client dá suporte a informações de relatório para tabelas em servidores vinculados, aceitando um nome de duas partes para os parâmetros *FKCatalogName* e *PKCatalogName* : *linked_server_name. catalog_name*.  
  
## <a name="see-also"></a>Consulte Também  
 [Função SQLForeignKeys](https://go.microsoft.com/fwlink/?LinkId=59344)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
