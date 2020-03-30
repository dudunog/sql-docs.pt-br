---
title: Opção de configuração de servidor Database Mail XPs | Microsoft Docs
ms.custom: ''
ms.date: 11/27/2018
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Database Mail XPs option
- Database Mail [SQL Server], enabling
ms.assetid: e22c4e63-1792-473b-af11-14a7931ca9ed
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e16286e558d860a346ba8fff366009f064e65f91
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68011964"
---
# <a name="database-mail-xps-server-configuration-option"></a>Opção de configuração de servidor Database Mail XPs

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Use a opção **DatabaseMail XPs** para habilitar o Database Mail neste servidor. Os valores possíveis são:  
  
- `0`: o Database Mail não está disponível (padrão).  
  
- `1`: o Database Mail está disponível.  
  
 A configuração entra em vigor imediatamente, sem que o servidor seja parado e reiniciado.  
  
 Depois de habilitar o Database Mail, você deve configurar um banco de dados de host de Database Mail para usar o Database Mail.  
  
 Configurar o Database Mail por meio do **Assistente para Configuração do Database Mail** faz com que sejam habilitados os procedimentos armazenados estendidos do Database Mail no banco de dados `msdb`. Se usar o **Assistente para Configuração do Database Mail**, você não precisará usar o exemplo de `sp_configure` abaixo.  
  
 Definir a opção **Database Mail XPs** como `0` impede que o Database Mail seja iniciado. Se estiver em execução quando a opção for definida como `0`, ele continuará em execução e enviando emails até estar ocioso pelo tempo configurado na opção `DatabaseMailExeMinimumLifeTime`.  
  
## <a name="examples"></a>Exemplos
 O exemplo a seguir habilita os procedimentos armazenados estendidos do Database Mail.  
  
```  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'Database Mail XPs', 1;  
GO  
RECONFIGURE  
GO  
```  

O exemplo a seguir habilitará os procedimentos armazenados estendidos do Database Mail se ainda não estiverem habilitados.

```sql
IF EXISTS (
    SELECT 1 FROM sys.configurations 
    WHERE NAME = 'Database Mail XPs' AND VALUE = 0)
BEGIN
  PRINT 'Enabling Database Mail XPs'
  EXEC sp_configure 'show advanced options', 1;  
  RECONFIGURE
  EXEC sp_configure 'Database Mail XPs', 1;  
  RECONFIGURE  
END
```

## <a name="see-also"></a>Consulte Também
[Database Mail](../../relational-databases/database-mail/database-mail.md)  
