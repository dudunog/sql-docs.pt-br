---
title: srv_alloc (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_alloc
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_alloc
ms.assetid: 91505c59-a273-452f-b71d-5e8205c21863
author: rothja
ms.author: jroth
ms.openlocfilehash: 729675f7df3a4e394bb28f4074644289489ef248
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050802"
---
# <a name="srv_alloc-extended-stored-procedure-api"></a>srv_alloc (API do procedimento armazenado estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Aloca memória dinamicamente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
void * srv_alloc ( DBINT  
size  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *size*  
 Especifica o número de bytes para alocar.  
  
## <a name="returns"></a>Retornos  
 Um ponteiro para o espaço recentemente alocado. Se *size* bytes não puderem ser alocados, um ponteiro nulo será retornado.  
  
## <a name="remarks"></a>Comentários  
 A função **srv_alloc** é equivalente à função **GlobalAlloc** da API do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Funções normais de gerenciamento de memória em tempo de execução da API C do Windows podem ser usadas em um aplicativo de API de procedimento armazenado estendido.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
