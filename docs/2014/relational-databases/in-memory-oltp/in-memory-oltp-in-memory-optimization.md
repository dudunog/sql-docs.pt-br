---
title: OLTP in-memory (otimização na memória) | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- In-Memory OLTP
- memory-optimized tables
ms.assetid: e1d03d74-2572-4a55-afd6-7edf0bc28bdb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 530e620be1a1c0f9d457eb23712c5228a3883d45
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175912"
---
# <a name="in-memory-oltp-in-memory-optimization"></a>OLTP na memória (otimização na memória)

  Novo no [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], o [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] pode melhorar significativamente o desempenho do aplicativo de banco de dados OLTP. O [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] é um mecanismo de banco de dados com otimização de memória integrado ao mecanismo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], otimizado para OLTP.

|||
|-|-|
|![Máquina Virtual do Azure](../../master-data-services/media/azure-virtual-machine.png "Máquina Virtual do Azure")|Você deseja experimentar o SQL Server 2016 ? Inscreva-se no Microsoft Azure e acesse **[Aqui](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)** para criar uma Máquina Virtual com o SQL Server 2016 já instalado. Você pode excluir a máquina virtual quando tiver terminado.|

 Para usar o [!INCLUDE[hek_2](../../../includes/hek-2-md.md)], é preciso definir uma tabela muito acessada como memória otimizada. As tabelas com otimização de memória são totalmente transacionais, duráveis e acessados usando o [!INCLUDE[tsql](../../../includes/tsql-md.md)] da mesma forma como ocorre com as tabelas baseadas em disco. Uma consulta pode fazer referência a tabelas com otimização de memória e tabelas baseadas em disco. Uma transação pode atualizar dados tanto nas tabelas com otimização de memória quanto as baseadas em disco. Os procedimentos armazenados que só fazem referência a tabelas com otimização de memória podem ser compilados nativamente em código de computador para mais melhorias de desempenho. O mecanismo do [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] é projetado para simultaneidade de sessão extremamente elevada para tipo de transações OLTP acionadas de uma camada intermediária altamente escalada. Para isso, ele usa estruturas de dados livre de travas e controle de simultaneidade otimista de diversas versões. O resultado é uma baixa latência previsível de menos de um milissegundo e alta taxa de transferência com escala linear para transações de banco de dados. O ganho de desempenho real depende de muitos fatores, mas é comum uma melhoria de 5 a 20 vezes no desempenho.

 A tabela a seguir resume os padrões de carga de trabalho que podem se beneficiar mais usando o [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]:

|Cenário de Implementação|Cenário de Implementação|Benefícios do [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]|
|-----------------------------|-----------------------------|-------------------------------------|
|Taxa de inserção de dados alta de várias conexões simultâneas.|Basicamente armazenamento somente de acréscimo.<br /><br /> Não é possível continuar com a inserção de carga de trabalho.|Eliminar a contenção.<br /><br /> Reduzir registros de log.|
|Desempenho de leitura e escala com inserções e atualizações em lote periódicas.|Operações de leitura de alto desempenho, especialmente quando cada solicitação de servidor tem várias operações de leitura para executar.<br /><br /> Incapaz de atender aos requisitos de aumento de escala.|Eliminar contenção quando novos dados chegam.<br /><br /> Recuperação de dados de latência mais baixa.<br /><br /> Minimizar o tempo de execução do código.|
|Processamento de lógica de negócios intensivo no servidor de banco de dados.|Inserir, atualizar e excluir carga de trabalho.<br /><br /> Computação intensiva dentro de procedimentos armazenados.<br /><br /> Contenção de leitura e gravação.|Eliminar a contenção.<br /><br /> Minimizar o tempo de execução de código para uma latência reduzida e maior taxa de transferência.|
|Baixa latência.|Exigir transações comerciais de baixa latência que as soluções típicas de banco de dados não podem realizar.|Eliminar a contenção.<br /><br /> Minimizar o tempo de execução do código.<br /><br /> Execução de código de baixa latência.<br /><br /> Recuperação eficaz de dados.|
|Gerenciamento do estado da sessão.|Inserção, atualização e pesquisas de pontos frequentes.<br /><br /> Carga de alta escala a partir de inúmeros servidores web sem monitoração de estado.|Eliminar a contenção.<br /><br /> Recuperação eficaz de dados.<br /><br /> Redução ou remoção opcional de E/S ao usar tabelas não duráveis|

 Para obter mais informações sobre cenários [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] em que o resultará em maiores ganhos de desempenho, consulte [padrões de carga de trabalho e considerações de migração comuns de OLTP na memória](https://msdn.microsoft.com/library/dn673538.aspx).

 O [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] aumentará mais o desempenho no OLTP com transações de curta execução.

 Os padrões de programação que o [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] melhorará incluem cenários de simultaneidade, pesquisas de pontos, cargas de trabalho em que há muitas inserções e atualizações e lógica de negócios em procedimentos armazenados.

 A integração com o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] significa que você pode ter tanto tabelas com otimização de memória quanto tabelas baseadas em disco no mesmo banco de dados e consultar ambos os tipos de tabela.

 No [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] há limitações na área da superfície do [!INCLUDE[tsql](../../../includes/tsql-md.md)] com suporte para [!INCLUDE[hek_2](../../../includes/hek-2-md.md)].

 O [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] obtém ganhos significativos de desempenho e escalabilidade ao usar:

