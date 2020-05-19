---
title: Conjunto de linhas LINKEDSERVERS (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- LINKEDSERVERS rowset
- enumerating data sources [OLE DB]
ms.assetid: 2633fd8a-65e7-498d-9aed-8e4b1cca2381
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cba1d6b4c9fb116d90bc68925c8f27d446c73c54
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704225"
---
# <a name="linkedservers-rowset-ole-db"></a>Conjunto de linhas LINKEDSERVERS (OLE DB)
  O conjunto de linhas **LINKEDSERVERS** enumera fontes de dados da organização que podem participar de consultas distribuídas do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 O conjunto de linhas **LINKEDSERVERS** contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Descrição|  
|-----------------|--------------------|-----------------|  
|SVR_NAME|DBTYPE_WSTR|Nome de um servidor vinculado.|  
|SVR_PRODUCT|DBTYPE_WSTR|Fabricante ou outro nome que identifique o tipo de repositório de dados representado pelo nome do servidor vinculado.|  
|SVR_PROVIDERNAME|DBTYPE_WSTR|Nome amigável do provedor OLE DB usado para consumir dados do servidor.|  
|SVR_DATASOURCE|DBTYPE_WSTR|Cadeia de caracteres OLE DB DBPROP_INIT_DATASOURCE usada para adquirir uma fonte de dados do provedor.|  
|SVR_PROVIDERSTRING|DBTYPE_WSTR|Valor DBPROP_INIT_PROVIDERSTRING do OLE DB usado para adquirir uma fonte de dados do provedor.|  
|SVR_LOCATION|DBTYPE_WSTR|Cadeia de caracteres de DBPROP_INIT_LOCATION do OLE DB usada para adquirir uma fonte de dados do provedor.|  
  
 O conjunto de linhas é classificado em SRV_NAME, havendo suporte a uma única restrição em SRV_NAME.  
  
## <a name="see-also"></a>Consulte Também  
 [Suporte ao conjunto de linhas de esquema &#40;OLE DB&#41;](schema-rowset-support-ole-db.md)  
  
  
