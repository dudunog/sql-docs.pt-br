---
description: Propriedade SQL
title: Propriedade SQL | Microsoft Docs
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SQL property [RDS]
ms.assetid: e0dabf23-a159-4fe5-a962-3df544a21f5c
author: rothja
ms.author: jroth
ms.openlocfilehash: 325f739e55bcb2b7d3e7440e9906fad341c01078
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724192"
---
# <a name="sql-property"></a>Propriedade SQL
Indica a cadeia de caracteres de consulta usada para recuperar o [conjunto de registros](../ado-api/recordset-object-ado.md).  
  
 Você pode definir a propriedade **SQL** em tempo de design no [RDS. ](./datacontrol-object-rds.md) Marcas de objeto do objeto DataControl ou em tempo de execução no código de script.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](/dotnet/framework/wcf/).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Design time: <PARAM NAME="SQL" VALUE="QueryString">  
Run time: DataControl.SQL = "QueryString"  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *QueryString*  
 Um valor de **cadeia de caracteres** que contém uma solicitação de dados SQL válida.  
  
 *DataControl*  
 Uma variável de objeto que representa um **RDS. Objeto DataControl** .  
  
## <a name="remarks"></a>Comentários  
 Em geral, essa é uma instrução SQL (usando o dialeto do servidor de banco de dados), como `"Select * from NewTitles"` . Para garantir que os registros sejam correspondidos e atualizados com precisão, uma consulta atualizável deve conter um campo diferente de um campo binário longo ou um campo computado.  
  
 A propriedade **SQL** será opcional se um objeto comercial personalizado do lado do servidor recuperar os dados para o cliente.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](./datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo da propriedade SQL (VBScript)](./sql-property-example-vbscript.md)   
 [Propriedade Connect (RDS)](./connect-property-rds.md)   
 [Método de consulta (RDS)](./query-method-rds.md)   
 [Método de atualização (RDS)](./refresh-method-rds.md)   
 [Método SubmitChanges (RDS)](./submitchanges-method-rds.md)