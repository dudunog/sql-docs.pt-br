---
title: Quando usar SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- SQLNCLI, about SQL Server Native Client
- data access [SQL Server Native Client], about SQL Server Native Client
ms.assetid: 08f18b36-209d-4cf7-9623-ebc61859a91d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7cc9a06601ed0819457b9348bb10cb33b4b92d37
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62637909"
---
# <a name="when-to-use-sql-server-native-client"></a>Quando usar o SQL Server Native Client
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client é uma tecnologia que você pode usar para acessar dados em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  Para obter uma discussão sobre as diferentes tecnologias de acesso a dados, confira [Roteiro das tecnologias de acesso a dados](https://go.microsoft.com/fwlink/?LinkID=179186)  
  
 Ao decidir se deve usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client como a tecnologia de acesso a dados do seu aplicativo, você deve considerar vários fatores.  
  
 No caso de novos aplicativos, se você estiver usando uma linguagem de programação gerenciada, como o Microsoft Visual C# ou o Visual Basic, e precisar acessar os novos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use o provedor de dados .NET Framework para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que faz parte do .NET Framework.  
  
 Caso esteja desenvolvendo um aplicativo baseado no COM e precise acessar os novos recursos incorporados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Caso não precise do acesso aos novos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você poderá continuar a usar o WDAC (Windows Data Access Components).  
  
 Para aplicativos OLE DB e ODBC existentes, o principal problema é se você precisa acessar os novos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Caso tenha um aplicativo consolidado que não precise dos novos recursos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você poderá continuar usando o WDAC. Mas se você precisar acessar esses novos recursos, como o [tipo de dados XML](/sql/t-sql/xml/xml-transact-sql), deverá usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Native Client.  
  
 Tanto o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client quanto o MDAC oferecem suporte ao isolamento de transação de leitura confirmada usando controle de versão de linha, mas apenas o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client oferece suporte ao isolamento da transação de instantâneo. (Em termos de programação, o isolamento de transação de leitura confirmada por meio do controle de versão de linha é igual à transação de leitura confirmada.)  
  
 Para obter informações sobre as diferenças [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entre o Native Client e o MDAC, consulte [atualizando um aplicativo para SQL Server Native Client do MDAC](../../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Programação de SQL Server Native Client](../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [Tópicos de instruções sobre ODBC](../native-client-odbc-how-to/odbc-how-to-topics.md)   
 [Tópicos de instruções sobre OLE DB](../native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
