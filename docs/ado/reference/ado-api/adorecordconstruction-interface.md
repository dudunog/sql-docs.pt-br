---
description: Interface ADORecordConstruction
title: Interface ADORecordConstruction | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ADORecordConstruction
helpviewer_keywords:
- ADORecordConstruction interface [ADO]
ms.assetid: 52a5429e-5829-455e-be3b-31f05cbecf2d
author: rothja
ms.author: jroth
ms.openlocfilehash: 4e56c1ed6339c7b0baf50abfc6308a2dc2be741a
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88976227"
---
# <a name="adorecordconstruction-interface"></a>Interface ADORecordConstruction
A interface **ADORecordConstruction**é usada para construir um objeto de **registro** ado de um objeto de **linha** OLE DB em um aplicativo C/C++.  
  
 Esta interface dá suporte às seguintes propriedades:  
  
## <a name="properties"></a>Propriedades  
  
|Propriedade|Descrição|  
|-|-|  
|[ParentRow](./parentrow-property-ado.md)|Somente gravação.<br />Define o contêiner de um objeto de **linha** de OLE DB neste objeto de **registro** ADO.|  
|[Fila](./row-property-ado.md)|Leitura/gravação.<br />Obtém/define um objeto de **linha** de OLE DB de/neste objeto de **registro** ADO.|  
  
## <a name="methods"></a>Métodos  
 Nenhum.  
  
## <a name="events"></a>Eventos  
 Nenhum.  
  
## <a name="remarks"></a>Comentários  
 Considerando um objeto de **linha** de OLE DB ( `pRow` ), a construção de um objeto de **registro** ADO ( `adoR` ), valores para as três operações básicas a seguir:  
  
1.  Criar um objeto de **registro** ADO:  
  
    ```  
    _RecordPtr adoR;  
    adoRs.CreateInstance(__uuidof(_Record));  
    ```  
  
2.  Consulte a interface **IADORecordConstruction** no objeto **Record** :  
  
    ```  
    adoRecordConstructionPtr adoRConstruct=NULL;  
    adoR->QueryInterface(__uuidof(ADORecordConstruction),  
                        (void**)&adoRConstruct);  
    ```  
  
3.  Chame o método de propriedade **IADORecordConstruction::p ut_Row** para definir o objeto de **linha** de OLE DB no objeto de **registro** ADO:  
  
    ```  
    IUnknown *pUnk=NULL;  
    pRow->QueryInterface(IID_IUnknown, (void**)&pUnk);  
    adoRConstruct->put_Row(pUnk);  
    ```  
  
 O objeto **adoR** resultante agora representa o objeto de **registro** ADO construído a partir do OLE DB objeto de **linha** .  
  
 Um objeto de **registro** ADO também pode ser construído a partir do contêiner de um objeto de **linha** de OLE DB.  
  
## <a name="requirements"></a>Requisitos  
 **Versão:** ADO 2,0 e posterior  
  
 **Biblioteca:** msado15.dll  
  
 **UUID:** 00000567-0000-0010-8000-00AA006D2EA4