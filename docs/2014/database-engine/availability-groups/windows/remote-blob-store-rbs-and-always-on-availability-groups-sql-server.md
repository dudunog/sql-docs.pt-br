---
title: RBS (Remote BLOB Store) e Grupos de Disponibilidade AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 01a70258-d4fd-40bc-bc44-c490b5d6c420
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: bcc51e3fc8269ef0035e52b040ca38eef0f23e84
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936607"
---
# <a name="remote-blob-store-rbs-and-alwayson-availability-groups-sql-server"></a>RBS (Remote Blob Store) e grupos de disponibilidade AlwaysOn (SQL Server)
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]o pode fornecer uma solução de alta disponibilidade e recuperação de desastre para objetos de blob do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [RBS (Remote BLOB Store)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md) . [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] protege quaisquer esquemas e metadados RBS armazenados em um banco de dados de disponibilidade replicando-os para as réplicas secundárias. Esse é o banco de dados de conteúdo do SharePoint. Em linhas gerais, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] armazena esses metadados RBS independentemente do blob.  
  
 A proteção para dados BLOB RBD depende do local do repositório de BLOB:  
  
|Local do repositório de BLOB|Os grupos de disponibilidade podem proteger esses dados BLOB?|  
|-------------------------|-----------------------------------------------------|  
|O mesmo banco de dados que contém os metadados RBS (armazenados por meio de um provedor remoto FILESTREAM RBS)|Sim|  
|Outro banco de dados na mesma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (armazenado por meio de um provedor remoto FILESTREAM RBS)|Sim<br /><br /> Recomendamos que você coloque esse banco de dados no mesmo grupo de disponibilidade que o banco de dados que contém os metadados RBS.|  
|Outro banco de dados em uma instância diferente do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (armazenado por meio de um provedor remoto FILESTREAM RBS)|Sim<br /><br /> Esse banco de dados deve estar em um grupo de disponibilidade separado.|  
|Um repositório de BLOB de terceiros|Não<br /><br /> Para proteger esses dados BLOB, use os mecanismos de alta disponibilidade do provedor de repositório de BLOB.|  
  
##  <a name="limitations"></a><a name="Limitations"></a> Limitações  
  
-   Os mantenedores do RBS precisam ser direcionados para a réplica primária.  
  
##  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Use um ouvinte de grupo de disponibilidade. Para obter mais informações, consulte [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md).  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
  
-   [Maintaining Remote BLOB Store](https://msdn.microsoft.com/library/gg316773\(SQL.105\).aspx) (Mantendo o Remote BLOB Store) (nos Manuais Online do [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] )  
  
-   [Running RBS Maintainer](https://blogs.msdn.com/b/sqlrbs/archive/2010/03/19/running-rbs-maintainer.aspx) (Executando o Mantenedor do RBS) (blog)  
  
-   [Configure Remote BLOB Storage (RBS) with the FILESTREAM provider (SharePoint 2010)](https://blogs.msdn.com/b/mvpawardprogram/archive/2012/04/02/configure-remote-blob-storage-rbs-with-the-filestream-provider-sharepoint-2010.aspx) (Configurar o RBS (Remote BLOB Storage) com o provedor FILESTREAM (SharePoint 2010)) (blog)  
  
## <a name="see-also"></a>Consulte Também  
 [Conectividade de cliente AlwaysOn &#40;SQL Server&#41;](always-on-client-connectivity-sql-server.md)   
 [Remote Blob Store &#40;RBS&#41; &#40;SQL Server&#41;](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
  
