---
description: Microsoft ODBC Driver for SQL Server no Windows
title: Microsoft ODBC Driver for SQL Server no Windows | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b10cfc22-6a2c-4707-a456-0dcec317982b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b52e3df054a0c13846741237000855c079c842b
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005900"
---
# <a name="microsoft-odbc-driver-for-sql-server-on-windows"></a>Microsoft ODBC Driver for SQL Server no Windows
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Os Microsoft ODBC Drivers para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] são drivers ODBC independentes que fornecem uma API (interface de programação de aplicativo) implementando as interfaces ODBC padrão para a Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].

O Microsoft ODBC Driver for SQL Server pode ser usado para criar novos aplicativos. Você também pode atualizar seus aplicativos mais antigos que usam um driver ODBC mais antigo no momento. O ODBC Driver for SQL Server dá suporte a conexões com o Banco de Dados SQL do Azure, o Azure Synapse Analytics e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  

## <a name="summary"></a>Resumo

| Versão       | Recursos com suporte      |
| ------------- |---------------| 
| Microsoft ODBC Driver 17 for SQL Server | <ul><li>Suporte a Always Encrypted para a API BCP</li><li>O novo atributo de cadeia de conexão UseFMTONLY faz com que o driver use metadados herdados em casos especiais que exigem tabelas temporárias</li>
| Microsoft ODBC Driver 13.1 for SQL Server     | <ul><li>Always Encrypted</li><li>Autenticação do Azure AD</li><li>AG (Grupos de Disponibilidade) AlwaysOn</li></ul>   | 
| Microsoft ODBC Driver 13 for SQL Server      | <ul><li>Nome de domínio internacionalizado (IDN)</li></ul> |
| Microsoft ODBC Driver 11 para SQL Server | <ul><li>Pool de conexões com reconhecimento de driver</li><li>Resiliência da conexão</li><li>Execução assíncrona (Método de Sondagem)</li></ul> |    

## <a name="documentation"></a>Documentação  
Esta documentação para o Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] inclui:  
  
-   [Notas sobre a Versão para ODBC para SQL Server no Windows](../../../connect/odbc/windows/release-notes-odbc-sql-server-windows.md)  
-   [Recursos do Microsoft ODBC Driver for SQL Server no Windows](../../../connect/odbc/windows/features-of-the-microsoft-odbc-driver-for-sql-server-on-windows.md)  
-   [Requisitos do sistema, instalação e arquivos de driver](../../../connect/odbc/windows/system-requirements-installation-and-driver-files.md)  
-   [Pooling de conexão com reconhecimento de driver no driver ODBC para SQL Server](../../../connect/odbc/windows/driver-aware-connection-pooling-in-the-odbc-driver-for-sql-server.md)  
-   [Exemplo de execução assíncrona &#40;método de notificação&#41](../../../connect/odbc/windows/asynchronous-execution-notification-method-sample.md)  
-   [Resiliência de conexão no driver ODBC do Windows](../../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md)  
-   [Uso do Always Encrypted com o Driver ODBC](../../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)
-   [Usando o Azure Active Directory com o Driver ODBC](../../../connect/odbc/using-azure-active-directory.md) 
-   [Como usar a resolução IP de rede transparente](../../../connect/odbc/using-transparent-network-ip-resolution.md)   

## <a name="community"></a>Comunidade  
- [Blog dos Drivers do SQL Server](https://techcommunity.microsoft.com/t5/sql-server/bg-p/SQLServer/label-name/SQLServerDrivers)  
- [SQL Server Data Access Forum](https://social.technet.microsoft.com/Forums/en/sqldataaccess/threads)  
  
## <a name="see-also"></a>Consulte Também  
- [Criando aplicativos com o SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)   
- [Perguntas frequentes do SQL Server Native Client](/previous-versions/aa937707(v=msdn.10))   
- [Referência do programador ODBC](../../../odbc/reference/odbc-programmer-s-reference.md)   
- [SQL Server Native Client (ODBC)](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)