---
title: Always Encrypted com enclaves seguros
description: Saiba mais sobre o Always Encrypted com o recurso de enclaves seguros do SQL Server.
ms.custom: seo-lt-2019
ms.date: 01/15/2021
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: ed6a0a041cba407b06b26e8b1d800da1f47b2bbb
ms.sourcegitcommit: 8ca4b1398e090337ded64840bcb8d6c92d65c29e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2021
ms.locfileid: "98534665"
---
# <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted com enclaves seguros

[!INCLUDE [sqlserver2019-windows-only-asdb](../../../includes/applies-to-version/sqlserver2019-windows-only-asdb.md)]

O Always Encrypted com enclaves seguros expande as funcionalidades de computação confidencial do [Always Encrypted](always-encrypted-database-engine.md) habilitando a criptografia in-loco e as consultas confidenciais mais avançadas. O Always Encrypted com enclaves seguros está disponível no [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] e no [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] (em versão prévia).

Introduzido no [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] em 2015 e no [!INCLUDE[sssql16](../../../includes/sssql16-md.md)], o Always Encrypted protege a confidencialidade dos dados confidenciais contra malware e usuários *não autorizados* com altos privilégios: DBAs, administradores de computadores, administradores de nuvem ou qualquer outra pessoa que tenha acesso legítimo a instâncias do servidor, hardware etc., mas não deveria ter acesso a uma parte ou todos os dados reais.  

Sem os aprimoramentos discutidos neste artigo, o Always Encrypted protege os dados criptografando-os no lado do cliente e *nunca* permitindo que os dados ou as chaves de criptografia correspondentes sejam exibidos em texto não criptografado dentro do [!INCLUDE[ssde-md](../../../includes/ssde-md.md)]. Como resultado, a funcionalidade em colunas criptografadas dentro do banco de dados fica muito restrita. As únicas operações que o [!INCLUDE[ssde-md](../../../includes/ssde-md.md)] pode executar em dados criptografados são comparações de igualdade (disponíveis somente com a [criptografia determinística](always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)). Não há suporte para todas as outras operações, incluindo operações de criptografia (criptografia de dados inicial ou rotação de chave) e consultas mais avançadas (por exemplo, correspondência de padrões) no banco de dados. Os usuários precisam mover os dados para fora do banco de dados para executar essas operações no lado do cliente.

O Always Encrypted *com enclaves seguros* soluciona essas limitações, permitindo algumas computações em dados de texto não criptografado em um enclave seguro no lado do servidor. Um enclave seguro é uma região protegida da memória dentro do processo do [!INCLUDE[ssde-md](../../../includes/ssde-md.md)]. O enclave seguro é exibido como uma caixa opaca para o restante do [!INCLUDE[ssde-md](../../../includes/ssde-md.md)] e os outros processos no computador de hospedagem. Não há nenhuma maneira de exibir os dados ou o código dentro do enclave de fora, mesmo com um depurador. Essas propriedades tornam o enclave seguro um *ambiente de execução confiável* que pode acessar com segurança chaves de criptografia e dados confidenciais em texto não criptografado, sem comprometer a confidencialidade dos dados.

O Always Encrypted usa enclaves seguros, conforme ilustrado no diagrama a seguir:

![fluxo de dados](./media/always-encrypted-enclaves/ae-data-flow.png)

Ao analisar uma instrução Transact-SQL enviada por um aplicativo, o [!INCLUDE[ssde-md](../../../includes/ssde-md.md)] determina se a instrução contém qualquer operação em dados criptografados que exigem o uso do enclave seguro. Para essas instruções:

- O driver de cliente envia as chaves de criptografia de coluna necessárias para as operações ao enclave seguro (por um canal seguro) e envia a instrução para execução.

- Ao processar a instrução, o [!INCLUDE[ssde-md](../../../includes/ssde-md.md)] delega operações de criptografia ou computações em colunas criptografadas ao enclave seguro. Se necessário, o enclave descriptografa os dados e executa computações em texto não criptografado.

Durante o processamento da instrução, as chaves de criptografia de coluna e os dados não são expostos em texto não criptografado no [!INCLUDE[ssde-md](../../../includes/ssde-md.md)] fora do enclave seguro.

## <a name="supported-enclave-technologies"></a>Tecnologias de enclave compatíveis

