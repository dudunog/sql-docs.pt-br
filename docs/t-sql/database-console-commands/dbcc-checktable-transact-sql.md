---
title: DBCC CHECKTABLE (Transact-SQL) | Microsoft Docs
ms.date: 11/14/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.custom: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CHECKTABLE_TSQL
- DBCC_CHECKTABLE_TSQL
- DBCC CHECKTABLE
- CHECKTABLE
dev_langs:
- TSQL
helpviewer_keywords:
- indexed views [SQL Server], DBCC CHECKTABLE
- page integrity checks [SQL Server]
- consistency [SQL Server], tables
- consistency [SQL Server], indexed views
- DBCC CHECKTABLE statement
- integrity [SQL Server]
- low overhead checks
- table integrity checks [SQL Server]
ms.assetid: 0d6cb620-eb58-4745-8587-4133a1b16994
author: pmasl
ms.author: umajay
ms.openlocfilehash: b882a0f234b6c30b61bc9875bb6b805baeaeb989
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754817"
---
# <a name="dbcc-checktable-transact-sql"></a>DBCC CHECKTABLE (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Verifica a integridade de todas as páginas e estruturas que compõem a tabela ou a exibição indexada.

![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
    
## <a name="syntax"></a>Sintaxe    
    
```syntaxsql
DBCC CHECKTABLE     
(    
    table_name | view_name    
    [ , { NOINDEX | index_id }    
     |, { REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD }     
    ]     
)    
    [ WITH     
        { [ ALL_ERRORMSGS ]    
          [ , EXTENDED_LOGICAL_CHECKS ]     
          [ , NO_INFOMSGS ]    
          [ , TABLOCK ]     
          [ , ESTIMATEONLY ]     
          [ , { PHYSICAL_ONLY | DATA_PURITY } ]     
          [ , MAXDOP = number_of_processors ]    
        }    
    ]    
```    
    
## <a name="arguments"></a>Argumentos    
 *table_name* | *view_name*  
 É a tabela ou exibição indexada para a qual executar verificações de integridade. Os nomes de tabela ou de exibição precisam estar em conformidade com as regras para [identificadores](../../relational-databases/databases/database-identifiers.md).  
    
NOINDEX  
 Especifica que não devem ser executadas verificações intensivas de índices não clusterizados de tabelas de usuário. Isto reduz o tempo de execução geral. NOINDEX não afeta tabelas do sistema porque as verificações de integridade sempre são executadas em todos os índices de tabela do sistema.  
    
 *index_id*  
 É o número da ID (identificação) do índice para o qual executar verificações de integridade. Se *index_id* for especificado, o DBCC CHECKTABLE executará verificações de integridade somente naquele índice, juntamente com o índice de heap ou clusterizado.  
    
REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD  
 Especifica que DBCC CHECKTABLE repara os erros encontrados. Para usar uma opção de reparo, o banco de dados deve estar em modo de usuário único.  
    
REPAIR_ALLOW_DATA_LOSS  
 Tenta reparar todos os erros relatados. Esses reparos podem provocar alguma perda de dados.  
    
REPAIR_FAST  
 A sintaxe é mantida apenas para compatibilidade com versões anteriores. Nenhuma ação de reparo é executada.  
    
REPAIR_REBUILD  
 Executa reparos que não têm nenhuma possibilidade de perda de dados. Isso pode incluir reparos rápidos, como reparo de linhas perdidas em índices não clusterizados e reparos mais demorados, como a recriação de um índice.  
 Esse argumento não repara erros que envolvem dados de FILESTREAM.  
    
 > [!NOTE]  
 > Use as opções REPAIR apenas como um último recurso. Para reparar erros, recomendamos restaurar de um backup. Operações de reparo não consideram nenhuma das restrições que podem existir em tabelas ou entre tabelas. Se a tabela especificada estiver envolvida em uma ou mais restrições, recomendamos a execução de `DBCC CHECKCONSTRAINTS` após uma operação de reparo.
 > Se for necessário usar REPAIR, execute `DBCC CHECKTABLE` sem uma opção de reparo para localizar o nível de reparo a ser usado. Se você pretende usar o nível REPAIR_ALLOW_DATA_LOSS, recomendamos que você faça backup do banco de dados antes de executar `DBCC CHECKTABLE` com essa opção.  
    
ALL_ERRORMSGS  
 Exibe um número ilimitado de erros. Todas as mensagens de erro são exibidas por padrão. Especificar ou omitir esta opção não têm nenhum efeito.  
    
EXTENDED_LOGICAL_CHECKS  
 Se o nível de compatibilidade for 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) ou superior, executará verificações de consistência lógica em uma exibição indexada, em índices XML e em índices espaciais, quando presentes.  
 Para obter mais informações, confira *Executando verificações de consistência lógica em índices* na seção [Comentários](#remarks) mais adiante neste tópico.  
    
NO_INFOMSGS  
 Suprime todas as mensagens informativas.  
    
TABLOCK  
 Faz com que DBCC CHECKTABLE obtenha um bloqueio de tabela compartilhada em vez de usar um instantâneo do banco de dados interno. TABLOCK faz com que DBCC CHECKTABLE seja executado com mais rapidez em uma tabela sob carga pesada, mas reduz a simultaneidade disponível na tabela durante a execução de DBCC CHECKTABLE.  
    
ESTIMATEONLY  
 Exibe a quantidade estimada de espaço do tempdb necessária para executar DBCC CHECKTABLE com todas as outras opções especificadas.  
    
PHYSICAL_ONLY  
 Limita a verificação à integridade da estrutura física da página, dos cabeçalhos de registros e da estrutura física de árvores B. Criada para fornecer uma pequena verificação de sobrecarga da consistência física da tabela, essa verificação também pode detectar páginas interrompidas e falhas comuns de hardware que podem comprometer os dados. Uma execução completa de DBCC CHECKTABLE pode demorar muito mais em versões anteriores. Esse comportamento ocorre devido às seguintes razões:  
 -   As verificações lógicas são mais abrangentes.  
 -   Algumas das estruturas subjacentes a serem verificadas são mais complexas.  
 -   Foram introduzidas muitas verificações novas para incluir os novos recursos.  
   
O uso da opção PHYSICAL_ONLY pode provocar um tempo de execução muito mais curto para DBCC CHECKTABLE em tabelas grandes. Portanto é recomendado para uso frequente em sistemas de produção. Ainda é recomendável executar um DBCC CHECKTABLE completo periodicamente. A frequência dessas execuções depende de fatores específicos aos negócios e ambientes de produção individuais. PHYSICAL_ONLY sempre implica em NO_INFOMSGS e não é permitido com nenhuma das opções de reparo.  
    
 > [!NOTE]  
 > A especificação de PHYSICAL_ONLY faz com que DBCC CHECKTABLE ignore todas as verificações de dados FILESTREAM.  
    
DATA_PURITY  
 Faz com que o DBCC CHECKTABLE verifique valores de colunas na tabela que não são válidos ou estão fora do intervalo. Por exemplo, o DBCC CHECKDB detecta colunas com valores de data e hora que são maiores ou menores do que o intervalo aceitável para o tipo de dados **datetime** ou **decimal** ou colunas de tipo de dados numérico aproximado com valores de escala ou de precisão que não são válidos.  
 Verificações de integridade de valor de coluna são habilitadas por padrão e não exigem a opção DATA_PURITY. Para bancos de dados atualizados de versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], é possível usar DBCC CHECKTABLE WITH DATA_PURITY para localizar e corrigir erros em uma tabela específica. No entanto verificações de valores de colunas na tabela não são habilitadas por padrão até que o DBCC CHECKDB WITH DATA_PURITY tenha sido executado sem erros no banco de dados. Depois disto, por padrão, DBCC CHECKDB e DBCC CHECKTABLE verificam a integridade de valores de colunas.  
 Erros de validação relatados por essa opção não podem ser corrigidos usando opções de reparo de DBCC. Para obter informações sobre como corrigir esses erros manualmente, confira o artigo 923247 da Base de Dados de Conhecimento: [Solução de problemas do erro 2570 do DBCC no SQL Server 2005 e em versões posteriores](https://support.microsoft.com/kb/923247).  
 Se PHYSICAL_ONLY estiver especificado, não serão executadas verificações de integridade de colunas.  
    
MAXDOP  
 **Aplica-se ao**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (No [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 e posterior).  
 
 Substitui a opção de configuração **max degree of parallelism** de **sp_configure** da instrução. O MAXDOP pode exceder o valor configurado com sp_configure. Se MAXDOP exceder o valor configurado com o Resource Governor, o Mecanismo de Banco de Dados usará o valor de MAXDOP do Resource Governor, descrito em ALTER WORKLOAD GROUP (Transact-SQL). Todas as regras semânticas usadas com a opção de configuração grau máximo de paralelismo são aplicáveis ao usar a dica de consulta MAXDOP. Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).  
    
 > [!NOTE]  
 > Se MAXDOP estiver definido como 0, o servidor escolherá o max degree of parallelism.  
    
## <a name="remarks"></a>Comentários    
    
> [!NOTE]    
> Para executar DBCC CHECKTABLE em cada tabela no banco de dados, use [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md).    
    
Para a tabela especificada, DBCC CHECKTABLE verifica o seguinte:
-   Páginas de dados de estouro de linha, índice, em linha e LOB estão vinculadas corretamente.    
-   Os índices estão na ordem de classificação correta.    
-   Os ponteiros são consistentes.    
-   Os dados em cada página são razoáveis, inclusive colunas computadas.    
-   Deslocamentos de página são razoáveis.    
-   Cada linha da tabela base tem uma linha correspondente em cada índice não clusterizado e vice-versa.    
-   Cada linha de um índice ou tabela particionada está na partição correta.    
-   A consistência no nível do link entre o sistema de arquivos e a tabela ao armazenar dados **varbinary(max)** no sistema de arquivos usando FILESTREAM.    
    
## <a name="performing-logical-consistency-checks-on-indexes"></a>Executando verificações de consistência lógica em índices    
A verificação de consistência lógica em índices varia de acordo com o nível de compatibilidade do banco de dados, da seguinte maneira:
-   Se o nível de compatibilidade for 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) ou superior:    
    -   A menos que NOINDEX esteja especificado, DBCC CHECKTABLE executará verificações de consistência física e lógica em uma única tabela e em todos os índices não clusterizados. Entretanto, em índices XML, índices espaciais e exibições indexadas, por padrão são executadas somente as verificações de consistência física.    
    -   Se WITH EXTENDED_LOGICAL_CHECKS estiver especificado, verificações lógicas serão executadas em uma exibição indexada, em índices XML e em índices espaciais, quando presentes. Por padrão, as verificações de consistência física são executadas antes das verificações de consistência lógica. Se NOINDEX também estiver especificado, apenas as verificações lógicas serão executadas.    
         Essas verificações de consistência lógica comparam a tabela de índice interna do objeto de índice com a tabela do usuário à qual se está fazendo referência. Para localizar linhas externas, uma consulta interna é construída para executar uma interseção completa das tabelas internas e do usuário. A execução dessa consulta pode afetar bastante o desempenho e não é possível controlar seu andamento. Portanto, recomendamos especificar WITH EXTENDED_LOGICAL_CHECKS apenas se você suspeitar de problemas de índice que não estão relacionados à dano físico ou se as somas de verificação em nível de página foram desativadas e você suspeitar de dano de hardware em nível de coluna.    
    -   Se o índice for filtrado, DBCC CHECKDB executará verificações de consistência para verificar se as entradas do índice atendem ao predicado do filtro.   
      
- Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], as verificações adicionais em colunas computadas persistentes, em colunas de UDT e em índices filtrados não serão executadas por padrão, para evitar as avaliações de expressão caras. Essa alteração reduz significativamente a duração de CHECKDB em bancos de dados que contêm esses objetos. No entanto, as verificações de consistência física desses objetos sempre são concluídas. Somente quando a opção EXTENDED_LOGICAL_CHECKS for especificada as avaliações de expressão serão executadas além das verificações lógicas já presentes (exibição indexada, índices XML e índices espaciais) como parte da opção EXTENDED_LOGICAL_CHECKS.
-  Se o nível de compatibilidade for 90 ([!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]) ou inferior, a menos que NOINDEX esteja especificado, DBCC CHECKTABLE executará verificações de consistência física e lógica em uma única tabela ou exibição indexada e em todos os índices XML e não clusterizados. Não há suporte para índices espaciais.
    
 **Para saber o nível de compatibilidade de um banco de dados**    
[Exibir ou alterar o nível de compatibilidade de um banco de dados](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)    
    
## <a name="internal-database-snapshot"></a>Instantâneo de banco de dados interno    
DBCC CHECKTABLE usa um instantâneo do banco de dados interno para fornecer a consistência transacional necessária ao executar essas verificações. Para obter mais informações, confira [Exibir o tamanho do arquivo esparso de um instantâneo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) e a seção "Uso de instantâneo de banco de dados interno do DBCC" em [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md).
Se um instantâneo não puder ser criado, ou se a opção TABLOCK estiver especificada, DBCC CHECKTABLE irá adquirir um bloqueio de tabela compartilhada para obter a consistência necessária.
    
