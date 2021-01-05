---
title: Espelhamento de banco de dados e catálogos de texto completo
description: Saiba como configurar um espelho de banco de dados em um banco de dados que tem um catálogo de texto completo e saiba mais sobre índices antes e depois do failover.
ms.custom: seo-lt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: database-mirroring
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- full-text catalogs [SQL Server], database mirroring
- catalogs [SQL Server], database mirroring
ms.assetid: e34072ae-fe8a-462d-bb03-02fa0987f793
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4ff2e2c4c79889c6ce9d20abc226e5b2450c552b
ms.sourcegitcommit: 370cab80fba17c15fb0bceed9f80cb099017e000
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97639974"
---
# <a name="database-mirroring-and-full-text-catalogs-sql-server"></a>Espelhamento de banco de dados e catálogos de texto completo (SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Para espelhar um banco de dados que possui um catálogo de texto completo, use o backup como sempre para criar um backup de banco de dados completo do banco de dados principal e então restaure o backup para copiar o banco de dados no servidor espelho. Para obter mais informações, veja [Preparar um banco de dados espelho para espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md).  
  
## <a name="full-text-catalog-and-indexes-before-failover"></a>Catálogo de texto completo e índices antes do failover  
 Em um banco de dados espelho criado recentemente, o catálogo de texto completo é o mesmo de quando foi feito o backup do banco de dados. Depois do início do espelhamento de banco de dados, qualquer alteração no nível de catálogo feira por instruções DDL (CREATE FULLTEXT CATALOG, ALTER FULLTEXT CATALOG, DROP FULLTEXT CATALOG) é registrada e enviada ao servidor espelho para ser reproduzida no banco de dados espelho. Porém, não são reproduzidas as alterações no nível de índice no banco de dados espelho, pois ele não está registrado no servidor principal. Portanto, à medida que o conteúdo do catálogo de texto completo muda no banco de dados principal, o conteúdo do catálogo de texto completo no banco de dados espelho não é sincronizado.  
  
## <a name="full-text-indexes-after-failover"></a>Índices de texto completo após o failover  
 Após um failover, o rastreamento completo de um índice de texto completo no novo servidor principal pode ser necessário ou útil nas situações seguintes:  
  
-   Se o rastreamento de alterações estiver OFF em um índice de texto completo, você deve iniciar um rastreamento completo nesse índice usando a seguinte instrução:  
  
     ALTER FULLTEXT INDEX ON *table_name* START FULL POPULATION  
  
-   Se estiver configurado para rastreamento de alterações automático, o índice de texto completo será sincronizado automaticamente. Porém, a sincronização reduz um pouco o desempenho do texto completo. Se o desempenho estiver muito lento, você poderá fazer com que um rastreamento completo seja executado definindo o rastreamento de alterações como desligado e redefinindo-o como automático:  
  
    -   Para definir o rastreamento de alterações como desligado:  
  
         ALTER FULLTEXT INDEX ON *table_name* SET CHANGE_TRACKING OFF  
  
    -   Para definir o rastreamento de alterações automático como automático:  
  
         ALTER FULLTEXT INDEX ON *table_name* SET CHANGE_TRACKING AUTO  
  
    > [!NOTE]  
    >  Para verificar se o controle de alterações automático está ativado, você pode usar a função [OBJECTPROPERTYEX](../../t-sql/functions/objectpropertyex-transact-sql.md) para consultar a propriedade **TableFullTextBackgroundUpdateIndexOn** da tabela.  
  
 Para obter mais informações, consulte [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md).  
  
> [!NOTE]  
>  Iniciar um rastreamento após um failover funciona da mesma maneira que iniciar um rastreamento após uma restauração.  
  
## <a name="after-forcing-service"></a>Depois de forçar serviço  
 Depois que o serviço é forçado para o servidor espelho (com possível perda de dados), inicie um rastreamento completo. O método a ser usado para iniciar um rastreamento completo depende se as alterações no índice de texto completo são rastreadas. Para obter mais informações, consulte "Índices de texto completo após o failover", anteriormente neste tópico.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)   
 [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)   
 [Espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)   
 [Fazer backup e restaurar índices e catálogos de texto completo](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
  