Em [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)], o Always Encrypted com enclaves seguros usa enclaves de memória seguros com [VBS (Segurança baseada em Virtualização)](https://www.microsoft.com/security/blog/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/) (também conhecido como enclaves VSM ou Modo Seguro Virtual) no Windows.

No [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)], o Always Encrypted com enclaves seguros usa os enclaves do [Intel SGX (Intel Software Guard Extensions)](https://itpeernetwork.intel.com/microsoft-azure-confidential-computing/). O Intel SGX é uma tecnologia de ambiente de execução confiável baseada em hardware compatível com bancos de dados que usam a configuração de hardware da [série DC](https://docs.microsoft.com/azure/azure-sql/database/service-tiers-vcore?tabs=azure-portal#dc-series).

## <a name="secure-enclave-attestation"></a>Atestado de enclave seguro

O enclave seguro dentro do [!INCLUDE[ssde-md](../../../includes/ssde-md.md)] pode acessar dados confidenciais e as chaves de criptografia de coluna em texto não criptografado. Portanto, antes do envio de uma instrução que envolva computações de enclave para o [!INCLUDE[ssde-md](../../../includes/ssde-md.md)], o driver de cliente dentro do aplicativo precisa verificar se o enclave seguro é um enclave VBS ou SGX original, e o código em execução no enclave seguro é a biblioteca original do Always Encrypted que implementa algoritmos de criptografia do Always Encrypted para criptografia in-loco e operações compatíveis em consultas confidenciais.

O processo de verificação do enclave é chamado de **atestado de enclave** e exige que um driver de cliente dentro do aplicativo e o [!INCLUDE[ssde-md](../../../includes/ssde-md.md)] entrem em contato com um serviço de atestado externo. As especificidades do processo de atestado dependem do tipo do enclave (VBS ou SGX) e do serviço de atestado.

O processo de atestado para enclaves seguros VBS no [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] é o [atestado de runtime do Windows Defender System Guard](https://www.microsoft.com/security/blog/2018/06/05/virtualization-based-security-vbs-memory-enclaves-data-protection-through-isolation/), que exige o HGS (Serviço Guardião de Host) como um serviço de atestado. 

O atestado de enclaves Intel SGX no [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] exige o [Atestado do Microsoft Azure](https://docs.microsoft.com/azure/attestation/overview).

> [!NOTE]
> O [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] não dá suporte ao Atestado do Microsoft Azure. O Serviço Guardião de Host é a única solução de atestado compatível com enclaves VBS no [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)].

## <a name="supported-client-drivers"></a>Drivers de cliente compatíveis

Para usar o Always Encrypted com enclaves seguros, um aplicativo precisa usar um driver de cliente compatível com esse recurso. Configure o aplicativo e o driver de cliente para habilitar computações de enclave e o atestado de enclave. Para obter detalhes, incluindo a lista de drivers de cliente compatíveis, confira [Desenvolver aplicativos usando o Always Encrypted](always-encrypted-client-development.md).

## <a name="terminology"></a>Terminologia

### <a name="enclave-enabled-keys"></a>Chaves habilitadas para enclave

O Always Encrypted com enclaves seguros apresenta o conceito de chaves habilitadas para enclave:

- **Chave mestra de coluna habilitada para enclave**: uma chave mestra de coluna que tem a propriedade `ENCLAVE_COMPUTATIONS` especificada no objeto de metadados da chave mestra de coluna no banco de dados. O objeto de metadados de chave mestra de coluna também precisa conter uma assinatura válida das propriedades de metadados. Para obter mais informações, confira [CREATE COLUMN MASTER KEY (Transact-SQL)](../../../t-sql/statements/create-column-master-key-transact-sql.md)
- **Chave de criptografia de coluna habilitada para enclave** – uma chave de criptografia de coluna que é criptografada com uma chave mestra de coluna habilitada para enclave. Somente as chaves de criptografia de coluna habilitadas para enclave podem ser usadas para computações dentro do enclave seguro. 

Para obter mais informações, confira [Gerenciar chaves para Always Encrypted com enclaves seguros](always-encrypted-enclaves-manage-keys.md).

### <a name="enclave-enabled-columns"></a>Colunas habilitadas para enclave

Uma coluna habilitada para enclave é uma coluna de banco de dados criptografada com uma chave de criptografia de coluna habilitada para enclave.

## <a name="confidential-computing-capabilities-for-enclave-enabled-columns"></a>Funcionalidades de computação confidencial para colunas habilitadas para enclave

Os dois principais benefícios do Always Encrypted com enclaves seguros são a criptografia in-loco e as consultas confidenciais avançadas.

### <a name="in-place-encryption"></a>Criptografia no local

A criptografia in-loco permite operações de criptografia em colunas de banco de dados dentro do enclave seguro, sem mover os dados para fora do banco de dados. Ela aprimora o desempenho e a confiabilidade da criptografia. Execute a criptografia in-loco usando a instrução [ALTER TABLE (Transact-SQL)](../../../t-sql/statements/alter-table-transact-sql.md). 

As operações de criptografia compatíveis in-loco são:

- Criptografia de uma coluna de texto não criptografado com uma chave de criptografia de coluna habilitada para enclave.
- Nova criptografia de uma coluna criptografada habilitada para enclave para:
  - Girar uma chave de criptografia de coluna: criptografar novamente a coluna com uma nova chave de criptografia de coluna habilitada para enclave.
  - Alterar o tipo de criptografia de uma coluna habilitada para enclave, por exemplo, de determinística para aleatória.
- Descriptografar dados armazenados em uma coluna habilitada para enclave (converter a coluna em uma coluna de texto não criptografado).

A criptografia in-loco é permitida com a criptografia determinística e aleatória, desde que as chaves de criptografia de coluna envolvidas em uma operação de criptografia sejam habilitadas para enclave.

### <a name="confidential-queries"></a>Consultas confidenciais

Consultas confidenciais são [consultas DML](../../../t-sql/queries/queries.md) que envolvem operações em colunas habilitadas para enclave executadas dentro do enclave seguro.

As operações compatíveis com os enclaves seguros são:

| Operação| [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] | [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] |
|:---|:---|:---|
| [Operadores de comparação](../../../mdx/comparison-operators.md) | Com suporte | Com suporte |
| [BETWEEN (Transact-SQL)](../../../t-sql/language-elements/between-transact-sql.md) | Com suporte | Com suporte |
| [IN (Transact-SQL)](../../../t-sql/language-elements/in-transact-sql.md) | Com suporte | Com suporte |
| [LIKE (Transact-SQL)](../../../t-sql/language-elements/like-transact-sql.md) | Com suporte | Com suporte |
| [DISTINCT](../../../t-sql/queries/select-transact-sql.md#c-using-distinct-with-select) | Com suporte | Com suporte |
| [Junções](../../performance/joins.md) | Só há suporte para junções de loop aninhadas | Com suporte |
| [SELECT – Cláusula ORDER BY (Transact-SQL)](../../../t-sql/queries/select-order-by-clause-transact-sql.md) | Sem suporte | Com suporte |
| [SELECT – GROUP BY – Transact-SQL](../../../t-sql/queries/select-group-by-transact-sql.md) | Sem suporte | Com suporte |

> [!NOTE]
> Só há suporte para as operações acima nos enclaves seguros em colunas habilitadas para enclave com a criptografia **aleatória**, não com a criptografia determinística. A comparação de igualdade permanece a única computação compatível em colunas que usam a criptografia determinística e é executada comparando o texto cifrado fora do enclave, independentemente de a coluna estar habilitada para enclave. A criptografia determinística dá suporte às seguintes operações que envolvem comparações de igualdade: 
> - [= (Equals)](../../../t-sql/language-elements/equals-transact-sql.md) em pesquisa de ponto, pesquisas e junções
> - [IN](../../../t-sql/language-elements/in-transact-sql.md)
> - [SELECT – GROUP BY](../../../t-sql/queries/select-group-by-transact-sql.md)
> - [DISTINCT](../../../t-sql/queries/select-transact-sql.md#c-using-distinct-with-select)
>
> No [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)], as consultas confidenciais que usam enclaves em uma coluna de cadeia de caracteres (`char`, `nchar`) exigem que a coluna use uma ordenação com ordem de classificação binary2 (BIN2). No [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)], as consultas confidenciais em cadeias de caracteres exigem uma ordenação BIN2 ou UTF-8. 

### <a name="indexes-on-enclave-enabled-columns"></a>Índices em colunas habilitadas para enclave

Você pode criar índices não clusterizados em colunas habilitadas para enclave que usam a criptografia aleatória para fazer consultas DML confidenciais com o enclave seguro executado mais rapidamente.

Para garantir que não haja vazamento de dados confidenciais de um índice em uma coluna criptografada que usa a criptografia aleatória, os valores de chave na estrutura de dados do índice (árvore B) são criptografados e classificados com base nos respectivos valores de texto não criptografado. A classificação pelo valor de texto não criptografado também é útil para o processamento de consultas dentro do enclave. Quando o executor de consultas no [!INCLUDE[ssde-md](../../../includes/ssde-md.md)] usa um índice em uma coluna criptografada para computações dentro do enclave, ele pesquisa o índice para procurar valores específicos armazenados na coluna. Cada pesquisa pode envolver várias comparações. O executor de consultas delega cada comparação ao enclave que descriptografa um valor armazenado na coluna e o valor da chave criptografada do índice a ser comparado, realiza a comparação em texto não criptografado e retorna o resultado da comparação ao executor.

Ainda não há suporte para criação de índices em colunas que usam criptografia aleatória e que não são habilitadas para enclave.

Um índice em uma coluna que usa a criptografia determinística é classificado com base no texto cifrado (não no texto não criptografado), independentemente de a coluna estar habilitada para enclave.

Para obter mais informações, confira [Criar e usar índices em colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-create-use-indexes.md). Para obter informações gerais sobre como funciona a indexação do [!INCLUDE[ssde-md](../../../includes/ssde-md.md)], confira o artigo [Descrição de índices clusterizados e não clusterizados](../../indexes/clustered-and-nonclustered-indexes-described.md).

### <a name="database-recovery"></a>Recuperação de banco de dados

Quando uma instância do SQL Server falha, os respectivos bancos de dados podem ficar em um estado em que os arquivos de dados podem conter algumas modificações de transações incompletas. Quando a instância é iniciada, ela executa um processo chamado [recuperação de banco de dados](../../logs/the-transaction-log-sql-server.md#recovery-of-all-incomplete-transactions-when--is-started), que envolve a reversão de todas as transações incompletas encontradas no log de transações para garantir que a integridade do banco de dados seja preservada. Caso uma transação incompleta tenha feito alterações em um índice, essas alterações também precisam ser desfeitas. Por exemplo, talvez seja necessário remover ou reinserir alguns valores de chave no índice.

> [!IMPORTANT]
> A Microsoft recomenda habilitar a [ADR (Recuperação de Banco de dados Acelerada)](../../backup-restore/restore-and-recovery-overview-sql-server.md#adr) no banco de dados, **antes** de criar o primeiro índice em uma coluna habilitada para enclave com criptografia aleatória. A ADR está habilitada por padrão no [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)], mas não no [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)].

Para desfazer uma alteração feita em um índice com o [processo de recuperação de banco de dados tradicional](/azure/sql-database/sql-database-accelerated-database-recovery#the-current-database-recovery-process) (que segue o modelo de recuperação [ARIES](https://people.eecs.berkeley.edu/~brewer/cs262/Aries.pdf)), o SQL Server precisa aguardar até que um aplicativo forneça a chave de criptografia da coluna para o enclave, o que pode levar muito tempo. A ADR (Recuperação Acelerada de Banco de Dados) reduz significativamente a quantidade de operações de desfazer que precisam ser adiadas devido a uma chave de criptografia de coluna não estar disponível no cache dentro do enclave. Consequentemente, esse recurso aumenta consideravelmente a disponibilidade do banco de dados, reduzindo a chance de uma nova transação ser bloqueada. Com a ADR habilitada, o SQL Server ainda pode precisar de uma chave de criptografia de coluna para concluir a limpeza de versões de dados anteriores, mas ele realiza esse processo como uma tarefa em segundo plano que não afeta a disponibilidade do banco de dados ou as transações do usuário. No entanto, talvez você receba mensagens de erro no log de erros, indicando falhas nas operações de limpeza devido à ausência de uma chave de criptografia da coluna.

## <a name="security-considerations"></a>Considerações de segurança

As considerações a seguir sobre segurança se aplicam ao Always Encrypted com enclaves seguros.

- A segurança dos dados dentro do enclave depende de um protocolo e serviço de atestado. Portanto, é necessário garantir que o serviço e as políticas de atestado, bem como a aplicação do serviço de atestado, sejam gerenciados por um administrador confiável. Além disso, os serviços de atestado normalmente têm suporte para diversas políticas e protocolos de atestado, alguns dos quais realizam uma verificação mínima do enclave e do respectivo ambiente, e são projetados para fins de testes e desenvolvimento. Siga rigorosamente as diretrizes específicas do serviço de atestado para garantir que você esteja usando as configurações e políticas recomendadas para suas implantações de produção. 
- Criptografar uma coluna que usa a criptografia aleatória com uma chave de criptografia de coluna habilitada para enclave pode resultar no vazamento da ordem dos dados armazenados na coluna, pois essas colunas dão suporte a comparações de intervalos. Por exemplo, se uma coluna criptografada contendo salários de funcionários tiver um índice, um administrador de banco de dados mal-intencionado poderá verificar o índice para encontrar o maior valor de salário criptografado e identificar uma pessoa que recebe esse salário (supondo que o nome dela não esteja criptografado). 
- Se usar o Always Encrypted para proteger dados confidenciais contra o acesso não autorizado por administradores de bancos de dados, não compartilhe as chaves mestras da coluna ou as chaves de criptografia da coluna com os administradores de bancos de dados. Um administrador de banco de dados pode gerenciar índices em colunas criptografadas sem ter acesso direto às chaves, aproveitando o cache de chaves de criptografia da coluna dentro do enclave.

## <a name="considerations-for-business-continuity-disaster-recovery-and-data-migration"></a><a name="anchorname-1-considerations-availability-groups-db-migration"></a> Considerações sobre continuidade dos negócios, recuperação de desastre e migração de dados

Ao configurar uma solução de alta disponibilidade ou de recuperação de desastre para um banco de dados usando o Always Encrypted com enclaves seguros, verifique se todas as réplicas de banco de dados podem usar um enclave seguro. Se um enclave estiver disponível para a réplica primária, mas não para a réplica secundária, qualquer instrução que tentar usar a funcionalidade do Always Encrypted com enclaves seguros falhará após o failover.

Ao copiar ou migrar um banco de dados usando o Always Encrypted com enclaves seguros, verifique se o ambiente de destino sempre dá suporte a enclaves. Caso contrário, as instruções que usam enclaves não funcionarão no banco de dados migrado ou de cópia.

Estas são as considerações específicas que você deve ter em mente:

- **SQL Server**
  - Ao configurar um [grupo de disponibilidade do Always On](../../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md), verifique se todas as instâncias do SQL Server que hospedam um banco de dados no grupo de disponibilidade dão suporte ao Always Encrypted com enclaves seguros e têm um enclave e um atestado configurados.
  - Quando você restaurar um arquivo de backup de um banco de dados que usa a funcionalidade do Always Encrypted com enclaves seguros em uma instância do SQL Server que não tem o enclave configurado, a operação de restauração será bem-sucedida e todas as funcionalidades que não dependem do enclave ficarão disponíveis. No entanto, todas as instruções seguintes que usarem a funcionalidade de enclave falharão, e os índices nas colunas habilitadas para enclave que usam a criptografia aleatória ficarão inválidos. O mesmo se aplica quando você anexa um banco de dados usando o Always Encrypted com enclaves seguros na instância que não têm o enclave configurado.
  - Caso seu banco de dados contenha índices em colunas habilitadas para enclave que usam a criptografia aleatória, habilite a [ADR (Recuperação Acelerada de Banco de Dados)](../../backup-restore/restore-and-recovery-overview-sql-server.md#adr) no banco de dados antes de criar um backup de banco de dados. A ADR garantirá que o banco de dados, inclusive os índices, fique disponível imediatamente após a restauração. Para saber mais, confira [Recuperação de banco de dados](#database-recovery).
  
- **Banco de Dados SQL do Azure**
  - Ao configurar a [replicação geográfica ativa](https://docs.microsoft.com/azure/azure-sql/database/active-geo-replication-overview), verifique se um banco de dados secundário dá suporte a enclaves seguros, caso o banco de dados primário dê suporte a eles.

No SQL Server e no Banco de Dados SQL do Azure, ao migrar seu banco de dados usando um arquivo BACPAC, remova todos os índices de colunas habilitadas para enclave que usam a criptografia aleatória antes de criar o arquivo BACPAC.

## <a name="known-limitations"></a>Limitações conhecidas

O Always Encrypted com enclaves seguros soluciona algumas limitações do Always Encrypted dando suporte à criptografia in-loco e a consultas confidenciais mais avançadas com índices, conforme explicado em [Funcionalidades de computação confidencial para colunas habilitadas para enclave](#confidential-computing-capabilities-for-enclave-enabled-columns).

Todas as outras limitações do Always Encrypted listadas em [Detalhes do recurso](always-encrypted-database-engine.md#feature-details) também se aplicam ao Always Encrypted com enclaves seguros.

As seguintes limitações são específicas do Always Encrypted com enclaves seguros:

- Não é possível criar índices clusterizados em colunas habilitadas para enclave com criptografia aleatória.
- Colunas habilitadas para enclave com criptografia aleatória não podem ser colunas de chave primária e não podem ser referenciadas por restrições de chaves estrangeiras nem por restrições de chaves exclusivas.
- No [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)], (esta limitação não se aplica ao [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]), só há suporte para junções de loop aninhadas (com índices, se disponíveis) em colunas habilitadas para enclave que usam a criptografia aleatória. Para obter informações sobre outras diferenças entre produtos, confira [Consultas confidenciais](#confidential-queries).
- Operações criptográficas in-loco não podem ser combinadas com outras alterações de metadados de coluna, exceto as alterações de ordenação, na mesma página de código e nulidade. Por exemplo, não é possível criptografar, recriptografar ou descriptografar uma coluna E alterar um tipo de dados da coluna em uma única instrução `ALTER TABLE`/`ALTER COLUMN` do Transact-SQL. É necessário usar duas instruções separadas.
- Não há suporte para o uso de chaves habilitadas para enclave para colunas em tabelas na memória.
- As expressões que definem colunas computadas não podem executar computações em colunas habilitadas para enclave que usam a criptografia aleatória (mesmo que as computações estejam entre as operações compatíveis listadas em [Consultas confidenciais](#confidential-queries)).
- Não há suporte para caracteres de escape em parâmetros do operador LIKE em colunas habilitadas para enclave usando criptografia aleatória.
- Consultas com o operador LIKE ou um operador de comparação que inclui um parâmetro de consulta com um dos seguintes tipos de dados (que se tornam objetos grandes após a criptografia) ignoram índices e executam verificações de tabela.
  - `nchar[n]` e `nvarchar[n]`, se n for maior que 3967.
  - `char[n]`, `varchar[n]`, `binary[n]`, `varbinary[n]`, se n for maior que 7935.
- Limitações de ferramentas:
  - Os únicos repositórios de chaves compatíveis com o armazenamento de chaves mestras de coluna habilitadas para enclave são o Repositório de Certificados do Windows e o Azure Key Vault.
  - Não há suporte para importar/exportar bancos de dados que contêm chaves habilitadas para enclave.
  - Para disparar uma operação criptográfica in-loco por meio de uma instrução `ALTER TABLE`/`ALTER COLUMN` do Transact-SQL, é necessário emitir a instrução usando uma janela de consulta no SSMS ou então, você pode escrever seu próprio programa que emite a instrução. No momento, o cmdlet Set-SqlColumnEncryption no módulo SqlServer PowerShell e o assistente de Always Encrypted no SQL Server Management Studio ainda não são compatíveis com a criptografia in-loco – eles movem os dados para fora do banco de dados para operações criptográficas, mesmo se as chaves de criptografia de coluna usadas para as operações estão habilitadas para enclave.

## <a name="next-steps"></a>Próximas etapas

- [Tutorial: Introdução ao Always Encrypted com enclaves seguros no SQL Server](../tutorial-getting-started-with-always-encrypted-enclaves.md)
- [Tutorial: Introdução ao Always Encrypted com enclaves seguros no Banco de Dados SQL do Azure](/azure/azure-sql/database/always-encrypted-enclaves-getting-started)
- [Configurar e usar o Always Encrypted com enclaves seguros](configure-always-encrypted-enclaves.md)

## <a name="see-also"></a>Confira também

- [Gerenciar chaves para Always Encrypted com enclaves seguros](always-encrypted-enclaves-manage-keys.md)