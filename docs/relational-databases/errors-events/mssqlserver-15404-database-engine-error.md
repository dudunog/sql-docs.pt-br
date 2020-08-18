---
description: MSSQLSERVER_15404
title: MSSQLSERVER_15404 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 15404 (Database Engine error)
ms.assetid: 69677f02-bc81-4e4a-99b8-5c1bd1de36df
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a9a05c8e47e97357b562a3429b98fe856e60d75f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88333852"
---
# <a name="mssqlserver_15404"></a>MSSQLSERVER_15404
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|15404|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|SEC_NTGRP_ERROR|  
|Texto da mensagem|Não foi possível obter informações sobre o grupo/usuário '*user*' do Windows NT, código de erro *code*.|  
  
## <a name="explanation"></a>Explicação  
15404 é usado na autenticação quando uma entidade de segurança inválida é especificada. A representação de uma conta do Windows falha porque não há uma relação de confiança total entre a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o domínio da conta do Windows.  
  
## <a name="user-action"></a>Ação do usuário  
Verifique se a entidade de segurança do Windows existe e não está digitada de forma incorreta.  
  
Se esse erro for resultante da falta de uma relação de confiança total entre a conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o domínio da conta do Windows, uma destas ações poderá corrigir o erro:  
  
-   Use uma conta do mesmo domínio que o usuário do Windows para o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Se o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estiver usando uma conta de computador como Serviço de Rede ou Sistema Local, o computador deverá ser confiável no domínio que contém o usuário do Windows.  
  
-   Usar uma conta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
