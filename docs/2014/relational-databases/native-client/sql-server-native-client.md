---
title: O que&#39;s New no SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: e4d4fe39-0090-42a7-8405-6378370d11cb
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 003abb67cd66d02294210ddb3f55061abcc804f4
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704141"
---
# <a name="what39s-new-in-sql-server-native-client"></a>O que&#39;s New no SQL Server Native Client
  O [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] instala o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client. Não há nenhum [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Native Client.  
  
 Não haverá mais atualizações para o driver ODBC no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. O sucessor do driver ODBC no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, denominado [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC Driver 11 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Windows, é instalado com o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. Para obter mais informações sobre o [!INCLUDE[msCoName](../../includes/msconame-md.md)] ODBC Driver 11 para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Windows, consulte [Microsoft ODBC Driver 11 para SQL Server - Windows](https://www.microsoft.com/download/details.aspx?id=36434).  
  
 O provedor OLE DB no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client foi atualizado por último no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client. Os desenvolvedores que quiserem usar o Provedor OLE DB para se conectar à versão mais recente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devem usar o provedor OLE DB fornecido com o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Native Client.  
  
 Os tópicos a seguir descrevem os novos recursos significativos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
-   [Suporte do SQL Server Native Client para LocalDB](features/sql-server-native-client-support-for-localdb.md)  
  
-   [Descoberta de metadados](features/metadata-discovery.md)  
  
-   [Suporte a UTF-16 no SQL Server Native Client 11.0](features/utf-16-support-in-sql-server-native-client-11-0.md)  
  
-   [Suporte do SQL Server Native Client à alta disponibilidade e recuperação de desastre](features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [Acessando informações de diagnóstico no log de eventos estendidos](features/accessing-diagnostic-information-in-the-extended-events-log.md)  
  
 Além disso, o ODBC no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client agora oferece suporte a três recursos que foram adicionados ao ODBC padrão no SDK do Windows 7:  
  
-   Execução assíncrona em operações relacionadas à conexão. Para obter mais informações, consulte [Execução assíncrona](https://go.microsoft.com/fwlink/?LinkID=191493).  
  
-   Extensibilidade do tipo de dados C. Para obter mais informações, consulte [Tipos de dados C em ODBC](https://go.microsoft.com/fwlink/?LinkID=191495).  
  
     Para dar suporte a esse recurso no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client, SQLGetDescField pode retornar `SQL_C_SS_TIME2` (para `time` tipos) ou `SQL_C_SS_TIMESTAMPOFFSET` (for `datetimeoffset` ) em vez de `SQL_C_BINARY` , se seu aplicativo usar o ODBC 3,8. Para obter mais informações, consulte [suporte de tipo de dados para aprimoramentos de data e hora ODBC](features/date-and-time-improvements.md).  
  
-   Chamando `SQLGetData` várias vezes com um buffer pequeno para recuperar um valor de parâmetro grande. Para obter mais informações, consulte [Recuperando parâmetros de saída usando SQLGetData](https://go.microsoft.com/fwlink/?LinkID=191494).  
  
 Os tópicos a seguir descrevem as alterações de comportamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
-   Ao chamar `ICommandWithParameters::SetParameterInfo` , o valor passado para o parâmetro *pwszName* deve ser um identificador válido. Para obter mais informações, consulte [ICommandWithParameters](../native-client-ole-db-interfaces/icommandwithparameters.md).  
  
-   `SQLDescribeParam` agora irá retornar de maneira consistente um valor que esteja de acordo com a especificação de ODBC. Para obter mais informações, consulte [SQLDescribeParam](../native-client-odbc-api/sqldescribeparam.md).  
  
-   [Alteração de comportamento do driver ODBC ao lidar com conversões de caracteres](features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Recursos do SQL Server Native Client](features/sql-server-native-client-features.md)  
  
  
