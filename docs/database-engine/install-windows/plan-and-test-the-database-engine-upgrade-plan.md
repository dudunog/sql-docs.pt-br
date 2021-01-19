---
title: Planejar e testar o plano de upgrade do mecanismo de banco de dados | Microsoft Docs
description: Este artigo descreve o planejamento que ocorre antes de você começar a sua atualização de SQL Server, incluindo uma lista de verificação de planejamento e desenvolvimento e teste de um plano de atualização.
ms.custom: ''
ms.date: 05/18/2018
ms.prod: sql
ms.technology: install
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 19c5b725-7400-4881-af8f-fd232ca28234
author: cawrites
ms.author: chadam
monikerRange: '>=sql-server-2016'
ms.openlocfilehash: 45b0ba2a207be68b0faaea0af0ba7592ae1f0f94
ms.sourcegitcommit: f29f74e04ba9c4d72b9bcc292490f3c076227f7c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/13/2021
ms.locfileid: "98172268"
---
# <a name="plan-and-test-the-database-engine-upgrade-plan"></a>Planejar e testar o plano de upgrade do mecanismo de banco de dados

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]
  
 Para executar uma atualização bem-sucedida do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] , independentemente da abordagem, o planejamento apropriado é obrigatório.  
  
## <a name="release-notes-and-known-upgrade-issues"></a>Notas de versão e problemas de upgrade conhecidos  
 Antes de fazer upgrade do [!INCLUDE[ssDE](../../includes/ssde-md.md)], examine:

- [Notas sobre a versão do SQL Server 2019](../../sql-server/sql-server-version-15-release-notes.md)
- [Notas de Versão do SQL Server 2017.](../../sql-server/sql-server-2017-release-notes.md) 
- [Notas de Versão do SQL Server 2016.](../../sql-server/sql-server-2016-release-notes.md)
- Artigo [Compatibilidade com versões anteriores do Mecanismo de Banco de Dados do SQL Server](../discontinued-database-engine-functionality-in-sql-server.md).  
  
## <a name="pre-upgrade-planning-checklist"></a>Lista de verificação de planejamento pré-upgrade  
 Antes de atualizar o [!INCLUDE[ssDE](../../includes/ssde-md.md)], examine a seguinte lista de verificação e os artigos associados. Estes artigos aplicam-se a todas as atualizações, independentemente do método de atualização, além de ajudar você a determinar o método de atualização mais apropriado: Atualização sem interrupção, atualização de nova instalação ou atualização in-loco. Por exemplo, talvez você não possa executar uma atualização in-loco ou uma atualização sem interrupção se estiver atualizando o sistema operacional, atualizando do SQL Server 2005 ou atualizando de uma versão de 32 bits do SQL Server. Para ver uma árvore de decisão, confira [Choose a Database Engine Upgrade Method](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md).  
  
-   **Requisitos de hardware e software:** examine os requisitos de hardware e software para a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esses requisitos podem ser encontrados em: [Requisitos de hardware e software para a instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md). Uma parte de qualquer ciclo de planejamento de atualização é considerar a atualização do hardware (um hardware mais novo é mais rápido e pode reduzir o licenciamento, seja devido ao menor número de processadores, seja devido à consolidação de banco de dados e servidor) e a atualização do sistema operacional. Esses tipos de alteração de hardware e software afetam o tipo de método de atualização que você escolhe.  
  
