---
title: srv_wsendmsg (API de Procedimento Armazenado Estendido) | Microsoft Docs
description: Saiba como srv_wsendmsg na API de procedimento armazenado estendido pode enviar uma mensagem Unicode para o cliente.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_wsendmsg
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_wsendmsg
ms.assetid: f2153076-32c9-4a52-8e1b-fc9618153543
author: rothja
ms.author: jroth
ms.openlocfilehash: 0256a21d4d64df710a4720797297293cbf8a9c0e
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248182"
---
# <a name="srv_wsendmsg-extended-stored-procedure-api"></a>srv_wsendmsg (API do procedimento armazenado estendido)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Envia uma mensagem de Unicode ao cliente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int srv_wsendmsg(SRV_PROC *   
srvproc  
, int   
msgnum  
, int   
severity  
, WCHAR *   
message  
, int   
msglen  
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que atua como identificador de uma conexão de cliente específica. A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
 *Msgnum*  
 É um número de mensagem de 4 bytes.  
  
 *Gravidade*  
 Especifica a gravidade do erro. Uma gravidade menor ou igual a 10 é considerada uma mensagem informativa. Caso contrário, trata-se de um erro.  
  
 *message*  
 É um ponteiro para a cadeia de caracteres de Unicode que será enviada ao cliente.  
  
 *msglen*  
 Especifica o comprimento, em caracteres, de *message*.  
  
## <a name="returns"></a>Retornos  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Comentários  
 Use esta função para enviar mensagens em Unicode. É semelhante a **srv_sendmsg**, mas a mensagem que envia é uma cadeia de caracteres de WCHAR em vez de uma cadeia de caracteres de DBCHAR. Observe que o comprimento da mensagem é informado em caracteres, e não em bytes, e que *msglen* nunca será igual a SRV_NULLTERM.  
  
 A função retorna FAIL quando  
  
-   O *msglen* fornecido não está no intervalo de 0-32242.  
  
-   O *msglen* fornecido é 0, mas o ponteiro de mensagem é o NULL.  
  
-   Ocorre um erro ao enviar a mensagem de erro na rede.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte Também  
 [srv_sendmsg &#40;API de Procedimento Armazenado Estendido&#41;](../../relational-databases/extended-stored-procedures-reference/srv-sendmsg-extended-stored-procedure-api.md)  
  
  
