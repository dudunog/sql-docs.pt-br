---
title: srv_rpcoptions (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_rpcoptions
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcoptions
ms.assetid: dbcce5d1-d5a1-4379-9597-04e43af5923d
author: rothja
ms.author: jroth
ms.openlocfilehash: 861c27e94d3717a4dbeba1fe5f2633c2604ee7c4
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050613"
---
# <a name="srv_rpcoptions-extended-stored-procedure-api"></a>srv_rpcoptions (API de procedimento armazenado estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Retorna opções de tempo de execução para o procedimento armazenado remoto atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DBUSMALLINT srv_rpcoptions ( SRV_PROC *  
srvproc   
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que é o identificador de uma conexão de cliente específica (neste caso, o identificador que recebeu o procedimento armazenado remoto). A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
## <a name="returns"></a>Retornos  
 Um bitmap que contém os sinalizadores de tempo de execução unidos em um OU lógico para o procedimento armazenado remoto atual. Se não houver um procedimento armazenado remoto atual, será retornado 0 e uma mensagem é gerada.  
  
## <a name="remarks"></a>Comentários  
 A seguinte tabela descreve cada sinalizador de tempo de execução.  
  
|Sinalizador de tempo de execução|Descrição|  
|--------------------|-----------------|  
|SRV_NOMETADATA|O cliente solicitou resultados sem informações de metadados. Esse sinalizador só é usado quando o cliente está se comunicando com uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Um aplicativo de API de procedimento armazenado estendido não pode omitir informações de metadados.|  
|SRV_RECOMPILE|O cliente solicitou a recompilação do procedimento armazenado remoto antes de executá-lo. Este sinalizador pode não se aplicar a um aplicativo de API de procedimento armazenado estendido.|  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
