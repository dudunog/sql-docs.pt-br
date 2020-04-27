---
title: Tabelas e índices particionados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- partitioned tables [SQL Server], about partitioned tables
- partitioned indexes [SQL Server], architecture
- partitioned tables [SQL Server], architecture
- partitioned indexes [SQL Server], about partitioned indexes
ms.assetid: cc5bf181-18a0-44d5-8bd7-8060d227c927
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5f96f82919b9f4a130ce8a533e6ffcf31e765f5f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65092036"
---
# <a name="partitioned-tables-and-indexes"></a>Partitioned Tables and Indexes
  O[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte ao particionamento de tabelas e índices. Os dados de tabelas e índices particionados são divididos em unidades que podem ser difundidas por mais de um grupo de arquivos em um banco de dados. Os dados são particionados horizontalmente, de forma que os grupos de linhas são mapeados em partições individuais. Todas as partições de um único índice ou de uma única tabela devem residir no mesmo banco de dados. A tabela ou o índice é tratado como uma única entidade lógica quando são executadas consultas ou atualizações nos dados. As tabelas e os índices particionados não estão disponíveis em todas as edições de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
> [!IMPORTANT]  
>  O[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] oferece suporte a até 15.000 partições por padrão. Nas versões anteriores do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o número de partições foi limitado a 1.000 por padrão. Nos sistemas baseados em x86, a criação de uma tabela ou de um índice com mais de 1000 partições é possível, mas não tem suporte.  
  
## <a name="benefits-of-partitioning"></a>Benefícios do particionamento  
 O particionamento de tabelas ou índices grandes pode ter a capacidade de gerenciamento e os benefícios de desempenho a seguir.  
  
-   Você pode transferir ou acessar subconjuntos de dados de forma rápida e eficaz e, ao mesmo tempo, manter a integridade de uma coleção de dados. Por exemplo, uma operação como o carregamento de dados de um sistema OLTP para OLAP leva apenas segundos, em vez dos minutos ou horas necessários quando os dados não estão paticionados.  
  
-   Você pode executar operações de manutenção mais rapidamente em uma ou mais partições. As operações são mais eficientes porque elas visam apenas estes subconjuntos de dados, e não a tabela inteira. Por exemplo, você pode optar por compactar dados em uma ou mais partições ou recriar uma ou mais partições de um índice.  
  
-   Você pode aprimorar o desempenho de consultas com base nos tipos de consultas executadas com frequência e em sua configuração de hardware. Por exemplo, o otimizador de consulta pode processar consultas de junção de igualdade entre duas ou mais tabelas particionadas mais rápido quando as colunas de particionamento nas tabelas são iguais, porque as próprias partições podem ser unidas.  
  
     Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa classificação de dados para operações de E/S, ele classifica os dados primeiro pela partição. O[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] acessa uma unidade de cada vez e isso pode reduzir o desempenho. Para melhorar o desempenho da classificação de dados, distribua os arquivos de dados de suas partições em mais de um disco configurando um RAID. Dessa maneira, embora o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ainda classifique os dados por partição, ele pode acessar todas as unidades de cada partição ao mesmo tempo.  
  
     Além disso, você pode melhorar o desempenho habilitando o escalonamento de bloqueios em nível de partição em, e não em uma tabela inteira. Isso pode reduzir a contenção de bloqueio na tabela.  
  
## <a name="components-and-concepts"></a>Componentes e conceitos  
 As condições a seguir são aplicáveis ao particionamento de tabela e de índice.  
  
 Função de partição  
 Um objeto de banco de dados que define como as linhas de uma tabela ou índice são mapeadas para um conjunto de partições, com base nos valores de determinada coluna, chamada de coluna de particionamento. Ou seja, a função de partição define o número de partições que a tabela terá e como serão definidos os limites das partições. Por exemplo, considerando uma tabela que contém dados de ordem de venda, você pode desejar particionar a tabela em doze (mensalmente) partições com base em uma coluna `datetime` como uma data de vendas.  
  
 Esquema de partição  
 Um objeto de banco de dados que mapeia as partições de uma função de partição para um conjunto de grupos de arquivos. O principal motivo para colocar suas partições em grupos de arquivos separados é para garantir que poderá efetuar operações de backup em partições de forma independente. Isso porque se pode executar backups em grupos de arquivos individuais.  
  
 Coluna de particionamento  
 A coluna de uma tabela ou índice que uma função de partição usa para particionar a tabela ou índice. Colunas computadas que participam de uma função de partição devem ser marcadas explicitamente como PERSISTED. Todos os tipos de dados que são válidos para uso como colunas de índice podem ser usados como uma coluna de particionamento, exceto `timestamp`. Os tipos de dados `ntext`, `text`, `image`, `xml`, `varchar(max)`, `nvarchar(max)` ou `varbinary(max)` não podem ser especificados. Também, não podem ser especificados o tipo definido pelo usuário do CLR (Common Language Runtime) do Microsoft .NET Framework e colunas de tipo de dados do alias.  
  
 Índice alinhado  
 Um índice que é baseado no mesmo esquema de partição que sua tabela correspondente. Quando uma tabela e seus índices estão em alinhamento, o SQL Server pode alternar partições rápida e eficientemente e, ao mesmo tempo, manter a estrutura de partição da tabela e de seus índices. Um índice não precisa participar na mesma função de partição nomeada para ser alinhado com sua tabela base. Entretanto, a função de partição de um índice e a tabela base devem ser essencialmente as mesmas, em que 1) os argumentos das funções de partição têm o mesmo tipo de dados, 2) eles definem o mesmo número de partições, e 3) eles definem os mesmos valores de limite para as partições.  
  
 Índice não alinhado  
 Um índice particionado independentemente de sua tabela correspondente. Quer dizer, o índice tem um esquema de partição diferente ou é colocado em um grupo de arquivos separado da tabela base. A criação de um índice particionado não alinhado pode ser útil nos seguintes casos:  
  
