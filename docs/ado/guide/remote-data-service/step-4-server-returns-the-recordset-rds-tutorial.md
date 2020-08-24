---
description: 'Etapa 4: O servidor retorna um conjunto de registros (Tutorial RDS)'
title: 'Etapa 4: o servidor retorna o conjunto de registros (tutorial RDS) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], server returns Recordset
ms.assetid: 3d1855c4-419c-4810-b5ea-6c874b5e2905
author: rothja
ms.author: jroth
ms.openlocfilehash: 3805ac88556b6d00aaf43bf5e1d28ece71c1c591
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759106"
---
# <a name="step-4-server-returns-the-recordset-rds-tutorial"></a>Etapa 4: O servidor retorna um conjunto de registros (Tutorial RDS)
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 O RDS converte o objeto **Recordset** recuperado em um formulário que pode ser enviado de volta ao cliente (ou seja, ele *realiza marshaling* do **conjunto de registros**). A forma exata da conversão e como ela é enviada depende de se o servidor está na Internet ou em uma intranet, em uma rede local ou se é uma biblioteca de vínculo dinâmico. No entanto, esse detalhe não é crítico; Tudo o que importa é que o RDS envie o **conjunto de registros** de volta ao cliente.  
  
 No lado do cliente, um objeto **Recordset** é retornado e atribuído a uma variável local.  
  
```vb
Sub RDSTutorial4()  
   Dim DS as New RDS.DataSpace  
   Dim RS as ADODB.Recordset  
   Dim DF as Object  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Etapa 5: o DataControl é tornado utilizável (tutorial do RDS)](./step-5-datacontrol-is-made-usable-rds-tutorial.md)   
 [Tutorial RDS (VBScript)](./rds-tutorial-vbscript.md)