---
title: Migrar bancos de dados do Sybase ASE para SQL Server-BD SQL do Azure | Microsoft Docs
ms.custom: ''
ms.date: 11/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: ed7952d4-8331-44d7-bccf-3440e17238b2
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c3735e03e3196f899ab33ca152364244e3331ac5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68028855"
---
# <a name="migrating-sap-ase-databases-to-sql-server---azure-sql-database-sybasetosql"></a>Migrando bancos de dados do SAP ASE para o SQL Server-SybaseToSQL (Azure SQL Database)
O Assistente de Migração do SQL Server (SSMA) para SAP Adaptive Server Enterprise (ASE) é um ambiente abrangente que ajuda você a migrar rapidamente bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SAP ase para o ou para o Azure SQL Database. Usando o SSMA para SAP ASE, você pode examinar os objetos e os dados do banco de dados, avaliar os bancos de dado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] migração, migrar objetos de banco de dados para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o ou o Azure SQL Database e, em seguida, migrar dados para o ou para o Azure.  
  
## <a name="recommended-migration-process"></a>Processo de migração recomendado  
Para migrar com êxito objetos e dados de bancos de dado SAP ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o ou para o banco de dados SQL do Azure, use o seguinte processo:  
  
1.  [Crie um novo projeto do SSMA](working-with-ssma-projects-sybasetosql.md).  
  
    Depois de criar o projeto, você pode definir opções de conversão de projeto, migração e mapeamento de tipo. Para obter informações sobre configurações de projeto, consulte [definindo opções de projeto &#40;SybaseToSQL&#41;](../../ssma/sybase/setting-project-options-sybasetosql.md). Para obter informações sobre como personalizar mapeamentos de tipo de dados, consulte [mapeando Sybase ase e SQL Server tipos de dados &#40;&#41;SybaseToSQL ](../../ssma/sybase/mapping-sybase-ase-and-sql-server-data-types-sybasetosql.md).  
  
2.  [Conecte-se ao servidor de banco de dados SAP ase](connecting-to-sybase-ase-sybasetosql.md).  
  
3.  [Conecte-se a uma instância do SQL Server](connecting-to-sql-server-sybasetosql.md) ou [Conecte-se a uma instância do banco de dados SQL do Azure](connecting-to-azure-sql-db-sybasetosql.md).  
  
4.  [Mapeie esquemas de banco de dados SAP ase para SQL Server/esquemas de banco de dados do banco de dados SQL do Azure](https://msdn.microsoft.com/2c927003-c49d-4fe1-8e3e-5b2899166268).  
  
5.  Opcionalmente, [Crie relatórios de avaliação](assessing-sybase-ase-database-objects-for-conversion-sybasetosql.md) para avaliar objetos de banco de dados para conversão e estimar o tempo de conversão.  
  
6.  [Converta esquemas de banco de dados do SAP ASE em esquemas de banco de dados SQL do SQL Server/Azure](https://msdn.microsoft.com/509cb65d-2f54-427a-83d7-37919cc4e3e3).  
  
7.  [Carregue os objetos de banco de dados convertidos em SQL Server/banco de dados SQL do Azure](https://msdn.microsoft.com/4c59256f-99a8-4351-9559-a455813dbd06).  
  
    Salve um script e execute-o no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou no banco de dados SQL do Azure ou sincronize os objetos de banco de dados.  
  
8.  [Migre dados para o SQL Server/banco de dado SQL do Azure](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811).  
  
9. Se necessário, atualize seus aplicativos de banco de dados.  
  
## <a name="see-also"></a>Confira também  
[Instalando o SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md)  
[Introdução com o SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/getting-started-with-ssma-for-sybase-sybasetosql.md)  
  
