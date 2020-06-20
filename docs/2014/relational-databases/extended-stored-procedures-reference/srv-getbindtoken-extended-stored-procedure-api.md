---
title: srv_getbindtoken (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_getbindtoken
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_getbindtoken
ms.assetid: c947d011-08ac-4fb8-b925-3da6e0999277
author: rothja
ms.author: jroth
ms.openlocfilehash: d42f95c8a7df87f20ebaa30501b96b5f2a00815a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050729"
---
# <a name="srv_getbindtoken-extended-stored-procedure-api"></a>srv_getbindtoken (API de Procedimento Armazenado Estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Obtém um token de associação da transação na sessão de cliente atual que invoca o procedimento armazenado estendido.  
  
 O procedimento armazenado estendido pode então usar **sp_bindsession** para associar qualquer sessão nova criada por ele no mesmo servidor à transação existente, de modo que a nova sessão possa compartilhar o mesmo espaço para bloqueio de transação com a sessão de cliente que invocou o procedimento armazenado estendido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int srv_getbindtoken (  
SRV_PROC*  
srvproc  
,  
char*  
bindtoken  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que atua como identificador de uma conexão de cliente específica. A estrutura contém todas as informações que a biblioteca de APIs de Procedimento Armazenado Estendido usa para gerenciar as comunicações e os dados entre o aplicativo e o cliente.  
  
 *bindtoken*  
 É um ponteiro para um buffer em que o token de associação será copiado. O token de associação é representado como uma cadeia de caracteres terminada por caractere nulo. O buffer que você especifica deve ter pelo menos 255 bytes.  
  
## <a name="returns"></a>Retornos  
 SUCCEED ou FAIL.  
  
## <a name="remarks"></a>Comentários  
  
### <a name="to-bind-an-extended-stored-procedure-session-to-the-client-session-that-called-it-so-they-share-the-same-transaction-lock-space"></a>Para associar uma sessão de procedimento armazenado estendido à sessão de cliente que a chamou para que compartilhem o mesmo espaço para bloqueio de transação  
  
1.  O procedimento armazenado estendido chama **svr_getbindtoken** para obter o token de associação da transação atual na sessão. O token é retornado no parâmetro *bindtoken* especificado.  
  
2.  O procedimento armazenado estendido abre sessão(ões) nova(s) com relação ao mesmo servidor. Nessa sessão, o procedimento armazenado estendido usa o token de associação com **sp_bindsession** para associar a nova sessão à mesma transação. O procedimento armazenado estendido pode criar várias sessões e associar todas as sessões à mesma transação.  
  
3.  Uma sessão associada é desassociada quando o procedimento armazenado externo é retornado ou quando **sp_bindsession** é chamado com uma cadeia de caracteres vazia.  
  
    > [!NOTE]  
    >  Somente uma sessão associada por vez pode ter acesso a uma conexão compartilhada. Se uma sessão no momento estiver executando uma instrução no servidor ou tiver resultados pendentes no servidor, nenhuma outra sessão que compartilha a mesma conexão associada poderá obter acesso ao servidor enquanto a sessão atual não tiver concluído a execução da instrução atual. Se uma sessão tentar obter acesso à conexão enquanto o servidor está ocupado, será retornado um erro para a sessão conflitante indicando que a conexão está sendo usada e que a sessão deve tentar novamente mais tarde.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Consulte Também  
 [sp_bindsession &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-bindsession-transact-sql)   
 [sp_getbindtoken &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-getbindtoken-transact-sql)  
  
  
