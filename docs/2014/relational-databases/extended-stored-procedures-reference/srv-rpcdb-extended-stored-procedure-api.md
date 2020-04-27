---
title: srv_rpcdb (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
api_name:
- srv_rpcdb
api_location:
- opends60.dll
topic_type:
- apiref
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcdb
ms.assetid: d52bfd22-7a7c-4ab0-af65-df96ff359e6f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7eb462881ab9ae5d6221498a84fc2b79e0524bc9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63046647"
---
# <a name="srv_rpcdb-extended-stored-procedure-api"></a>srv_rpcdb (API do procedimento armazenado estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Retorna o componente de nome de banco de dados para o procedimento armazenado remoto atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DBCHAR * srv_rpcdb (  
SRV_PROC * srvproc,int *len );  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que atua como identificador de uma conexão de cliente específica. A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
 *Len*  
 É um ponteiro para uma variável `int` que recebe o comprimento do nome do banco de dados. Se *len* for NULL, o tamanho do nome do banco de dados não será retornado.  
  
## <a name="returns"></a>Retornos  
 Um ponteiro DBCHAR para a cadeia de caracteres com terminação nula para a parte do nome do banco de dados do procedimento armazenado remoto atual. Se não houver nenhum procedimento armazenado remoto atual, NULL será retornado e o parâmetro *len* será definido como -1.  
  
## <a name="remarks"></a>Comentários  
 Esta função retorna somente o componente de banco de dados do nome de objeto de procedimento armazenado remoto. Isto não inclui os especificadores opcionais para proprietário, nome do procedimento armazenado remoto e número do procedimento armazenado remoto.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
