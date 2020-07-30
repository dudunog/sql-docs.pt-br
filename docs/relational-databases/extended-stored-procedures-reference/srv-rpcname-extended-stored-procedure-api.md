---
title: srv_rpcname (API de Procedimento Armazenado Estendido) | Microsoft Docs
description: Saiba como srv_rpcname na API de procedimento armazenado estendido retorna o componente de nome do procedimento para o procedimento armazenado remoto atual.
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_rpcname
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_rpcname
ms.assetid: 0a1424e4-3319-4836-b8d8-5e0344cc683f
author: rothja
ms.author: jroth
ms.openlocfilehash: 99e901a9ae1a14644d522b23747f1d242f8c95d3
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87248275"
---
# <a name="srv_rpcname-extended-stored-procedure-api"></a>srv_rpcname (API de procedimento armazenado estendido)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Retorna o componente de nome de procedimento para o procedimento armazenado remoto atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
DBCHAR * srv_rpcname (  
SRV_PROC *  
srvproc  
,  
int *  
len   
);  
```  
  
## <a name="arguments"></a>Argumentos  
 *srvproc*  
 É um ponteiro para a estrutura SRV_PROC que é o identificador de uma conexão de cliente específica (neste caso, o identificador que recebeu o procedimento armazenado remoto). A estrutura contém informações que a biblioteca de APIs de procedimento armazenado estendido usa para gerenciar a comunicação e os dados entre o aplicativo e o cliente.  
  
 *Len*  
 É um ponteiro para uma variável inteira que recebe o comprimento do nome do banco de dados. Se *len* for NULL, o comprimento do nome do procedimento armazenado remoto não será retornado.  
  
## <a name="returns"></a>Retornos  
 Um ponteiro DBCHAR para a cadeia de caracteres com terminação nula do componente de nome de procedimento armazenado remoto do procedimento armazenado remoto atual. Se não houver um procedimento armazenado remoto atual, NULL será retornado e *len* será definido como -1.  
  
## <a name="remarks"></a>Comentários  
 Essa função retorna apenas o nome do procedimento armazenado remoto. Ela não inclui os especificadores opcionais para proprietário, nome do banco de dados e número do procedimento armazenado remoto.  
  
 Como é válido chamar **srv_rpcname** quando não existe um procedimento armazenado remoto (nenhum erro informativo ocorre), essa função fornece um método para determinar se um procedimento armazenado remoto existe.  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