-   A tabela base não foi particionada.  
  
-   A chave de índice é exclusiva e não contém a coluna de particionamento da tabela.  
  
-   Você deseja que a tabela base participe de junções colocadas com mais tabelas que usam colunas de junção diferentes.  
  
 Eliminação de partição  
 O processo pelo qual o otimizador de consulta acessa apenas as partições relevantes para satisfazer os critérios de filtro da consulta.  
  
## <a name="performance-guidelines"></a>Diretrizes de desempenho  
 O limite novo, superior de 15.000 partições afeta a memória, operações de índice particionadas, comandos DBCC e consultas. Esta seção descreve as implicações de desempenho de aumentar o número de partições acima de 1.000 e fornece soluções alternativas quando necessário. Com o limite no número máximo de partições elevado para 15.000, você pode armazenar dados por mais tempo. Porém, você só deve reter dados enquanto necessário e manter um equilíbrio entre desempenho e número de partições.  
  
### <a name="memory-usage-and-guidelines"></a>Uso de memória e diretrizes  
 É recomendável usar pelo menos 16 GB de RAM se um número grande de partições estiver em uso. Se o sistema não tiver memória suficiente, instruções DML (linguagem de manipulação de dados), instruções DDL (linguagem de definição de dados) e outras operações poderão falhar devido à memória insuficiente. Sistemas com 16 GB de RAM que executam muitos processos com uso intenso de memória podem ficar sem memória em operações executadas em um número grande de partições. Portanto, quanto mais memória você tiver acima de 16 GB, menor será a probabilidade de encontrar problemas de desempenho e memória.  
  
 As limitações de memória podem afetar o desempenho ou a capacidade do SQL Server de criar um índice particionado. Este será o caso especialmente quando o índice não está alinhado com sua tabela base ou não está alinhado com o índice clusterizado, se a tabela já tiver um índice clusterizado aplicado a ela.  
  
### <a name="partitioned-index-operations"></a>Operações de índice particionado  
 As limitações de memória podem afetar o desempenho ou a capacidade do SQL Server de criar um índice particionado. Este é especialmente o caso com índices não alinhados. É possível criar e reconstruir índices não alinhados em uma tabela com mais de 1.000 partições, mas não há suporte para isso. Fazer isso pode provocar degradação do desempenho ou consumo excessivo de memória durante essas operações.  
  
 A criação e a recompilação de índices alinhados poderão demorar mais para serem executadas à medida que aumentar o número de partições. É recomendável não executar vários comandos de índice de criação e recriação ao mesmo tempo porque você pode encontrar problemas de desempenho e memória.  
  
 Quando o SQL Server executar uma classificação para criar índices particionados, ele criará primeiro uma tabela de classificação para cada partição. Ele criará as tabelas de classificação no respectivo grupo de arquivos de cada partição ou no `tempdb`, se a opção de índice SORT_IN_TEMPDB for especificada. Cada tabela de classificação exige uma quantia mínima de memória para construir. Quando você estiver construindo um índice particionado que está alinhado com a tabela base, uma tabela de classificação por vez será criada, usando menos memória. Porém, quando você estiver construindo um índice particionado não alinhado, as tabelas de classificação serão criadas ao mesmo tempo. Como resultado, deve haver memória suficiente para controlar essas classificações simultâneas. Quanto maior o número de partições, mais memória será necessária. O tamanho mínimo para cada tabela de classificação, para cada partição é de 40 páginas, com 8 quilobites por página. Por exemplo, um índice particionado não alinhado com 100 partições requer memória suficiente para classificar serialmente 4.000 (40 x 100) páginas ao mesmo tempo. Se essa memória estiver disponível, a operação de construção terá sucesso, mas o desempenho poderá ser afetado. Se essa memória não estiver disponível, a operação de criação falhará. Como alternativa, um índice particionado alinhado com 100 partições requer apenas memória suficiente para classificar serialmente 40 páginas, porque as classificações não são executadas ao mesmo tempo.  
  
 Para ambos os índices, alinhados e não alinhados, os requisitos de memória poderão ser maiores se o SQL Server aplicar graus de paralelismo à operação de criação em um computador com multiprocessador. Isso ocorre porque quanto maior os graus de paralelismo, maior será o requisito de memória. Por exemplo, se o SQL Server define os graus de paralelismo como 4, um índice particionado não alinhado com 100 partições requer memória suficiente para quatro processadores para classificar serialmente 4.000 páginas, ao mesmo tempo, ou 16.000 páginas. Se o índice particionado for alinhado, o requisito de memória será reduzido para quatro processadores classificando 40 páginas, 160 (4 x 40) páginas. Você pode usar a opção de índice MAXDOP para reduzir os graus de paralelismo manualmente.  
  
