---
description: sp_refresh_parameter_encryption (Transact-SQL)
title: sp_refresh_parameter_encryption (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sp_refresh_parameter_encryption
- sp_refresh_parameter_encryption_TSQL
- sys.sp_refresh_parameter_encryption
- sys.sp_refresh_parameter_encryption_TSQL
helpviewer_keywords:
- sp_refresh_parameter_encryption
- Always Encrypted, sp_refresh_parameter_encryption
ms.assetid: 00b44baf-fcf0-4095-aabe-49fa87e77316
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 64ca46d46ac648fdebeb8c028df312472e4f5d58
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88645051"
---
# <a name="sp_refresh_parameter_encryption-transact-sql"></a>sp_refresh_parameter_encryption (Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

Atualiza os metadados de Always Encrypted para os parâmetros do procedimento armazenado não associado a esquema especificado, função definida pelo usuário, exibição, gatilho DML, gatilho DDL no nível de banco de dados ou gatilho DDL de nível de servidor no banco de dados atual. 

 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sys.sp_refresh_parameter_encryption [ @name = ] 'module_name' 
    [ , [ @namespace = ] '<class>' ]
[ ; ]

<class> ::=
{ DATABASE_DDL_TRIGGER | SERVER_DDL_TRIGGER }
```

## <a name="arguments"></a>Argumentos

`[ @name = ] 'module_name'` É o nome do procedimento armazenado, a função definida pelo usuário, a exibição, o gatilho DML, o gatilho DDL no nível do banco de dados ou o gatilho DDL no nível do servidor. *module_name* não pode ser um procedimento armazenado Common Language Runtime (CLR) ou uma função CLR. *module_name* não pode ser associado a esquema. *module_name* é `nvarchar` , sem padrão. *module_name* pode ser um identificador de várias partes, mas só pode fazer referência a objetos no banco de dados atual.

`[ @namespace = ] ' < class > '` É a classe do módulo especificado. Quando *module_name* é um gatilho DDL, `<class>` é necessário. `<class>` é `nvarchar(20)`. As entradas válidas são `DATABASE_DDL_TRIGGER` e `SERVER_DDL_TRIGGER` .    

## <a name="return-code-values"></a>Valores do código de retorno  

0 (êxito) ou um número diferente de zero (falha)


## <a name="remarks"></a>Comentários

Os metadados de criptografia para parâmetros de um módulo podem ficar desatualizados, se:   
* As propriedades de criptografia de uma coluna em uma tabela que o módulo referencia, foram atualizadas. Por exemplo, uma coluna foi descartada e uma nova coluna com o mesmo nome, mas um tipo de criptografia diferente, uma chave de criptografia ou um algoritmo de criptografia foi adicionado.  
* O módulo faz referência a outro módulo com metadados de criptografia de parâmetro desatualizados.  

Quando as propriedades de criptografia de uma tabela são modificadas, `sp_refresh_parameter_encryption` devem ser executadas para qualquer módulo que referencie diretamente ou indiretamente a tabela. Esse procedimento armazenado pode ser chamado nesses módulos em qualquer ordem, sem exigir que o usuário atualize primeiro o módulo interno antes de passar para seus chamadores.

`sp_refresh_parameter_encryption` não afeta nenhuma permissão, propriedades estendidas ou `SET` opções associadas ao objeto. 

Para atualizar um gatilho DDL de nível de servidor, execute este procedimento armazenado a partir do contexto de qualquer banco de dados.

> [!NOTE]
>  Todas as assinaturas associadas ao objeto são descartadas quando você executa o `sp_refresh_parameter_encryption` .

## <a name="permissions"></a>Permissões

Requer `ALTER` a permissão no módulo e a `REFERENCES` permissão em qualquer tipo CLR definido pelo usuário e em coleções de esquema XML que são referenciadas pelo objeto.   

Quando o módulo especificado é um gatilho DDL de nível de banco de dados, o requer `ALTER ANY DATABASE DDL TRIGGER` permissão no banco de dados atual.    

Quando o módulo especificado é um gatilho DDL de nível de servidor, o requer `CONTROL SERVER` permissão.

Para módulos que são definidos com a `EXECUTE AS` cláusula, a `IMPERSONATE` permissão é necessária na entidade de segurança especificada. Geralmente, a atualização de um objeto não altera sua `EXECUTE AS` entidade de segurança, a menos que o módulo tenha sido definido com `EXECUTE AS USER` e o nome de usuário da entidade de segurança agora seja resolvido para um usuário diferente do que fazia no momento em que o módulo foi criado.
 
## <a name="examples"></a>Exemplos

O exemplo a seguir cria uma tabela e um procedimento que referencia a tabela, configura Always Encrypted e, em seguida, demonstra a alteração da tabela e a execução do `sp_refresh_parameter_encryption` procedimento.  

Primeiro, crie a tabela inicial e um procedimento armazenado referenciando a tabela.
```sql
CREATE TABLE [Patients]([PatientID] [int] IDENTITY(1,1) NOT NULL,
    [SSN] [char](11), 
    [FirstName] [nvarchar](50) NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [MiddleName] [nvarchar](50) NULL,
    [StreetAddress] [nvarchar](50) NOT NULL,
    [City] [nvarchar](50) NOT NULL,
    [ZipCode] [char](5) NOT NULL,
    [State] [char](2) NOT NULL,
    [BirthDate] [date] NOT NULL,
 CONSTRAINT [PK_Patients] PRIMARY KEY CLUSTERED 
(
    [PatientID] ASC
) WITH 
    (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, 
     IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, 
     ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]) ON [PRIMARY];
GO

CREATE PROCEDURE [find_patient] @SSN [char](11)
AS
BEGIN
    SELECT * FROM [Patients] WHERE SSN=@SSN
END;
GO
```

Em seguida, configure as chaves de Always Encrypted.
```sql
CREATE COLUMN MASTER KEY [CMK1]
WITH
(
       KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',
    KEY_PATH = N'CurrentUser/my/A66BB0F6DD70BDFF02B62D0F87E340288E6F9305'
);
GO

CREATE COLUMN ENCRYPTION KEY [CEK1]
WITH VALUES
(
       COLUMN_MASTER_KEY = [CMK1],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 
       0x016E000001630075007200720065006E00740075007300650072002F006D0079002F006100360036006200620030006600360064006400370030006200640066006600300032006200360032006400300066003800370065003300340030003200380038006500360066003900330030003500CA0D0CEC74ECADD1804CF99137B4BD06BBAB15D7EA74E0C249A779C7768A5B659E0125D24FF827F5EA8CA517A8E197ECA1353BA814C2B0B2E6C8AB36E3AE6A1E972D69C3C573A963ADAB6686CF5D24F95FE43140C4F9AF48FBA7DF2D053F3B4A1F5693A1F905440F8015BDB43AF8A04BE4E045B89876A0097E5FBC4E6A3B9C3C0D278C540E46C53938B8C957B689C4DC095821C465C73117CBA95B758232F9E5B2FCC7950B8CA00AFE374DE42847E3FBC2FDD277035A2DEF529F4B735C20D980073B4965B4542A34723276A1646998FC6E1C40A3FDB6ABCA98EE2B447F114D2AC7FF8C7D51657550EC5C2BABFFE8429B851272086DCED94332CF18FA854C1D545A28B1EF4BE64F8E035175C1650F6FC5C4702ACF99850A4542B3747EAEC0CC726E091B36CE24392D801ECAA684DE344FECE05812D12CD72254A014D42D0EABDA41C89FC4F545E88B4B8781E5FAF40D7199D4842D2BFE904D209728ED4F527CBC169E2904F6E711FF81A8F4C25382A2E778DD2A58552ED031AFFDA9D9D891D98AD82155F93C58202FC24A77F415D4F8EF22419D62E188AC609330CCBD97CEE1AEF8A18B01958833604707FDF03B2B386487CC679D7E352D0B69F9FB002E51BCD814D077E82A09C14E9892C1F8E0C559CFD5FA841CEF647DAB03C8191DC46B772E94D579D8C80FE93C3827C9F0AE04D5325BC73111E07EEEDBE67F1E2A73580085
);
GO
```


Por fim, substituimos a coluna SSN pela coluna Encrypted e executamos o `sp_refresh_parameter_encryption` procedimento para atualizar os componentes de Always Encrypted.
```sql
ALTER TABLE [Patients] DROP COLUMN [SSN];
GO

ALTER TABLE [Patients] 
    ADD [SSN] [char](11) COLLATE Latin1_General_BIN2 
    ENCRYPTED WITH 
        (COLUMN_ENCRYPTION_KEY = [CEK1], 
        ENCRYPTION_TYPE = Deterministic, 
        ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') 
    NOT NULL;
GO

EXEC sp_refresh_parameter_encryption [find_patient];
GO
```

## <a name="see-also"></a>Consulte Também 

[Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
[Assistente do Always Encrypted](../../relational-databases/security/encryption/always-encrypted-wizard.md)   

