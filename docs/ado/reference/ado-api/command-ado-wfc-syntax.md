---
title: Comando (ADO – sintaxe WFC) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Command collection [ADO], ADO/WFC syntax
ms.assetid: 39d0aa06-03ac-4c9a-8400-83947756ef99
author: rothja
ms.author: jroth
ms.openlocfilehash: 61b5a54778bb680b68e923d198831d770973d1a7
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760439"
---
# <a name="command-ado---wfc-syntax"></a>Comando (ADO – Sintaxe WFC)
## <a name="package-commswfcdata"></a>pacote com. ms. wfc. Data  
  
### <a name="constructor"></a>Construtor  
  
```  
public Command()  
public Command(String commandtext)  
```  
  
### <a name="methods"></a>Métodos  
  
```  
public void cancel()  
public com.ms.wfc.data.Parameter createParameter(String  
    Name, int Type, int Direction, int Size, Object Value)  
public Recordset execute()  
public Recordset execute(Object[] parameters)  
public Recordset execute(Object[] parameters, int options)  
public int executeUpdate(Object[] parameters)  
public int executeUpdate(Object[] parameters, int options)  
public int executeUpdate()  
```  
  
 O método **ExecuteUpdate** é um método de caso especial que chama o método de **execução** ADO subjacente com determinados parâmetros. O método **ExecuteUpdate** não dá suporte ao retorno de um objeto **Recordset** , portanto, o parâmetro *Options* do método **Execute** é modificado com **AdoEnums. executeoptions. nograves**. Depois que o método **Execute** é concluído, seu parâmetro *RecordsAffected* atualizado é passado de volta para o método **ExecuteUpdate** , que finalmente é retornado como um **int**.  
  
### <a name="properties"></a>Propriedades  
  
```  
public com.ms.wfc.data.Connection getActiveConnection()  
public void setActiveConnection(com.ms.wfc.data.Connection con)  
public void setActiveConnection(String conString)  
public String getCommandText()  
public void setCommandText(String command)  
public int getCommandTimeout()  
public void setCommandTimeout(int timeout)  
public int getCommandType()  
public void setCommandType(int type)  
public String getName()  
public void setName(String name)  
public boolean getPrepared()  
public void setPrepared(boolean prepared)  
public int getState()  
public com.ms.wfc.data.Parameter getParameter(int n)  
public com.ms.wfc.data.Parameter getParameter(String n)  
public com.ms.wfc.data.Parameters getParameters()  
public AdoProperties getProperties()  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)