> [!NOTE]    
> Se DBCC CHECKTABLE for executado no tempdb, ele precisará adquirir um bloqueio de tabela compartilhada. Isso porque, por razões de desempenho, instantâneos do banco de dados não estão disponíveis em tempdb. Isso significa que não é possível obter a consistência transacional exigida.    
    
## <a name="checking-and-repairing-filestream-data"></a>Verificando e reparando dados FILESTREAM    
Quando FILESTREAM está habilitado para um banco de dados e uma tabela, é possível armazenar opcionalmente BLOBs (objetos binários grandes) **varbinary(max)** no sistema de arquivos. Ao usar DBCC CHECKTABLE em uma tabela que armazena BLOBs no sistema de arquivos, DBCC verifica a consistência em nível de vinculação entre o sistema de arquivos e o banco de dados.
Por exemplo, se uma tabela contiver uma coluna **varbinary(max)** que use o atributo FILESTREAM, o DBCC CHECKDB verificará se existe um mapeamento de um-para-um entre os diretórios e os arquivos do sistema de arquivos e entre as linhas e as colunas da tabela e os valores das colunas. DBCC CHECKTABLE poderá reparar dano se você especificar a opção REPAIR_ALLOW_DATA_LOSS. Para reparar danos de FILESTREAM, o DBCC excluirá todas as linhas da tabela que não têm dados do sistema de arquivos e excluirá todos os diretórios e arquivos que não são mapeados para uma linha de tabela, coluna ou valor de coluna.
    
