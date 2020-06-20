---
title: Configurar operações de índice paralelo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index parallel operations [SQL Server]
- processors [SQL Server], parallel index operations
- max degree of parallelism option
- MAXDOP index option, parallel index operations
- parallel index operations [SQL Server]
ms.assetid: 8ec8c71e-5fc1-443a-92da-136ee3fc7f88
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8831aadae15af03a05f4ab03cfe514e54566df1f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050015"
---
# <a name="configure-parallel-index-operations"></a>Configurar operações de índice paralelo
  Este tópico define o grau máximo de paralelismo e explica como modificar essa configuração no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Em computadores multiprocessadores em execução no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise ou superior, as instruções de índice podem usar vários processadores para executar operações de verificação, classificação e índice associadas à instrução de índice da mesma forma que outras consultas. O número de processadores usados para executar uma única instrução de índice é determinado pela opção de configuração [Grau Máximo de Paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) , pela carga de trabalho atual e pelas estatísticas de índice. A opção grau máximo de paralelismo determina o número máximo de processadores a serem usados na execução no plano paralelo. Se o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] detectar que o sistema está ocupado, o grau de paralelismo da operação de índice será automaticamente reduzido antes do início da execução da instrução. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] também poderá diminuir o grau de paralelismo se a coluna de chave à esquerda de um índice não particionado tiver um número limitado de valores distintos ou a frequência de cada valor distinto variar de forma significativa.  
  
> [!NOTE]  
>  As operações de índice paralelas não estão disponíveis em todas as edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [recursos com suporte nas edições do SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para definir a opção max degree of paralelismo, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   O número de processadores usados pelo otimizador de consulta normalmente fornece melhor desempenho. Porém, operações como criar, recriar ou cancelar índices muito grandes são recursos intensivos e podem causar recursos insuficientes em outros aplicativos e operações de banco de dados durante a operação de índice. Quando ocorrer esse problema, você poderá configurar manualmente o número máximo de processadores usados para executar a instrução de índice, limitando o número de processadores para a operação de índice.  
  
-   A opção de índice MAXDOP substitui a opção de configuração max degree of parallelism apenas para consultas que especificam essa opção. A tabela a seguir lista os valores inteiros válidos que podem ser especificados com a opção de configuração grau máximo de paralelismo e a opção de índice MAXDOP.  
  
    |Valor|Descrição|  
    |-----------|-----------------|  
    |0|Especifica que o servidor determina o número de CPUs que são usadas, dependendo da carga de trabalho do sistema atual. Esse é o valor padrão e a configuração recomendada.|  
    |1|Suprime a geração de plano paralelo. A operação será executada em série.|  
    |2-64|Limita o número de processadores ao valor especificado. Menos processadores podem ser usados dependendo da carga de trabalho atual. Se um valor maior que o número de CPUs disponíveis for especificado, o número atual de CPUs disponíveis será usado.|  
  
-   Execução de índice paralelo e a opção de índice MAXDOP se aplicam às seguintes instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] :  
  
    -   CREATE INDEX  
  
    -   ALTER INDEX REBUILD  
  
    -   DROP INDEX (Isso só se aplica aos índices cluster.)  
  
    -   ALTER TABLE ADD (índice) CONSTRAINT  
  
    -   ALTER TABLE DROP (índice cluster) CONSTRAINT  
  
-   A opção de índice MAXDOP não pode ser especificada na instrução ALTER INDEX REORGANIZE.  
  
-   Requisitos de memória para operações de índice de partição que necessitam de classificação poderão ser maiores se o otimizador de consulta aplicar graus de paralelismo à operação de criação. Quanto maior os graus de paralelismo, o maior será o requisito de memória. Para saber mais, confira [Partitioned Tables and Indexes](../partitions/partitioned-tables-and-indexes.md).  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER na tabela ou exibição.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-set-max-degree-of-parallelism-on-an-index"></a>Para definir o grau máximo de paralelismo de um índice  
  
1.  No Pesquisador de Objetos, clique no sinal de mais para expandir o banco de dados que contém a tabela na qual você deseja definir o grau máximo de paralelismo de um índice.  
  
2.  Expanda a pasta **Tabelas** .  
  
3.  Clique no sinal de mais para expandir a tabela na qual você deseja definir o grau máximo de paralelismo de um índice.  
  
4.  Expanda a pasta **Índices** .  
  
5.  Clique com o botão direito do mouse no índice do qual você deseja definir o grau máximo de paralelismo e selecione **Propriedades**.  
  
6.  Em **Selecione uma página**, selecione **Opções**.  
  
7.  Selecione **Grau máximo de paralelismo**e insira um valor entre 1 e 64.  
  
8.  Clique em **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-set-max-degree-of-parallelism-on-an-existing-index"></a>Para definir o grau máximo de paralelismo de um índice existente  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    /*Alters the IX_ProductVendor_VendorID index on the Purchasing.ProductVendor table so that, if the server has eight or more processors, the Database Engine will limit the execution of the index operation to eight or fewer processors.  
    */  
    ALTER INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor  
    REBUILD WITH (MAXDOP=8);   
    GO  
    ```  
  
 Para obter mais informações, consulte [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql).  
  
#### <a name="set-max-degree-of-parallelism-on-a-new-index"></a>Defina o grau máximo de paralelismo de um novo índice  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    CREATE INDEX IX_ProductVendor_NewVendorID   
    ON Purchasing.ProductVendor (BusinessEntityID)  
    WITH (MAXDOP=8);  
    GO  
    ```  
  
 Para obter mais informações, consulte [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql).  
  
  