-   **Ambiente atual:** pesquise seu ambiente atual para entender os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estão sendo usados e os clientes que se conectam ao seu ambiente.  
  
    -   **Provedores de cliente:** embora a atualização não exija que você atualize o provedor de cada um de seus clientes, você pode optar por fazer isso. Se você estiver fazendo upgrade do [!INCLUDE[sql14](../../includes/sssql14-md.md)] ou anterior, os seguintes recursos do [!INCLUDE[sql15](../../includes/sssql16-md.md)] exigirão um provedor atualizado para cada cliente ou o provedor atualizado fornecerá funcionalidade adicional:  
  
       -   [Always Encrypted &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)  
  
       -   [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
       -   [Ouvintes do grupo de disponibilidade, conectividade de cliente e failover de aplicativo &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md)  
  
       -   Atualização de segurança do TLS  

   >[!NOTE]
   >A lista anterior também se aplica ao [!INCLUDE[sscurrent](../../includes/sscurrent-md.md)].
  
-   **Componentes de terceiros:** determine a compatibilidade de componentes de terceiros, como backup integrado.  
  
-   **Ambiente de destino:** verifique se seu ambiente de destino atende aos requisitos de hardware e software e se pode dar suporte aos requisitos do sistema original. Por exemplo, a atualização pode envolver a consolidação de várias instâncias do SQL Server em um instância única e nova do [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] ou a virtualização do ambiente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uma nuvem privada ou pública.  
  
-   **Edição:** determine a edição apropriada do [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] para a sua atualização, bem como os caminhos de atualização válidos para a atualização. Para obter informações detalhadas, consulte [Supported Version and Edition Upgrades](../../database-engine/install-windows/supported-version-and-edition-upgrades.md). Antes de atualizar de uma edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra, verifique se há suporte à funcionalidade usada atualmente na edição para a qual está atualizando.  
  
    > [!NOTE]  
    >  Quando você atualizar o [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] de uma versão anterior da edição do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise, escolha entre Enterprise Edition: Licenciamento baseado em núcleo e Enterprise Edition. Estas edições Enterprise só diferem com relação aos modos de licenciamento. Para saber mais, confira [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
-   **Compatibilidade com versões anteriores:** leia o artigo sobre compatibilidade com versões anteriores do mecanismo de banco de dados do [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] para examinar as alterações no comportamento entre o [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] e a versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da qual você está atualizando. Consulte [SQL Server Database Engine Backward Compatibility](../discontinued-database-engine-functionality-in-sql-server.md).  
  
-   **Assistente de Migração de Dados:** execute o Assistente de Migração de Dados para auxiliar no diagnóstico de problemas que podem bloquear o processo de atualização ou exigir modificação em scripts ou aplicativos existentes devido a uma alteração da falha.
    Você pode baixar o Assistente de Migração de Dados [aqui](https://aka.ms/get-dma).  
  
-   **Verificador de configuração do sistema:** execute o SCC (Verificador de Configuração do Sistema) do [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] para determinar se o programa de instalação do SQL Server detecta todos os problemas de bloqueio antes de você agendar a atualização. Para obter mais informações, consulte [Check Parameters for the System Configuration Checker](../../database-engine/install-windows/check-parameters-for-the-system-configuration-checker.md).  
  
-   **Atualizar tabelas com otimização de memória:** ao atualizar uma instância de banco de dados do SQL Server 2014 contendo tabelas com otimização de memória para o SQL Server 2016, o processo de atualização exige tempo adicional para converter as tabelas com otimização de memória no novo formato em disco (e o banco de dados fica offline enquanto essas etapas estão ocorrendo).   A quantidade de tempo depende do tamanho das tabelas com otimização de memória e da velocidade do subsistema de E/S. A atualização exige três tamanhos de operações de dados para atualizações de instalação nova e in-loco (a etapa 1 não é necessária para atualizações sem interrupção, mas as etapas 2 e 3 são obrigatórias):  
  
    1.  Execute a recuperação de banco de dados usando o formato em disco antigo (incluindo carregar todos os dados em tabelas com otimização de memória do disco na memória)  
  
    2.  Serialize os dados no disco no novo formato em disco  
  
    3.  Execute a recuperação de banco de dados usando o novo formato (incluindo carregar todos os dados em tabelas com otimização de memória do disco na memória)  
  
     Além disso, espaço insuficiente em disco durante esse processo causa a falha da recuperação. Verifique se há espaço suficiente em disco para armazenar o banco de dados existente mais armazenamento adicional igual ao tamanho atual dos contêineres no grupo de arquivos MEMORY_OPTIMIZED_DATA no banco de dados para realizar uma atualização in-loco ou ao anexar um banco de dados SQL Server 2014 a uma instância do SQL Server 2016. Use a consulta a seguir para determinar o espaço em disco atualmente necessário para o grupo de arquivos MEMORY_OPTIMIZED_DATA e, consequentemente, também a quantidade de espaço livre em disco necessária para uma atualização bem-sucedida:  
  
    ```  
    select cast(sum(size) as float)*8/1024/1024 'size in GB'   
    from sys.database_files  
    where data_space_id in (select data_space_id from sys.filegroups where type=N'FX')  
    ```  
  
## <a name="develop-and-test-the-upgrade-plan"></a>Desenvolver e testar o plano de upgrade  
 A melhor abordagem é tratar a atualização como trataria qualquer projeto de TI. Organize uma equipe de atualização que tenha a administração, a rede, ETL (extração, transformação e carregamento) e outras habilidades necessárias de banco de dados para a atualização. A equipe precisa:  
  
-   **Escolher o método de atualização:** Veja [Escolher um método de atualização do mecanismo de banco de dados](../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md).  
  
-   **Desenvolver um plano de reversão:** executar esse plano permite que você restaure o ambiente original se precisar fazer uma reversão.  
  
-   **Determinar os critérios de aceitação:** verifique se a atualização foi bem-sucedida antes de direcionar os usuários para o ambiente atualizado.  
  
-   **Testar o plano de atualização:** para testar o desempenho usando a carga de trabalho real, use o utilitário Microsoft SQL Server Distributed Replay. Esse utilitário pode usar vários computadores para reproduzir dados de rastreamento, simulando uma carga de trabalho crítica à missão. Ao executar uma reprodução em um servidor de teste antes e depois de uma atualização do SQL Server, você pode medir diferenças de desempenho e procurar alguma incompatibilidade que seu aplicativo possa ter com a atualização. Para obter mais informações, consulte [SQL Server Distributed Replay](../../tools/distributed-replay/sql-server-distributed-replay.md) e [Opções de linha de comando da ferramenta de administração &#40;Distributed Replay Utility&#41;](../../tools/distributed-replay/administration-tool-command-line-options-distributed-replay-utility.md).  
  
## <a name="next-steps"></a>Próximas etapas  
[Atualizar o Mecanismo de Banco de Dados](../../database-engine/install-windows/upgrade-database-engine.md) 
  
## <a name="additional-resources"></a>Recursos adicionais 
[Guia de Migração de Banco de Dados](https://aka.ms/datamigration)