---
description: 'Alternativas: usar instruções SQL'
title: 'Alternativas: usando instruções SQL | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ADO]
- editing data [ADO], sql statements
- ADO, SQL statements
ms.assetid: 8b528b23-063d-45ea-8dea-6a90d4060b20
author: rothja
ms.author: jroth
ms.openlocfilehash: 423a0afa6bba082cbebc28bee07c5be3ba90c6f1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88991617"
---
# <a name="alternatives-using-sql-statements"></a>Alternativas: usar instruções SQL
O ADO também permite o uso de comandos como alternativas para suas propriedades e métodos internos para a edição de dados. Dependendo do seu provedor, todas as operações mencionadas nesta seção também podem ser realizadas passando comandos para sua fonte de dados. Por exemplo, instruções SQL UPDATE podem ser usadas para modificar dados sem usar a propriedade **Value** de um **campo**. As instruções SQL INSERT podem ser usadas para adicionar novos registros a uma fonte de dados, em vez do método ADO **AddNew**. Para obter mais informações sobre o SQL ou a linguagem de manipulação de dados do seu provedor, consulte a documentação da fonte de dados.  
  
 Por exemplo, você pode passar uma cadeia de caracteres SQL contendo uma instrução DELETE para um banco de dados, conforme mostrado no código a seguir:  
  
```  
'BeginSQLDelete  
strSQL = "DELETE FROM Shippers WHERE ShipperID = " & intId  
objConn1.Execute strSQL, , adCmdText + adExecuteNoRecords  
'EndSQLDelete  
```
