---
title: Criando um aplicativo de provedor de OLE DB de SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, application creation
- applications [SQL Server Native Client]
- OLE DB, creating applications
ms.assetid: f3ae6815-f32d-4913-a1a2-2ba2f20cfd88
author: rothja
ms.author: jroth
ms.openlocfilehash: dd8ef192fb17a5b2719481fa43fd06b370868c62
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85056035"
---
# <a name="creating-a-sql-server-native-client-ole-db-provider-application"></a>Criando um aplicativo provedor OLE DB do SQL Server Native Client
  A criação de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplicativo de provedor de OLE DB de cliente nativo envolve estas etapas:  
  
1.  Estabelecimento de uma conexão a uma fonte de dados.  
  
2.  Execução de um comando.  
  
3.  Processamento dos resultados.  
  
> [!NOTE]  
>  Quando possível, use a Autenticação do Windows. Se a Autenticação do Windows não estiver disponível, solicite aos usuários que digitem suas credenciais em tempo de execução. Evite armazenar as credenciais em um arquivo. Se for necessário persistir as credenciais, criptografe-as com a [Win32 cryptoAPI](https://go.microsoft.com/fwlink/?LinkId=9504).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Estabelecendo uma conexão com uma fonte de dados](establishing-a-connection-to-a-data-source.md)  
  
-   [Executando um comando](executing-a-command.md)  
  
-   [Processando resultados](processing-results.md)  
  
-   [Sobre propriedades OLE DB](about-ole-db-properties.md)  
  
-   [Usando a cláusula OUTPUT com OLE DB no SQL Server Native Client](using-the-output-clause-with-ole-db-in-sql-server-native-client.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;OLE DB&#41;](../native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
