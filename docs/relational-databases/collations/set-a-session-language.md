---
title: Definir um idioma da sessão | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [SQL Server], international considerations
- globalization [SQL Server], sessions
- time [SQL Server]
- sessions [SQL Server], languages
- international considerations [SQL Server], sessions
- dates [SQL Server], session languages
- global considerations [SQL Server], sessions
- client-side session language
- time [SQL Server], session languages
- messages [SQL Server], international considerations
- server-side session language
ms.assetid: de7f2c90-8f4f-4cfc-94cc-4933a7fd2bde
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 201dbacf7ce2dde7cb3da387bbfd79070e1790ed
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68140865"
---
# <a name="set-a-session-language"></a>Definir um idioma de sessão
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  O idioma da sessão pode ser usado para definir como os seguintes elementos são exibidos no servidor com base na preferência cultural e de idioma:  
  
-   O idioma que será usado para erros e outras mensagens do sistema. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a várias cópias de todas as cadeias de caracteres de erros e de mensagens do sistema em todos os idiomas nos quais o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está disponível. Essas mensagens podem ser exibidas na exibição de catálogo [sys.messages](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md) . Quando uma versão localizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]é instalada, essas mensagens do sistema são traduzidas para a versão do idioma instalado. Por padrão, você também obtém o conjunto dessas mensagens em inglês (EUA). Além disso, é possível adicionar mensagens definidas pelo usuário em um idioma específico usando [sp_addmessage](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md).  
  
-   O formato de dados de data e hora.  
  
-   Os nomes de dias e meses, inclusive abreviações.  
  
-   O primeiro dia da semana.  
  
-   Dados de moeda.  
  
 Há 33 idiomas disponíveis para uso como configurações de sessão. Para obter uma lista de idiomas, consulte [sys.syslanguages](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md).  
  
## <a name="setting-the-session-language-from-the-server"></a>Definindo o idioma da sessão no servidor  
 Para definir o idioma da sessão do lado de servidor, use [SET LANGUAGE](../../t-sql/statements/set-language-transact-sql.md).  
  
## <a name="setting-the-session-language-from-the-client"></a>Definindo o idioma da sessão no cliente  
 O idioma da sessão pode ser definido no lado do cliente usando o OLE DB, ODBC ou ADO.NET. Para OLE DB, use a propriedade SSPROP_INIT_CURRENTLANGUAGE. Para obter mais informações, consulte [Propriedades de inicialização e autorização](../../relational-databases/native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
 Para ODBC, use a palavra-chave Idioma. Para obter mais informações, consulte [SQLConfigDataSource](../../relational-databases/native-client-odbc-api/sqlconfigdatasource.md).  
  
 Para ADO.NET, use o parâmetro **Idioma Atual** do objeto **ConnectionString** . Para obter mais informações, consulte a documentação do SDK do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Data Access Components (MDAC).  
  
  
