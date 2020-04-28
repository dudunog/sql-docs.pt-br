---
title: ExecuteOptionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ExecuteOptionEnum
helpviewer_keywords:
- ExecuteOptionEnum enumeration [ADO]
ms.assetid: 68bfa83a-5df4-4bef-8736-0f88ae8c29ea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bef70bd72425e749865e31ecf162e719737dd272
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67932842"
---
# <a name="executeoptionenum"></a>ExecuteOptionEnum
Especifica como um provedor deve executar um comando.  
  
|Constante|Valor|Descrição|  
|--------------|-----------|-----------------|  
|**adAsyncExecute**|0x10|Indica que o comando deve ser executado de forma assíncrona.<br /><br /> Esse valor não pode ser combinado com o valor de [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) **adCmdTableDirect**.|  
|**adAsyncFetch**|0x20|Indica que as linhas restantes após a quantidade inicial especificada na propriedade [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) devem ser recuperadas de forma assíncrona.|  
|**adAsyncFetchNonBlocking**|0x40|Indica que o thread principal nunca é bloqueado durante a recuperação. Se a linha solicitada não tiver sido recuperada, a linha atual será automaticamente movida para o final do arquivo.<br /><br /> Se você abrir um [conjunto de registros](../../../ado/reference/ado-api/recordset-object-ado.md) de um [fluxo](../../../ado/reference/ado-api/stream-object-ado.md) que contém um **conjunto de registros**armazenado persistentemente, o **adAsyncFetchNonBlocking** não terá efeito; a operação será síncrona e bloqueada.<br /><br /> **adAsynchFetchNonBlocking** não tem efeito quando a opção [adCmdTableDirect](../../../ado/reference/ado-api/commandtypeenum.md) é usada para abrir o **conjunto de registros**.|  
|**adExecuteNoRecords**|0x80|Indica que o texto do comando é um comando ou procedimento armazenado que não retorna linhas (por exemplo, um comando que só insere dados). Se qualquer linha for recuperada, elas serão descartadas e não retornadas.<br /><br /> **adExecuteNoRecords** só pode ser passado como um parâmetro opcional para o método de **execução** de **comando** ou conexão.|  
|**adExecuteStream**|0x400|Indica que os resultados de uma execução de comando devem ser retornados como um fluxo.<br /><br /> **adExecuteStream** só pode ser passado como um parâmetro opcional para o método **Execute Command** .|  
|**adExecuteRecord**||Indica que **CommandText** é um comando ou procedimento armazenado que retorna uma única linha que deve ser retornada como um objeto de **registro** .|  
|**adOptionUnspecified**|-1|Indica que o comando não está especificado.|  
  
## <a name="adowfc-equivalent"></a>Equivalente do ADO/WFC  
 Pacote: **com. ms. wfc. Data**  
  
|Constante|  
|--------------|  
|AdoEnums.ExecuteOption.ASYNCEXECUTE|  
|AdoEnums.ExecuteOption.ASYNCFETCH|  
|AdoEnums.ExecuteOption.ASYNCFETCHNONBLOCKING|  
|AdoEnums. ExecuteOption. nograves|  
|AdoEnums. ExecuteOption. não especificado|  
  
## <a name="applies-to"></a>Aplica-se A  
  
|||  
|-|-|  
|[Método Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)|[Método Execute (conexão ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|  
|[Método Open (Conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[Método Requery](../../../ado/reference/ado-api/requery-method.md)|
