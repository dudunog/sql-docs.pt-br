---
title: O grupo de arquivos com otimização de memória | Microsoft Docs
description: Saiba como criar um grupo de arquivo com otimização de memória, que tem contêineres para arquivos de dados e arquivos delta, antes de criar tabelas com otimização de memória no SQL Server.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 14106cc9-816b-493a-bcb9-fe66a1cd4630
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 636bc0ebcfbd85f9da38ecff6cd1ff4a966164c8
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85715350"
---
# <a name="the-memory-optimized-filegroup"></a>O grupo de arquivos com otimização de memória
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Para criar tabelas com otimização de memória, você deve primeiro criar um grupo de arquivos com otimização de memória. O grupo de arquivos com otimização de memória retém um ou mais contêineres. Cada contêiner contém arquivos de dados ou arquivos delta, ou então ambos.  
  
 Embora as linhas de dados das tabelas `SCHEMA_ONLY` não persistam e os metadados para tabelas otimizadas para memória e procedimentos armazenados compilados nativamente estejam armazenados nos catálogos tradicionais, o mecanismo [!INCLUDE[hek_2](../../includes/hek-2-md.md)] ainda requer um grupo de arquivos com otimização de memória para tabelas otimizadas para memória `SCHEMA_ONLY` para fornecer uma experiência uniforme para bancos de dados com tabelas otimizadas para memória.  
  
 O grupo de arquivos com otimização de memória baseia-se no grupo de arquivos do fluxo de arquivos, com as seguintes diferenças:  
  
-   Só é possível criar um grupo de arquivos com otimização de memória por banco de dados. É necessário marcar explicitamente o grupo de arquivos como contendo o memory_optimized_data. Você pode criar o grupo de arquivos ao criar o banco de dados ou poderá adicioná-lo posteriormente:  
  
    ```sql  
    ALTER DATABASE imoltp ADD FILEGROUP imoltp_mod CONTAINS MEMORY_OPTIMIZED_DATA  
    ```  
  
-   É necessário adicionar um ou mais contêineres ao grupo de arquivos `MEMORY_OPTIMIZED_DATA`. Por exemplo:  
  
    ```sql  
    ALTER DATABASE imoltp ADD FILE (name='imoltp_mod1', filename='c:\data\imoltp_mod1') TO FILEGROUP imoltp_mod  
    ```  
  
-   Não é necessário habilitar o fluxo de arquivos ([Habilitar e configurar FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)) para criar um grupo de arquivos com otimização de memória. O mapeamento do fluxo de arquivos é realizado pelo mecanismo [!INCLUDE[hek_2](../../includes/hek-2-md.md)] .  
  
-   Você pode adicionar novos contêineres a um grupo de arquivos com otimização de memória. Você pode precisar de um novo contêiner para expandir o armazenamento necessário para a tabela otimizada para memória e também para distribuir ES entre vários contêineres.  
  
-   O movimento dos dados com um grupo de arquivos com otimização de memória é otimizado em uma configuração do Grupo de Disponibilidade AlwaysOn. Diferente dos arquivos do fluxo de arquivos enviados para as réplicas secundárias, os arquivos de ponto de verificação (tanto de dados quanto de delta) no grupo de arquivos com otimização de memória não são enviados para as réplicas secundárias. Os arquivos de dados e delta são criados usando o log de transação na réplica secundária.  
  
As limitações a seguir aplicam-se a um grupo de arquivos com otimização de memória:  
  
-   Depois de usar um grupo de arquivos com otimização de memória, você somente poderá removê-lo ao descartar o banco de dados. Em um ambiente de produção, é muito improvável que você precise remover o grupo de arquivos com otimização de memória.  
  
-   Não é possível descartar um contêiner não vazio ou mover os pares de dados e arquivo delta para outro contêiner no grupo de arquivos com otimização de memória.    
  
## <a name="configuring-a-memory-optimized-filegroup"></a>Configurando um grupo de arquivos com otimização de memória  
Considere criar múltiplos contêineres em um grupo de arquivos com otimização de memória e distribui-los em diferentes unidades para obter mais largura de banda para transferir os dados para a memória. 
 
Em um contêiner múltiplo, cenário com várias unidades, os arquivos de dados e delta são alocados em rodízio nos contêineres. O primeiro arquivo de dados é alocado no primeiro contêiner e o arquivo delta é alocado no próximo contêiner, repetindo o padrão de alocação. Este esquema de alocação distribui os dados e os arquivos delta uniformemente entre os contêineres se você possui um arquivo ímpar de unidades, cada um mapeado para um contêiner. Contudo, se você possuir um número par de unidades, cada um mapeado para um contêiner, isso poderá resultar no armazenamento desequilibrado dos dados para unidades ímpares e arquivos deltas mapeados para unidades pares. Para obter um fluxo equilibrado de E/S na recuperação, considere a colocação de pares de arquivos de dados e delta nos mesmos eixos/armazenamentos.
  
Ao configurar o armazenamento, é necessário fornecer espaço livre em disco de quatro vezes o tamanho das tabelas com otimização de memória. Também é necessário garantir que o subsistema de E/S seja compatível com a IOPS necessária para a carga de trabalho. Se os pares de dados e arquivo delta forem preenchidos em um IOPS específico, será necessário três vezes o tamanho do IOPS para abranger as operações de armazenamento e mesclagem. Você pode adicionar capacidade de armazenamento e IOPS adicionando um ou mais contêineres ao grupo de arquivos com otimização de memória.  
 
> [!CAUTION]
> Se um `MAXSIZE` valor está definido para o grupo de arquivos com otimização de memória e arquivos de ponto de verificação excedem o tamanho máximo do contêiner, o banco de dados se torna suspeito.   
> Nesse caso, não tente definir o banco de dados como OFFLINE e ONLINE, fazendo o banco de dados permanecer no estado RECOVERY_PENDING.
  
## <a name="see-also"></a>Consulte Também  
[Criando e gerenciando armazenamento para objetos com otimização de memória](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
[Database Files and Filegroups](../../relational-databases/databases/database-files-and-filegroups.md)    
[Opções de arquivo e grupos de arquivos ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-file-and-filegroup-options.md) 

