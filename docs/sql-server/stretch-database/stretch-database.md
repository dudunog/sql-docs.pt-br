---
description: Stretch Database
title: Stretch Database
ms.date: 06/27/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database
ms.assetid: ce6db775-21a5-40bc-95a1-f560376d4ee2
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: 2338cfe80dafb68eefaba3d6302d4afc84a585c6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88497987"
---
# <a name="stretch-database"></a>Stretch Database
[!INCLUDE [sqlserver2016-windows-only](../../includes/applies-to-version/sqlserver2016-windows-only.md)]


  O Stretch Database migra seus dados frios de forma transparente e segura para a nuvem do Microsoft Azure.  
  
 Se você deseja começar a usar o Stretch Database imediatamente, veja [Comece executando o Assistente para Habilitar o Banco de Dados para Alongamento](../../sql-server/stretch-database/get-started-by-running-the-enable-database-for-stretch-wizard.md).  
  
## <a name="what-are-the-benefits-of-stretch-database"></a>Quais são os benefícios do Stretch Database?  
 O Stretch Database oferece os seguintes benefícios:  
  
 **Fornece disponibilidade econômica para dados sem vida**  
 Ampliar dados transacionais quentes e frios dinamicamente a partir do SQL Server para o Microsoft Azure com o SQL Server Stretch Database. Ao contrário do armazenamento de dados frios típicos, seus dados estão sempre online e disponível para consulta. Você pode fornecer linhas de tempo de retenção de dados mais longas sem muito trabalho para obter grandes tabelas, como o Histórico de Pedidos do Cliente. Aproveite o baixo custo do Azure, em vez de dimensionar amplos armazenamentos no local. Você escolhe a camada de preços e definições de configuração no Portal do Azure para manter o controle sobre o preço e os custos. Escale vertical ou horizontalmente conforme o necessário. Visite [Preços do SQL Server Stretch Database](https://azure.microsoft.com/pricing/details/sql-server-stretch-database/) para obter mais detalhes.  
  
 **Não requer alterações em consultas nem em aplicativos**  
 Acesse os dados do SQL Server diretamente, independentemente se é local ou ampliado para a nuvem.  Defina a política que determina onde os dados são armazenados, e o SQL Server tratará da movimentação dos dados em segundo plano. A tabela inteira está sempre online e é passível de consulta. Além disso, o Stretch Database não exige nenhuma mudança nos aplicativos ou nas consultas existentes. A localização dos dados é completamente transparente para o aplicativo.  
  
 **Simplifica a manutenção de dados local**  
 Reduza a necessidade de manutenção e armazenamento no local dos seus dados. Os backups de seus dados no local são executados mais rápido e são concluídos dentro da janela de manutenção. Os backups para a parte da nuvem de seus dados são executados automaticamente. Suas necessidades de armazenamento no local são reduzidas significativamente. O armazenamento do Azure pode ser 80% mais barato do que adicionar ao SSD local.  
  
 **Mantém seus dados seguros mesmo durante a migração**  
 Fique tranquilo para ampliar seus aplicativos mais importantes com segurança para a nuvem. O Always Encrypted do SQL Server fornece a criptografia para seus dados em movimento. A Segurança em Nível de Linha e outros recursos de segurança avançados do SQL Server também funcionam com o Stretch Database para proteger seus dados.  
  
## <a name="what-does-stretch-database-do"></a>Qual é a função do Stretch Database?  
 Depois de habilitar o Stretch Database para uma instância do SQL Server e um banco de dados, e selecionar pelo menos uma tabela, ele começa silenciosamente a migrar os dados frios para o Azure.  
  
-   Se você armazenar dados frios em uma tabela separada, poderá migrar a tabela inteira.  
  
-   Se a tabela contiver dados quentes e frios, será possível especificar uma função de filtro para selecionar as linhas a serem migradas.

**Você não precisa alterar as consultas existentes e aplicativos cliente.** Você continua a ter acesso direto aos dados locais e remotos, mesmo durante a migração de dados. Há uma pequena quantidade de latência para consultas remotas, mas você só encontra essa latência ao consultar os dados frios.

**O Stretch Database garante que nenhum dado será perdido** caso ocorra uma falha durante a migração. Ele também tem uma lógica de repetição para lidar com problemas de conexão que podem ocorrer durante a migração. Um modo de exibição de gerenciamento dinâmico fornece o status da migração.

**Você pode pausar a migração de dados** para solucionar problemas no servidor local ou para maximizar a largura de banda de rede disponível.  
  
 ![Visão geral do banco de dados de ampliação](../../sql-server/stretch-database/media/stretch-overview.png "Visão geral do banco de dados de ampliação")  
  
## <a name="is-stretch-database-for-you"></a>O Stretch Database serve para você?  
 Se você puder fazer as seguintes afirmações, o Stretch Database pode ajudar a atender às suas necessidades e resolver seus problemas.  
  
|Se você for um tomador de decisões|Se você for um DBA|  
|--------------------------------|---------------------|  
|Preciso manter dados transacionais por longos períodos.|O tamanho das minhas tabelas está saindo do controle.|  
|Às vezes, preciso consultar os dados frios.|Meus usuários dizem que querem ter acesso aos dados frios, mas eles raramente os utilizam.|  
|Tenho aplicativos, incluindo aplicativos mais antigos, que não quero atualizar.|Preciso continuar comprando e adicionando mais armazenamento.|  
|Quero encontrar uma forma de economizar dinheiro com armazenamento.|Não consigo fazer backup nem restaurar as tabelas grandes contidas no SLA.|  
  
## <a name="what-kind-of-databases-and-tables-are-candidates-for-stretch-database"></a>Quais tipos de bancos de dados e tabelas são candidatos ao Stretch Database?  
 O Stretch Database se destina a bancos de dados transacionais com grandes quantidades de dados frios, geralmente armazenados em uma pequena quantidade de tabelas. Essas tabelas podem conter mais de um bilhão de linhas.  
  
 Se você usa o recurso de tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use o Stretch Database para migrar toda ou parte da tabela de histórico associada para um armazenamento econômico no Azure. Para obter mais informações, veja [Gerenciar a retenção de dados históricos em tabelas temporais com controle de versão do sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md).  
  
 Use o Supervisor do Stretch Database, um recurso do Supervisor de Atualização do SQL Server 2016, para identificar os bancos de dados e tabelas candidatos ao Stretch Database. Para obter mais informações, veja [Identificar bancos de dados e tabelas para o Stretch Database executando o supervisor do Stretch Database](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md). Para saber mais sobre os possíveis problemas de bloqueio, veja [Limitações do Stretch Database](../../sql-server/stretch-database/limitations-for-stretch-database.md).  

## <a name="test-drive-stretch-database"></a>Faça o test drive do Stretch Database  
 **Faça o test drive do Stretch Database com o banco de dados de exemplo AdventureWorks** . Para obter o banco de dados de exemplo AdventureWorks, baixe pelo menos o arquivo de banco de dados e o arquivo de exemplos e scripts [aqui](https://github.com/microsoft/sql-server-samples/releases/tag/adventureworks). Depois de você restaurar o banco de dados de exemplo para uma instância do SQL Server 2016, descompacte o arquivo de exemplos e abra o arquivo Stretch DB Samples da pasta Stretch DB. Execute os scripts neste arquivo para verificar o espaço usado por seus dados antes e depois de habilitar o Stretch Database, para acompanhar o andamento da migração de dados e para confirmar que você pode continuar a consultar os dados existentes e a inserir novos dados durante e após a migração de dados.  
  
## <a name="next-step"></a>Próxima etapa  
 **Identifique bancos de dados e tabelas que são candidatos para o Stretch Database.** Baixe o Assistente de Migração de Dados e execute uma avaliação para identificar bancos de dados e tabelas candidatos ao Stretch Database. Para obter mais informações, veja [Identificar bancos de dados e tabelas para o Stretch Database executando o supervisor do Stretch Database](../../sql-server/stretch-database/stretch-database-databases-and-tables-stretch-database-advisor.md).  
  
  
