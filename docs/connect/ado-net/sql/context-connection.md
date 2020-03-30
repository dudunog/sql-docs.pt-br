---
title: A conexão de contexto
description: Descreve a conexão de contexto.
ms.date: 08/15/2019
ms.assetid: e443ca86-9243-4234-a822-ed10a53a9de0
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 6dd4260fa15b737ce6b1411056b82bac93f33fa6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78897007"
---
# <a name="the-context-connection"></a>A conexão de contexto

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

O problema de acesso a dados internos é um cenário bastante comum. Ou seja, você deseja acessar o mesmo servidor no qual sua função ou seu procedimento armazenado CLR (Common Language Runtime) está em execução. Uma opção é criar uma conexão usando <xref:Microsoft.Data.SqlClient.SqlConnection>, especificar uma cadeia de conexão que aponta para o servidor local e abrir a conexão. Isso exige a especificação de credenciais para fazer logon. A conexão está em uma sessão do banco de dados diferente do procedimento armazenado ou da função, pode ter opções `SET` diferentes, está em uma transação separada, não vê suas tabelas temporárias e assim por diante. Se código da função ou do procedimento armazenado gerenciado estiver em execução no processo do SQL Server, isso ocorrerá porque alguém se conectou a esse servidor e executou uma instrução SQL para invocá-lo. Provavelmente, você deseja que o procedimento armazenado ou a função seja executado no contexto dessa conexão, juntamente com sua transação, opções `SET` e assim por diante. Isto é chamado de conexão de contexto.  
  
A conexão de contexto permite executar instruções Transact-SQL no mesmo contexto em que seu código foi invocado pela primeira vez. Para obter informações mais detalhadas, confira [A conexão de contexto](https://go.microsoft.com/fwlink/?LinkId=115395) dos Manuais Online do SQL Server.
