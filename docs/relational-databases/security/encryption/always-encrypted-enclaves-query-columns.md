---
title: Executar instruções Transact-SQL usando os enclaves seguros
description: Executar instruções DDL (linguagem de definição de dados) para configurar a criptografia para a coluna ou gerenciar índices em colunas criptografadas e consultar colunas criptografadas
ms.custom: ''
ms.date: 01/15/2021
ms.reviewer: vanto
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: conceptual
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 8aecf4b22cf02ae91d259f45daff1d2cd8414f97
ms.sourcegitcommit: 8ca4b1398e090337ded64840bcb8d6c92d65c29e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2021
ms.locfileid: "98534685"
---
# <a name="run-transact-sql-statements-using-secure-enclaves"></a>Executar instruções Transact-SQL usando os enclaves seguros

[!INCLUDE [sqlserver2019-windows-only-asdb](../../../includes/applies-to-version/sqlserver2019-windows-only-asdb.md)]

O [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md) permite que algumas instruções T-SQL (Transact-SQL) executem computações confidenciais em colunas de banco de dados criptografadas em um enclave seguro no lado do servidor.

## <a name="statements-using-secure-enclaves"></a>Instruções com enclaves seguros

Os tipos de instrução T-SQL a seguir utilizam enclaves seguros.

### <a name="ddl-statements-using-secure-enclaves"></a>Instruções DDL com enclaves seguros

Os tipos de instruções [DDL (linguagem de definição de dados)](../../../t-sql/statements/statements.md#data-definition-language) a seguir exigem enclaves seguros.

- Instruções [ALTER TABLE column_definition (Transact-SQL)](../../../t-sql/statements/alter-table-column-definition-transact-sql.md) que disparam operações de criptografia in-loco usando chaves habilitadas para enclave. Para obter mais informações, confira [Configurar a criptografia de coluna in-loco usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-configure-encryption.md).
- Instruções [CREATE INDEX (Transact-SQL)](../../../t-sql/statements/create-index-transact-sql.md) e [ALTER INDEX (Transact-SQL)](../../../t-sql/statements/alter-index-transact-sql.md) que criam ou alteram índices em colunas habilitadas para enclave que usam a criptografia aleatória. Para obter mais informações, confira [Criar e usar índices em colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-create-use-indexes.md).
  
### <a name="dml-statements-using-secure-enclaves"></a>Instruções DML com enclaves seguros

As seguintes instruções ou consultas [DML (linguagem de manipulação de dados)](../../../t-sql/statements/statements.md#data-manipulation-language) em colunas habilitadas para enclave que usam a criptografia aleatória exigem enclaves seguros:

- Consultas que usam um ou mais dos seguintes operadores Transact-SQL compatíveis em enclaves seguros:
  - [Operadores de comparação](../../../mdx/comparison-operators.md)
  - [BETWEEN (Transact-SQL)](../../../t-sql/language-elements/between-transact-sql.md)
  - [IN (Transact-SQL)](../../../t-sql/language-elements/in-transact-sql.md)
  - [LIKE (Transact-SQL)](../../../t-sql/language-elements/like-transact-sql.md)
  - [DISTINCT](../../../t-sql/queries/select-transact-sql.md#c-using-distinct-with-select)
  - As [junções](../../performance/joins.md) - [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)] só dão suporte a junções de loop aninhadas. O [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] dá suporte a junções de loop, hash e mesclagem aninhadas
  - [SELECT – Cláusula ORDER BY (Transact-SQL)](../../../t-sql/queries/select-order-by-clause-transact-sql.md). Compatível com o [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]. Não compatível com o [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)]
  - [SELECT – Cláusula GROUP BY (Transact-SQL)](../../../t-sql/queries/select-group-by-transact-sql.md). Compatível com o [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)]. Não compatível com o [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)]
- Consultas que inserem, atualizam ou excluem linhas que, por sua vez, disparam a inserção e/ou a remoção de uma chave de índice em/de um índice em uma coluna habilitada para enclave. Para obter mais informações, confira [Criar e usar índices em colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-create-use-indexes.md).

> [!NOTE]
> Só há suporte para operações em índices e consultas DML confidenciais com enclaves em colunas habilitadas para enclave que usam a criptografia aleatória. Não há suporte para a criptografia determinística.
>
> No [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)], as consultas confidenciais com enclaves em colunas de cadeias de caracteres (`char`, `nchar`) exigem uma ordenação com ordem de classificação binary2 (BIN2) configurada para a coluna. No [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)], é necessário usar ordenações BIN2 ou UTF-8.

### <a name="dbcc-commands-using-secure-enclaves"></a>Comandos DBCC com enclaves seguros