## <a name="checking-objects-in-parallel"></a>Verificando objetos em paralelo    
Por padrão, DBCC CHECKTABLE executa a verificação paralela de objetos. O grau de paralelismo é automaticamente determinado pelo processador de consulta. O grau máximo de paralelismo é configurado da mesma maneira como o de consultas paralelas. Para restringir o número máximo de processadores disponíveis para a verificação do DBCC, use [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md). Para obter mais informações, veja [Configurar a opção max degree of parallelism de configuração de servidor](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).
A verificação paralela pode ser desabilitada usando o sinalizador de rastreamento 2528. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).
    
> [!NOTE]    
> Durante uma operação de DBCC CHECKTABLE, os bytes armazenados em uma coluna de tipo definido pelo usuário, ordenada por byte, devem ser iguais aos da serialização computada do valor do tipo definido pelo usuário. Se isto não for verdadeiro, a rotina de DBCC CHECKTABLE relatará um erro de consistência.    
    
## <a name="understanding-dbcc-error-messages"></a>Compreendendo mensagens de erro DBCC    
Depois que o comando DBCC CHECKTABLE é concluído, uma mensagem é gravada no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o comando DBCC for executado com êxito, a mensagem indicará uma conclusão bem-sucedida e o tempo de execução do comando. Se o comando DBCC parar antes de concluir a verificação devido a um erro, a mensagem indicará que o comando foi finalizado, um valor de estado e a duração da execução do comando. A tabela a seguir lista e descreve os valores de estado que podem ser incluídos na mensagem.
    
|Estado|Descrição|    
|-----------|-----------------|    
|0|O número do erro 8930 foi gerado. Isso indica um dano de metadados que provocou a finalização do comando DBCC.|    
|1|O erro número 8967 foi gerado. Ocorreu um erro interno de DBCC.|    
|2|Ocorreu uma falha durante o reparo do banco de dados em modo de emergência.|    
|3|Isso indica um dano de metadados que provocou a finalização do comando DBCC.|    
|4|Uma declaração ou violação de acesso foi detectada.|    
|5|Ocorreu um erro desconhecido que finalizou o comando DBCC.|    
    
