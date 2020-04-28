---
title: Propriedade executeoptions (RDS) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- ExecuteOptions property [ADO], VBScript example
ms.assetid: 62a4fd88-afc3-4f1f-b978-40710a30c4e9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2ae55ec1fccbd491854fb8bff2daa215d38b20ee
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67964182"
---
# <a name="executeoptions-property-rds"></a>Propriedade ExecuteOptions (RDS)
Indica se a execução assíncrona está habilitada.  
  
> [!IMPORTANT]
>  A partir do Windows 8 e do Windows Server 2012, os componentes do servidor RDS não são mais incluídos no sistema operacional Windows (consulte Windows 8 e [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) para obter mais detalhes). Os componentes do cliente RDS serão removidos em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Os aplicativos que usam o RDS devem migrar para o [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="settings-and-return-values"></a>Configurações e valores de retorno  
 Define ou retorna um dos valores a seguir.  
  
|Constante|Descrição|  
|--------------|-----------------|  
|**adcExecSync**|Executa a próxima atualização do conjunto de [registros](../../../ado/reference/ado-api/recordset-object-ado.md) de forma síncrona.|  
|**adcExecAsync**|Padrão. Executa a próxima atualização do conjunto de **registros** de forma assíncrona.|  
  
> [!NOTE]
>  Cada arquivo executável que usa essas constantes deve fornecer declarações para eles. Você pode recortar e colar as declarações de constante desejadas do arquivo Adcvbs. Inc, localizadas na pasta de instalação padrão da biblioteca do RDS.  
  
## <a name="remarks"></a>Comentários  
 Se **executeoptions** for definido como **adcExecAsync**, isso executará de forma assíncrona a próxima chamada de **atualização** no [RDS. ](../../../ado/reference/rds-api/datacontrol-object-rds.md) **Conjunto de registros**do objeto DataControl.  
  
 Se você tentar chamar [redefine](../../../ado/reference/rds-api/reset-method-rds.md), [Refresh](../../../ado/reference/rds-api/refresh-method-rds.md), [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md), [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)ou [Recordset](../../../ado/reference/rds-api/recordset-sourcerecordset-properties-rds.md) enquanto outra operação assíncrona pode alterar o [RDS. ](../../../ado/reference/rds-api/datacontrol-object-rds.md)O **conjunto de registros** do objeto DataControl está em execução, ocorre um erro.  
  
 Se ocorrer um erro durante uma operação assíncrona, o **RDS. **O valor [ReadyState](../../../ado/reference/rds-api/readystate-property-rds.md) do objeto DataControl é alterado de **adcReadyStateLoaded** para **adcReadyStateComplete**, e o valor da propriedade **Recordset** permanece como *Nothing*.  
  
## <a name="applies-to"></a>Aplica-se A  
 [Objeto DataControl (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo das propriedades executeoptions e FetchOptions (VBScript)](../../../ado/reference/rds-api/executeoptions-and-fetchoptions-properties-example-vbscript.md)   
 [Método Cancel (RDS)](../../../ado/reference/rds-api/cancel-method-rds.md)


