---
title: Migrar bancos de dados MySQL para SQL Server-BD SQL do Azure | Microsoft Docs
description: Use esse processo recomendado para migrar bancos de dados MySQL para o SQL Server ou o Azure SQL Database usando o Assistente de Migração do SQL Server (SSMA).
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 8006f9a0-394d-4238-8dc5-44255134628b
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 0daee899775b5a8bb3a0e4b6ee0eef4a93eca00b
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293585"
---
# <a name="migrating-mysql-databases-to-sql-server---azure-sql-db-mysqltosql"></a>Migrando bancos de dados MySQL para SQL Server-BD SQL do Azure (MySQLToSql)
O Assistente de Migração do SQL Server (SSMA) para MySQL é um ambiente abrangente que ajuda você a migrar rapidamente bancos de dados MySQL para SQL Server ou SQL Azure. Usando o SSMA para MySQL, você pode examinar os objetos e os dados do banco de dados, avaliar os bancos de dado para migração, migrar objetos de banco para SQL Server ou SQL Azure e, em seguida, migrar dados para SQL Server ou SQL Azure.  
  
## <a name="recommended-migration-process"></a>Processo de migração recomendado  
Para migrar com êxito os objetos e os dados de bancos de dados MySQL para SQL Server ou SQL Azure, use o seguinte processo:  
  
1.  [Trabalhando com projetos do SSMA &#40;MySQLToSQL&#41;](../../ssma/mysql/working-with-ssma-projects-mysqltosql.md).  
  
    Depois de criar o projeto, você pode definir opções de conversão de projeto, migração e mapeamento de tipo. Para obter mais informações sobre configurações de projeto, consulte [definindo opções de projeto &#40;MySQLToSQL&#41;](../../ssma/mysql/setting-project-options-mysqltosql.md). Para obter informações sobre como personalizar mapeamentos de tipo de dados, consulte [mappinging MySQL and SQL Server Data Types &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-and-sql-server-data-types-mysqltosql.md)  
  
2.  [Conectando-se ao MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
3.  [Conectando-se ao SQL Server &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
4.  [Mapeando bancos de dados MySQL para SQL Server esquemas &#40;MySQLToSQL&#41;](../../ssma/mysql/mapping-mysql-databases-to-sql-server-schemas-mysqltosql.md)  
  
5.  [Conectando-se ao BD SQL do Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)  
  
6.  Opcionalmente, a [avaliação de bancos de dados MySQL para conversão &#40;MySQLToSQL&#41;](../../ssma/mysql/assessing-mysql-databases-for-conversion-mysqltosql.md) para avaliar os objetos de banco para conversão e estimar o tempo de conversão.  
  
7.  [Convertendo bancos de dados MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
8.  [Sincronização](loading-converted-database-objects-into-sql-server-mysqltosql.md)  
  
9. Você pode fazer isso de uma das seguintes maneiras:  
  
    -   Salve um script e execute-o em SQL Server ou SQL Azure.  
  
    -   Sincronize os objetos de banco de dados.  
  
10. [Migrando dados do MySQL para o SQL Server-BD SQL do Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
11. Se necessário, atualize os aplicativos de banco de dados.  
  
> [!NOTE]  
> Não é possível migrar os esquemas Information_schema e MySQL.  
  
## <a name="see-also"></a>Consulte Também  
[Instalando o SSMA para MySQL &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
[Introdução com o SSMA para MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/getting-started-with-ssma-for-mysql-mysqltosql.md)  
  
