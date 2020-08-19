---
description: DLL de instalação do driver
title: DLL de instalação de driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- installing ODBC components [ODBC], driver setup DLL
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: 49bab021-81fa-402e-b7a4-a5214f1fadc4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 79fff6ce68e7860b444ebefa736cb959cd54576b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476202"
---
# <a name="driver-setup-dll"></a>DLL de instalação do driver
> [!NOTE]  
>  A partir do Windows XP e do Windows Server 2003, o ODBC está incluído no sistema operacional Windows. Você só deve instalar explicitamente o ODBC em versões anteriores do Windows.  
  
 A DLL de instalação do driver contém as funções **ConfigDriver** e **ConfigDSN** . O **ConfigDriver** executa tarefas de instalação específicas do driver, como inserir informações específicas do driver no registro. O **ConfigDSN** mantém informações específicas do driver sobre fontes de dados no registro. Para obter uma descrição completa dessas funções, consulte [Setup DLL API Reference](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 **ConfigDSN** chama as seguintes funções na DLL do instalador para manter as informações da fonte de dados no registro:  
  
-   **SQLWriteDSNToIni**. Adicione uma fonte de dados.  
  
-   **SQLRemoveDSNFromIni**. Excluir uma fonte de dados.  
  
-   **SQLWritePrivateProfileString**. Escreva um valor específico de driver em uma subchave de especificação de fonte de dados.  
  
-   **SQLGetPrivateProfileString**. Ler um valor específico de driver de uma subchave de especificação de fonte de dados.  
  
-   **SQLGetTranslator**. Solicita ao usuário um nome de tradutor e uma opção. Essa função chama **ConfigTranslator** na DLL de instalação do tradutor.  
  
 A DLL de instalação do driver é escrita pelo desenvolvedor do driver. Ele pode fazer parte da DLL do driver ou de uma DLL separada.
