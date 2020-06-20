---
title: Enviando conjuntos de resultados para o servidor (API de procedimento armazenado estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], sending result sets
- result sets [SQL Server], extended stored procedures
ms.assetid: 9d54673d-ea9d-4ac6-825a-f216ad8b0e34
author: rothja
ms.author: jroth
ms.openlocfilehash: 82984440f96416189eb18f900764ee7bdaf05a01
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050860"
---
# <a name="sending-result-sets-to-the-server-extended-stored-procedure-api"></a>Enviando conjuntos de resultados ao Servidor (API do procedimento armazenado estendido)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a integração CLR.  
  
 Ao enviar um conjunto de resultados para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o procedimento armazenado estendido deve chamar a API apropriada da seguinte maneira:  
  
-   A função **srv_sendmsg** pode ser chamada em qualquer ordem antes ou depois de todas as linhas (se houver) terem sido enviadas com **srv_sendrow**. Todas as mensagens devem ser enviadas ao cliente antes que o status de conclusão seja enviado com **srv_senddone**.  
  
-   A função **srv_sendrow** é chamada uma vez para cada linha enviada ao cliente. Todas as linhas devem ser enviadas ao cliente antes que quaisquer mensagens, valores de status ou status de conclusão sejam enviados com **srv_sendmsg**, o argumento **srv_status** de **srv_pfield**ou **srv_senddone**.  
  
-   O envio de uma linha que não tinha todas as suas colunas definidas com **srv_describe** faz com que o aplicativo gere uma mensagem de erro informativa e retorne a falha para o cliente. Neste caso, a linha não é enviada.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando procedimentos armazenados estendidos](creating-extended-stored-procedures.md)  
  
  