### <a name="dbcc-commands"></a>Comandos DBCC  
 Com um número maior de partições, os comandos DBCC podem demorar mais para serem executados à medida que aumentar o número de partições.  
  
### <a name="queries"></a>Consultas  
 Consultas que usam a eliminação de partição podem ter desempenho comparável ou aprimorado com número maior de partições. Consultas que não usam a eliminação de partição podem levar mais tempo para executar à medida que o número de partições aumenta.  
  
 Por exemplo, digamos que uma tabela tem 100 milhões de linhas e colunas `A`, `B`e `C`. No cenário 1, a tabela é dividida em 1.000 partições na coluna `A`. No cenário 2, a tabela é dividida em 10.000 partições na coluna `A`. Uma consulta na tabela que tem uma cláusula WHERE filtrada na coluna `A` executará a eliminação de partição e examinará uma partição. Essa mesma consulta pode ser executada mais rapidamente no cenário 2, pois há menos linhas a serem examinadas em uma partição. Uma consulta com uma cláusula WHERE filtrada na coluna B examinará todas as partições. A consulta pode ser executada mais rapidamente no cenário 1 do que no cenário 2, pois há menos partições a serem examinadas.  
  
 As consultas que usam operadores como TOP ou MAX/MIN em colunas que não sejam a coluna de particionamento podem sofrer redução do desempenho com o particionamento porque todas as partições precisam ser avaliadas.  
  
## <a name="behavior-changes-in-statistics-computation-during-partitioned-index-operations"></a>Alterações de comportamento em computação de estatísticas durante operações de índice particionadas  
 A partir do [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], as estatísticas não são criadas por meio do exame de todas as linhas da tabela quando um índice particionado é criado ou reconstruído. Em vez disso, o otimizador de consultas usa o algoritmo de amostragem padrão para gerar estatísticas. Depois de atualizar um banco de dados com índices particionados, você pode notar uma diferença nos dados de histograma destes índices. Esta alteração no comportamento pode não afetar o desempenho de consulta. Para obter estatísticas em índices particionados por meio do exame de todas as linhas da tabela, use CREATE STATISTICS ou UPDATE STATISTICS com a cláusula FULLSCAN.  
  
## <a name="related-tasks"></a>Related Tasks  
  
|||  
|-|-|  
|**Tarefas**|**Tópico**|  
|Descreve como criar funções de partição e esquemas de partição, e depois aplicá-los a uma tabela e índice.|[Criar tabelas e índices particionados](create-partitioned-tables-and-indexes.md)|  
|||  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Você pode localizar os livros brancos a seguir em estratégias e implementações úteis de tabelas e índices particionados.  
  
-   [Estratégias de tabelas e índices particionados usando o SQL Server 2008](https://msdn.microsoft.com/library/dd578580\(SQL.100\).aspx)  
  
-   [Como implementar uma janela deslizante automática](https://msdn.microsoft.com/library/aa964122\(SQL.90\).aspx)  
  
-   [Carregamento em massa em uma tabela particionada](https://msdn.microsoft.com/library/cc966380.aspx)  
  
-   [Aperfeiçoamentos de processamento de consultas em tabelas e índices particionados](https://msdn.microsoft.com/library/ms345599.aspx)  
  
-   [10 principais práticas recomendadas para a criação de um Data Warehouse relacional em grande escala](http://sqlcat.com/top10lists/archive/2008/02/06/top-10-best-practices-for-building-a-large-scale-relational-data-warehouse.aspx)  
  
  
