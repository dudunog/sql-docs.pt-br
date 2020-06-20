---
title: srv_rpcparams (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_rpcparams
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcparams
ms.assetid: 96a5e6f6-d320-4623-b96e-0a856e3abebb
author: rothja
ms.author: jroth
ms.openlocfilehash: 2303ad02f6b50ecf1e3b0b43c91aab7dc4bd2b22
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050566"
---
# <a name="srv_rpcparams-extended-stored-procedure-api"></a>srv_rpcparams (API de procedimento armazenado estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Retorna o número de parâmetros para o procedimento armazenado remoto atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int srv_rpcparams ( SRV_PROC *  
srvproc   
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que é o identificador de uma conexão de cliente específica (neste caso, o identificador que recebeu o procedimento armazenado remoto). A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
## <a name="returns"></a>Retornos  
 O número de parâmetros no procedimento armazenado remoto. Se não houver nenhum parâmetro no procedimento armazenado remoto ou se não houver nenhum procedimento armazenado remoto atual, -1 será retornado e ocorrerá um erro de informação.  
  
## <a name="remarks"></a>Comentários  
 Esta função retorna o número de parâmetros no procedimento armazenado remoto atual. Normalmente é chamado do procedimento armazenado remoto.  
  
 Quando uma chamada de procedimento armazenado remoto é feita com parâmetros, os parâmetros podem ser passados pelo nome ou pela posição (sem-nome). Se a chamada de procedimento armazenado remoto tiver sido feita com alguns parâmetros passados pelo nome e outros pela posição, ocorrerá um erro. Quando esse erro ocorrer, o manipulador de procedimento armazenado remoto será chamado, mas não receberá os parâmetros e **srv_rpcparams** retornará 0.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