## <a name="error-reporting"></a>Relatório de Erros    
Um arquivo de minidespejo (`SQLDUMP*nnnn*.txt`) é criado no diretório de LOG [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sempre que DBCC CHECKTABLE detecta um erro de currupção. Quando a coleta de dados *Uso de Recursos* e os recursos de *Relatório de Erros* recursos estão habilitados para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o arquivo é encaminhado automaticamente ao [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Os dados coletados são usados para aprimorar a funcionalidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
O arquivo de despejo contém os resultados do comando DBCC CHECKTABLE e saídas de diagnóstico adicionais. O arquivo tem DACLs (listas de controle de acesso discricionário) restritas. O acesso é limitado à conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aos membros da função sysadmin. Por padrão, a função sysadmin contém todos os membros do grupo BUILTIN\Administradores do Windows e do grupo do administrador local. O comando DBCC não falhará se o processo de coleta de dados falhar.
    
## <a name="resolving-errors"></a>Resolvendo erros    
 Se qualquer erro for relatado pelo DBCC CHECKTABLE, recomendamos a restauração do banco de dados do backup em vez da execução de REPAIR com uma das opções REPAIR. Se não existir nenhum backup, a execução de REPARAR poderá corrigir os erros relatados. A opção REPAIR a ser usada é especificada no fim da lista de erros relatados. No entanto, a correção dos erros usando a opção REPAIR_ALLOW_DATA_LOSS pode exigir que algumas páginas e, portanto, dados, sejam excluídos.    
O reparo pode ser executado sob uma transação do usuário para permitir que o usuário reverta as alterações feitas. Se reparos forem revertidos, o banco de dados ainda conterá erros e deverá ser restaurado de um backup. Depois de concluir todos os reparos, faça backup do banco de dados.
    
## <a name="result-sets"></a>Conjuntos de resultados    
O DBCC CHECKTABLE retorna o seguinte conjunto de resultados. O mesmo conjunto de resultados será retornado se você especificar apenas o nome da tabela ou qualquer uma das opções.
    
```
DBCC results for 'HumanResources.Employee'.    
There are 288 rows in 13 pages for object 'Employee'.    
DBCC execution completed. If DBCC printed error messages, contact your system administrator.    
```    
    
O DBCC CHECKTABLE retornará o conjunto de resultados a seguir se a opção de ESTIMATEONLY for especificada:
    
```
Estimated TEMPDB space needed for CHECKTABLES (KB)     
--------------------------------------------------     
21    
(1 row(s) affected)    
DBCC execution completed. If DBCC printed error messages, contact your system administrator.    
```    
    
## <a name="permissions"></a>Permissões    
O usuário precisa ser o proprietário da tabela ou ser membro da função de servidor fixa sysadmin, da função de banco de dados fixa db_owner ou da função de banco de dados fixa db_ddladmin.    
    
## <a name="examples"></a>Exemplos    
    
### <a name="a-checking-a-specific-table"></a>a. Verificando uma tabela específica    
O exemplo a seguir verifica a integridade da página de dados da tabela `HumanResources.Employee` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].
    
```sql    
DBCC CHECKTABLE ('HumanResources.Employee');    
GO    
```    
    
### <a name="b-performing-a-low-overhead-check-of-the-table"></a>B. Executando uma verificação de sobrecarga baixa da tabela    
 O exemplo a seguir executa uma verificação de sobrecarga baixa da tabela `Employee` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].    
    
```sql    
DBCC CHECKTABLE ('HumanResources.Employee') WITH PHYSICAL_ONLY;    
GO    
```    
    
### <a name="c-checking-a-specific-index"></a>C. Verificando um índice específico    
 O exemplo a seguir verifica um índice específico obtido por meio de acesso a `sys.indexes`.    
    
```sql    
DECLARE @indid int;    
SET @indid = (SELECT index_id     
              FROM sys.indexes    
              WHERE object_id = OBJECT_ID('Production.Product')    
                    AND name = 'AK_Product_Name');    
DBCC CHECKTABLE ('Production.Product',@indid);    
```    
    
## <a name="see-also"></a>Consulte Também    
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)     
[DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)    
    
  
