---
title: srv_senddone (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_senddone
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_senddone
ms.assetid: 1fc4f1d5-56d4-43f6-b5e4-0c0cc295cba3
author: rothja
ms.author: jroth
ms.openlocfilehash: aa71ebe23557ab470748b3108fc1263469a193cf
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050559"
---
# <a name="srv_senddone-extended-stored-procedure-api"></a>srv_senddone (API de procedimento armazenado estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Envia uma mensagem de conclusão de resultado para o cliente.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
int srv_senddone (  
SRV_PROC *  
srvproc  
,  
DBUSMALLINT   
status  
,  
DBUSMALLINT  
info  
,  
DBINT  
count   
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que é o identificador de uma conexão de cliente específica (neste caso, o identificador que recebeu a solicitação de linguagem). A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
 *status*  
 É um campo de 2 bytes para vários sinalizadores *status* . Vários sinalizadores podem ser definidos usando os operadores lógicos AND e OR com valores de sinalizador *status* . A seguinte tabela lista os possíveis sinalizadores *status* .  
  
|Sinalizador de status|Descrição|  
|-----------------|-----------------|  
|SRV_DONE_COUNT|O parâmetro *count* contém uma contagem válida.|  
|SRV_DONE_ERROR|O comando do cliente atual recebeu um erro.|  
  
 *detalhes*  
 É um campo reservado de 2 bytes. Defina o valor como 0.  
  
 *contagem*  
 É um campo de 4 bytes usado para indicar uma contagem do conjunto de resultados atual. Se o sinalizador SRV_DONE_COUNT for definido no campo *status* , *count* manterá uma contagem válida.  
  
## <a name="returns"></a>Retornos  
 SUCCEED ou FAIL  
  
## <a name="remarks"></a>Comentários  
 Uma solicitação do cliente pode fazer com que o servidor execute vários comandos e retorne vários conjuntos de resultados. Para cada conjunto de resultados, **srv_senddone** deve retornar uma mensagem de conclusão de resultado para o cliente.  
  
 O campo *count* indica o número de linhas afetadas por um comando. Se o campo *count* contiver uma contagem, o sinalizador SRV_DONE_COUNT deverá ser definido no campo *status* . Essa configuração permite ao cliente distinguir entre um valor *count* igual a 0 e um campo não usado *count* .  
  
 Não chame **srv_senddone** no manipulador SRV_CONNECT.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