Os comandos administrativos [DBCC (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-transact-sql.md) que envolvem a verificação da integridade dos índices também poderão exigir enclaves seguros se o banco de dados contiver índices em colunas habilitadas para enclave que usam a criptografia aleatória. Por exemplo, [DBCC CHECKDB (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) e [DBCC CHECKTABLE (Transact-SQL)](../../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md).

## <a name="prerequisites-for-running-statements-using-secure-enclaves"></a>Pré-requisitos para executar instruções usando enclaves seguros

Seu ambiente precisa atender aos requisitos a seguir para dar suporte a instruções em execução que usam um enclave seguro.

- A instância do [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] ou o banco de dados e o servidor do [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] precisam ser configurados corretamente para dar suporte aos enclaves e ao atestado. Para obter mais informações, confira [Configurar o atestado e enclave seguro](configure-always-encrypted-enclaves.md#set-up-the-secure-enclave-and-attestation).
- Você precisará obter uma URL de atestado do ambiente do administrador de serviços de atestado.

  - Se você estiver usando o [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] e o HGS (Serviço Guardião de Host), confira [Determinar e compartilhar a URL de atestado do HGS](always-encrypted-enclaves-host-guardian-service-deploy.md#step-6-determine-and-share-the-hgs-attestation-url).
  - Se você estiver usando o [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] e o Atestado do Microsoft Azure, confira [Determinar a URL de atestado para a política de atestado](/azure-sql/database/always-encrypted-enclaves-configure-attestation#determine-the-attestation-url-for-your-attestation-policy).

- Se você estiver se conectando ao banco de dados usando seu aplicativo, ele precisará usar um driver de cliente que dê suporte ao Always Encrypted com enclaves seguros. O aplicativo precisa se conectar ao banco de dados com o Always Encrypted habilitado para a conexão de banco de dados e o protocolo e a URL de atestado configurados corretamente. Para obter informações detalhadas, confira [Desenvolver aplicativos usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-client-development.md).
- Se você estiver usando o SSMS (SQL Server Management Studio) ou o Azure SQL Data Studio, precisará habilitar o Always Encrypted e configurar o protocolo e a URL de atestado ao se conectar ao banco de dados. Confira as seções a seguir para obter detalhes.

> [!NOTE]
> A conexão com o banco de dados com o Always Encrypted e o atestado configurado não é necessária para as seguintes operações se você está usando chaves de criptografia de coluna armazenadas em cache: Consultas DDL que criam ou alteram índices, consultas DML que atualizam índices e comandos DBCC que verificam a integridade do índice. Para obter mais informações, confira [Invocar operações de indexação usando chaves de criptografia de coluna armazenadas em cache](always-encrypted-enclaves-create-use-indexes.md#invoke-indexing-operations-using-cached-column-encryption-keys).

### <a name="prerequisites-for-running-t-sql-statements-using-enclaves-in-ssms"></a>Pré-requisitos para executar instruções T-SQL usando enclaves no SSMS

Requisitos mínimos de versão do SQL Server Management Studio:

- SSMS 18.3 ao usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].
- SSMS 18.8 ao usar o [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].

Execute as instruções em uma janela de consulta que usa uma conexão que tenha o Always Encrypted e a URL de atestado correta configurada.

1. Na caixa de diálogo **Conectar ao servidor**, especifique o nome do servidor, selecione um método de autenticação e especifique suas credenciais.
2. Clique em **Opções >>** e selecione a guia **Always Encrypted**.
3. Marque a caixa de seleção **Habilitar o Always Encrypted (criptografia de coluna)** e especifique a URL de atestado de enclave. Por exemplo, `https://hgs.bastion.local/Attestation` ou `https://contososqlattestation.uks.attest.azure.net/attest/SgxEnclave`.

    ![Conectar-se ao servidor com o atestado usando o SSMS](./media/always-encrypted-enclaves/column-encryption-setting.png)

4. Selecione **Conectar**.
5. Se precisar habilitar a parametrização para consultas do Always Encrypted, selecione **Habilitar** caso planeje executar consultas DML parametrizadas. Para obter mais informações, confira [Parametrização do Always Encrypted](always-encrypted-query-columns-ssms.md#param).

Para obter mais informações, confira [Habilitar e desabilitar o Always Encrypted para uma conexão de banco de dados](always-encrypted-query-columns-ssms.md#en-dis).

### <a name="prerequisites-for-running-t-sql-statements-using-enclaves-in-azure-data-studio"></a>Pré-requisitos para executar instruções T-SQL usando enclaves no Azure Data Studio

A versão mínima **1.23** ou superior é recomendada.

Execute as instruções em uma janela de consulta que usa uma conexão que tenha o Always Encrypted habilitado e a URL e o protocolo de atestado corretos configurados.

1. Na caixa de diálogo **Conexão**, clique em **Avançado...** .
2. Para habilitar o Always Encrypted para a conexão, defina o campo **Always Encrypted** como **Habilitado**.
3. Especifique o protocolo e a URL de atestado.
    - Se você estiver usando o [!INCLUDE [sssqlv15-md](../../../includes/sssqlv15-md.md)], defina **Protocolo de Atestado** como **Serviço Guardião de Host** e insira a URL de atestado do Serviço Guardião de Host no campo **URL de Atestado de Enclave**.
    - Se estiver usando o [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)], defina **Protocolo de Atestado** como **Atestado do Azure** e insira a URL de atestado que referencia a política no Atestado do Microsoft Azure no campo **URL de Atestado de Enclave**.

    ![Conectar-se ao servidor com o atestado usando o Azure Data Studio](./media/always-encrypted-enclaves/azure-data-studio-connect-with-enclaves.png)

4. Clique em **OK** para fechar as **Propriedades avançadas**.

Para obter mais informações, confira [Habilitar e desabilitar o Always Encrypted para uma conexão de banco de dados](always-encrypted-query-columns-ads.md#enabling-and-disabling-always-encrypted-for-a-database-connection).

Se você planeja executar consultas DML parametrizadas, habilite também a [Parametrização do Always Encrypted](always-encrypted-query-columns-ads.md#parameterization-for-always-encrypted).

## <a name="examples"></a>Exemplos

Esta seção inclui exemplos de consultas DML que usam enclaves. 

Os exemplos usam o esquema abaixo.

```sql
CREATE SCHEMA [HR];
GO

CREATE TABLE [HR].[Jobs](
 [JobID] [int] IDENTITY(1,1) PRIMARY KEY,
 [JobTitle] [nvarchar](50) NOT NULL,
 [MinSalary] [money] ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
 [MaxSalary] [money] ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL
);
GO

CREATE TABLE [HR].[Employees](
 [EmployeeID] [int] IDENTITY(1,1) PRIMARY KEY,
 [SSN] [char](11) ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
 [FirstName] [nvarchar](50) NOT NULL,
 [LastName] [nvarchar](50) NOT NULL,
 [Salary] [money] ENCRYPTED WITH (COLUMN_ENCRYPTION_KEY = [CEK1], ENCRYPTION_TYPE = Randomized, ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NOT NULL,
 [JobID] [int] NULL,
 FOREIGN KEY (JobID) REFERENCES [HR].[Jobs] (JobID)
);
GO
```

### <a name="exact-match-search"></a>Pesquisa de correspondência exata

A consulta abaixo executa uma pesquisa de correspondência exata na coluna de cadeia de caracteres `SSN` criptografada.

```sql
DECLARE @SSN char(11) = '795-73-9838';
SELECT * FROM [HR].[Employees] WHERE [SSN] = @SSN;
GO
```

### <a name="pattern-matching-search"></a>Pesquisa de correspondência de padrões

A consulta abaixo executa uma pesquisa de correspondência de padrões na coluna de cadeia de caracteres `SSN` criptografada, pesquisando os funcionários com os últimos quatro dígitos especificados de um número do seguro social.

```sql
DECLARE @SSN char(11) = '795-73-9838';
SELECT * FROM [HR].[Employees] WHERE [SSN] = @SSN;
GO
```

### <a name="range-comparison"></a>Comparação de intervalos

A consulta abaixo executa uma comparação de intervalos na coluna `Salary` criptografada, pesquisando os funcionários com salários dentro do intervalo especificado.

```sql
DECLARE @MinSalary money = 40000;
DECLARE @MaxSalary money = 45000;
SELECT * FROM [HR].[Employees] WHERE [Salary] > @MinSalary AND [Salary] < @MaxSalary;
GO
```

### <a name="joins"></a>Junções

A consulta abaixo executa uma junção entre as tabelas `Employees` e `Jobs` usando a coluna `Salary` criptografada. A consulta recupera os funcionários com salários fora de um intervalo de salário para o trabalho do funcionário.

```sql
SELECT * FROM [HR].[Employees] e
JOIN [HR].[Jobs] j
ON e.[JobID] = j.[JobID] AND e.[Salary] > j.[MaxSalary] OR e.[Salary] < j.[MinSalary];
GO
```

### <a name="sorting"></a>Classificação

A consulta abaixo classifica os registros de funcionários com base na coluna `Salary` criptografada, recuperando os dez funcionários com os salários mais altos.
> [!NOTE]
> Há suporte para a classificação de colunas criptografadas no [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)], mas não no [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)].

```sql
SELECT TOP(10) * FROM [HR].[Employees]
ORDER BY [Salary] DESC;
GO
```

## <a name="next-steps"></a>Próximas etapas

- [Desenvolver aplicativos usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-client-development.md)

## <a name="see-also"></a>Confira também

- [Solução de problemas comuns do Always Encrypted com enclaves seguros](always-encrypted-enclaves-troubleshooting.md)
- [Tutorial: Introdução ao Always Encrypted com enclaves seguros no SQL Server](../tutorial-getting-started-with-always-encrypted-enclaves.md)
- [Tutorial: Introdução ao Always Encrypted com enclaves seguros no Banco de Dados SQL do Azure](/azure/azure-sql/database/always-encrypted-enclaves-getting-started)
- [Configurar a criptografia de coluna in-loco usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-configure-encryption.md)
- [Criar e usar índices em colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-create-use-indexes.md)