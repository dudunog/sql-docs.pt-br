---
title: srv_pfieldex (API de Procedimento Armazenado Estendido) | Microsoft Docs
description: Saiba como srv_pfieldex na API de procedimento armazenado estendido retorna um ponteiro para os dados que contêm o campo de SRV_PROC solicitado.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_pfieldex
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_pfieldex
ms.assetid: d4e9a34b-b3a3-434f-8556-768bd20d145a
author: rothja
ms.author: jroth
ms.openlocfilehash: ee0bf315964d5710d657abf2288a2b9a79b3c00b
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248281"
---
# <a name="srv_pfieldex-extended-stored-procedure-api"></a>srv_pfieldex (API de procedimento armazenado estendido)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Retorna um ponteiro para dados que contêm o campo SRV_PROC solicitado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
void *srv_pfieldex(SRV_PROC *   
srvproc  
, int   
field  
, int *   
len  
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que atua como identificador de uma conexão de cliente específica. A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
 *campo*  
 Especifica o campo *srvproc* a ser retornado.  
  
|Campo|Descrição|Tipo de retorno|  
|-----------|-----------------|------------------|  
|SRV_MSGLCID|LCID de mensagem da sessão atual.|ULONG *|  
|SRV_INSTANCENAME|Nome de instância (se nomeado); caso contrário, retorna NULL.|WCHAR*|  
  
 *Len*  
 É um ponteiro para uma variável **int** que contém o tamanho do valor de *field* retornado, em bytes. Se *len* for NULL, o tamanho não será retornado. Quando NULL é retornado, **len* é definido como 0.  
  
## <a name="returns"></a>Retornos  
 Um ponteiro para dados cujo tipo depende de *field*. NULL é retornado quando *len* é NULL ou *srvproc* é NULL. Se o *field* for desconhecido, NULL será retornado. Quando NULL é retornado, **len* é definido como 0.  
  
> [!IMPORTANT]  
>  O buffer retornado pelo servidor deve ser somente leitura. Caso contrário, o estado do servidor pode estar corrompido.  
  
## <a name="remarks"></a>Comentários  
 **Observação de segurança** Você deve examinar detalhadamente o código-fonte de procedimentos armazenados estendidos e testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