-   Algoritmos otimizados para acessar dados residentes em memória.

-   Controle de simultaneidade otimista que elimina bloqueios lógicos.

-   Objetos livres de bloqueio que eliminam todas as travas e bloqueios físicos. Os threads que executam o trabalho transacional não usam bloqueios ou travas para controle de simultaneidade.

-   Procedimentos armazenados compilados nativamente, os quais têm um desempenho significativamente melhor do que os procedimentos armazenados interpretados, ao acessar uma tabela com otimização de memória.

> [!IMPORTANT]
>  Algumas alterações de sintaxe em tabelas e procedimentos armazenados serão exigidas para usar o [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]. Para obter mais informações, veja [Migrando para o OLTP in-memory](migrating-to-in-memory-oltp.md). Antes de tentar migrar uma tabela baseada em disco para uma tabela com otimização de memória, leia [Determinando se uma tabela ou um procedimento armazenado deve ser movido para o OLTP in-memory](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md) para ver quais tabelas e procedimentos armazenados se beneficiarão do [!INCLUDE[hek_2](../../../includes/hek-2-md.md)].

## <a name="in-this-section"></a>Nesta seção
 Esta seção fornece informações sobre os seguintes conceitos:

|Tópico|Descrição|
|-----------|-----------------|
|[Requisitos para usar tabelas com otimização de memória](memory-optimized-tables.md)|Aborda os requisitos de hardware e software, e as diretrizes para usar tabelas com otimização de memória.|
|[Usando OLTP na Memória em um Ambiente de VM](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)|Abrange o uso do [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] em um ambiente virtualizado.|
|[Exemplos de código de OLTP na memória](in-memory-oltp-code-samples.md)|Contém exemplos de código que mostram como criar e usar uma tabela com otimização de memória.|
|[Tabelas com otimização de memória](memory-optimized-tables.md)|Apresenta tabelas com otimização de memória.|
|[Variáveis de tabela com otimização de memória](../../database-engine/memory-optimized-table-variables.md)|Exemplo de código mostrando como usar uma variável de tabela com otimização de memória em vez de uma variável de tabela tradicional para reduzir o uso de tempdb.|
|[Índices em tabelas com otimização de memória](../../database-engine/indexes-on-memory-optimized-tables.md)|Incorpora índices com otimização de memória.|
|[procedimentos armazenados compilados nativamente](natively-compiled-stored-procedures.md)|Apresenta procedimentos armazenados compilados de modo nativo.|
|[Gerenciando memória para OLTP na memória](../../database-engine/managing-memory-for-in-memory-oltp.md)|Compreendendo e gerenciando o uso de memória no sistema.|
|[Criando e gerenciando armazenamento para objetos com otimização de memória](creating-and-managing-storage-for-memory-optimized-objects.md)|A aborda os arquivos delta e de dados, que armazenam informações sobre transações em tabelas com otimização de memória.|
|[Backup, restauração e recuperação de tabelas com otimização de memória](restore-and-recovery-of-memory-optimized-tables.md)|Discute backup, restauração e recuperação de tabelas com otimização de memória.|
|[Suporte ao Transact-SQL para OLTP na memória](transact-sql-support-for-in-memory-oltp.md)|Discute o suporte do [!INCLUDE[tsql](../../../includes/tsql-md.md)] para [!INCLUDE[hek_2](../../../includes/hek-2-md.md)].|
|[Suporte de alta disponibilidade para bancos de dados OLTP na memória](high-availability-support-for-in-memory-oltp-databases.md)|Discute grupos de disponibilidade e clustering de failover no [!INCLUDE[hek_2](../../../includes/hek-2-md.md)].|
|[Suporte ao SQL Server para OLTP na memória](sql-server-support-for-in-memory-oltp.md)|Lista a sintaxe nova e atualizada, e os recursos que oferecem suporte a tabelas com otimização de memória.|
|[Migrando para OLTP na memória](migrating-to-in-memory-oltp.md)|Aborda como migrar tabelas baseadas em disco para tabelas com otimização de memória.|

 Mais informações sobre o [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] estão disponíveis em:

-   [Microsoft?? SQL Server?? Guia do produto 2014](https://www.microsoft.com/download/confirmation.aspx?id=39269)

-   [Blog do OLTP in-memory](https://go.microsoft.com/fwlink/?LinkId=311696)

-   [OLTP na memória-padrões comuns de carga de trabalho e considerações de migração](https://msdn.microsoft.com/library/dn673538.aspx)

-   [Visão geral interna do OLTP na memória do SQL Server](https://download.microsoft.com/download/8/3/6/8360731A-A27C-4684-BC88-FC7B5849A133/SQL_Server_2016_In_Memory_OLTP_White_Paper.pdf)
    <!--
         (https://download.microsoft.com/download/8/3/6/8360731A-A27C-4684-BC88-FC7B5849A133/SQL_Server_2016_In_Memory_OLTP_White_Paper.pdf)
         (/sql/relational-databases/in-memory-oltp/sql-server-in-memory-oltp-internals-for-sql-server-2016?view=sql-server-2016)
    -->

## <a name="see-also"></a>Consulte Também
 [Recursos de banco de dados](../database-features.md)


