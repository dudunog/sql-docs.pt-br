---
title: Registrando tipos definidos pelo usuário no SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- UDTs [CLR integration], maintaining
- user-defined types [CLR integration], maintaining
- dependencies [CLR integration]
- deploying user-defined types [CLR integration]
- CurrencyConversion function
- user-defined types [CLR integration], deploying
- Transact-SQL deploying UDTs
- assemblies [CLR integration], user-defined types
- cross-database UDT support
- CREATE ASSEMBLY statement
- DROP TYPE statement
- Currency UDT
- CREATE TYPE statement
- registering user-defined types
- UDTs [CLR integration], deploying
- removing user-defined types
- user-defined types [CLR integration], registering
- ALTER ASSEMBLY statement
- UDTs [CLR integration], registering
- ADD FILE clause
ms.assetid: f7da3e92-e407-4f0b-b3a3-f214e442b37d
author: rothja
ms.author: jroth
ms.openlocfilehash: 7d24f7948e093335eff708f3c4a8a7361cfc156f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84954602"
---
# <a name="registering-user-defined-types-in-sql-server"></a>Registrando tipos definidos pelo usuário no SQL Server
  Para usar um UDT (tipo definido pelo usuário) no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você deve registrá-lo. O registro de um UDT envolve o registro do assembly e a criação do tipo no banco de dados em que deseja usá-lo. Os UDTs têm escopo em um único banco de dados e não podem ser usados em vários bancos de dados, a menos que o assembly e a UDT idênticos sejam registrados em cada banco de dados. Quando o assembly do UDT é registrado e o tipo é criado, você pode usar a UDT no [!INCLUDE[tsql](../../includes/tsql-md.md)] e em código de cliente. Para obter mais informações, veja [Tipos CLR definidos pelo usuário](clr-user-defined-types.md).  
  
## <a name="using-visual-studio-to-deploy-udts"></a>Usando o Visual Studio para implantar UDTs  
 O modo mais fácil de implantar seu UDT é usar o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio. Para cenários de implantação mais complexos e mais flexibilidade, entretanto, use o [!INCLUDE[tsql](../../includes/tsql-md.md)] como discutido posteriormente neste tópico.  
  
 Siga estas etapas para criar e implantar um UDT usando o Visual Studio:  
  
1.  Crie um novo projeto de **banco de dados** nos nós de linguagem **Visual Basic** ou **Visual C#** .  
  
2.  Acrescente uma referência ao banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que conterá a UDT.  
  
3.  Adicione uma classe de **tipo definida pelo usuário** .  
  
4.  Escreva o código para implementar a UDT.  
  
5.  No menu **Compilar** , selecione **implantar**. O assembly será registrado e o tipo será criado no banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="using-transact-sql-to-deploy-udts"></a>Usando o Transact-SQL para implantar UDTs  
 A sintaxe CREATE ASSEMBLY do [!INCLUDE[tsql](../../includes/tsql-md.md)] é usada para registrar o assembly no banco de dados no qual você deseja usar a UDT. Ele é armazenado internamente em tabelas do sistema do banco de dados, e não externamente, no sistema de arquivos. Se a UDT for dependente de assembly externos, eles também deverão ser carregados no banco de dados. A instrução CREATE TYPE é usada para criar a UDT no banco de dados no qual será usada. Para obter mais informações, consulte [criar ASSEMBLY &#40;Transact-sql&#41;](/sql/t-sql/statements/create-assembly-transact-sql) e [criar tipo &#40;&#41;do Transact-SQL ](/sql/t-sql/statements/create-type-transact-sql).  
  
### <a name="using-create-assembly"></a>Usando CREATE ASSEMBLY  
 A sintaxe CREATE ASSEMBLY registra o assembly no banco de dados no qual você deseja usar a UDT. Quando o assembly é registrado, não possui dependências.  
  
 Não é permitido criar várias versões do mesmo assembly em um determinado banco de dados. Entretanto, é possível criar várias versões do mesmo assembly com base em cultura em um determinado banco de dados. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferencia várias versões de cultura de um assembly por nomes diferentes dos registrados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte “Criando e usando assemblies de nome forte”, no SDK do .NET Framework.  
  
 Quando CREATE ASSEMBLY for executada com o conjunto de permissões SAFE ou EXTERNAL_ACCESS, o assembly será marcado para garantir que seja verificável e fortemente tipado. Se você omitir a especificação de um conjunto de permissões, SAFE será considerado. Códigos com o conjunto de permissões UNSAFE não serão marcados. Para obter mais informações sobre conjuntos de permissões de assembly, confira [Criando assemblies](../../relational-databases/clr-integration/assemblies-designing.md).  
  
#### <a name="example"></a>Exemplo  
 A instrução a seguir [!INCLUDE[tsql](../../includes/tsql-md.md)] registra o assembly de ponto no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no banco de dados **AdventureWorks** , com o conjunto de permissões seguro. Se a cláusula WITH PERMISSION_SET for omitida, o assembly será registrado com o conjunto de permissões SAFE.  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM '\\ShareName\Projects\Point\bin\Point.dll'   
WITH PERMISSION_SET = SAFE;  
```  
  
 A instrução a seguir [!INCLUDE[tsql](../../includes/tsql-md.md)] registra o assembly usando *<argumento assembly_bits>* na cláusula FROM. Este valor `varbinary` representa o arquivo como um fluxo de bytes.  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM 0xfeac4 ... 21ac78  
```  
  
### <a name="using-create-type"></a>Usando CREATE TYPE  
 Quando o assembly é carregado no banco de dados, você pode criar o tipo que usa a instrução do [!INCLUDE[tsql](../../includes/tsql-md.md)]. Isto acrescenta o tipo à lista de tipos disponíveis para esse banco de dados. O tipo tem escopo de banco de dados e só pode ser usado no banco de dados no qual foi criado. Se a UDT já existir no banco de dados, a instrução de CREATE TYPE falhará com um erro.  
  
> [!NOTE]  
>  A sintaxe CREATE TYPE também é usada para criar tipos de dados de alias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e tem o objetivo de substituir `sp_addtype` como uma forma de criar tipos de dados de alias. Alguns argumentos opcionais da sintaxe CREATE TYPE se referem à criação de UDTs e não são aplicáveis à criação de tipos de dados de alias (como um tipo de base).  
  
 Para obter mais informações, consulte [criar tipo &#40;&#41;Transact-SQL ](/sql/t-sql/statements/create-type-transact-sql).  
  
#### <a name="example"></a>Exemplo  
 A instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir cria o tipo `Point`. O nome externo é especificado usando a sintaxe de nomenclatura de duas partes de *AssemblyName*. *UDTName*.  
  
```  
CREATE TYPE dbo.Point   
EXTERNAL NAME Point.[Point];  
```  
  
## <a name="removing-a-udt-from-the-database"></a>Removendo uma UDT do banco de dados  
 A instrução de DROP TYPE remove uma UDT do banco de dados atual. Quando uma UDT é descartada, você pode usar a instrução de DROP ASSEMBLY para descartar o assembly do banco de dados.  
  
 A instrução de DROP TYPE não é executada nas seguintes situações:  
  
-   Tabelas no banco de dados que contêm colunas definidas usando a UDT.  
  
-   Funções, procedimentos armazenados ou gatilhos que usam variáveis ou parâmetros da UDT, criadas no banco de dados com a cláusula WITH SCHEMABINDING.  
  
### <a name="example"></a>Exemplo  
 O [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir deve ser executado nesta ordem: Primeiro, a tabela que referencia a UDT `Point` deve ser descartada, depois o tipo e, finalmente, o assembly.  
  
```  
DROP TABLE dbo.Points;  
DROP TYPE dbo.Point;  
DROP ASSEMBLY Point;  
```  
  
### <a name="finding-udt-dependencies"></a>Localizando dependências do UDT  
 Se houver objetos dependentes, como tabelas com definições de coluna de UDT, a instrução DROP TYPE falhará. Ela também falhará se houver funções, procedimentos armazenados ou gatilhos criados no banco de dados usando a cláusula WITH SCHEMABINDING, se essas rotinas usarem variáveis ou parâmetros do tipo definido pelo usuário. Você deve descartar todos os objetos dependentes primeiro e, em seguida, executar a instrução DROP TYPE.  
  
 A consulta a seguir [!INCLUDE[tsql](../../includes/tsql-md.md)] localiza todas as colunas e parâmetros que usam um UDT no banco de dados **AdventureWorks** .  
  
```  
USE Adventureworks;  
SELECT o.name AS major_name, o.type_desc AS major_type_desc  
     , c.name AS minor_name, c.type_desc AS minor_type_desc  
     , at.assembly_class  
  FROM (  
        SELECT object_id, name, user_type_id, 'SQL_COLUMN' AS type_desc  
          FROM sys.columns  
     UNION ALL  
        SELECT object_id, name, user_type_id, 'SQL_PROCEDURE_PARAMETER'  
          FROM sys.parameters  
     ) AS c  
  JOIN sys.objects AS o  
    ON o.object_id = c.object_id  
  JOIN sys.assembly_types AS at  
    ON at.user_type_id = c.user_type_id;  
```  
  
## <a name="maintaining-udts"></a>Mantendo UDTs  
 Não é possível modificar um UDT quando ele for criado em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], embora você possa alterar o assembly em que o tipo é baseado.  Na maioria dos casos, você deve remover a UDT do banco de dados com a instrução DROP TYPE do [!INCLUDE[tsql](../../includes/tsql-md.md)], fazer alterações no assembly subjacente e recarregar usando a instrução ALETER ASSEMBLY.  Em seguida, será necessário recriar a UDT e todos os objetos dependentes.  
  
### <a name="example"></a>Exemplo  
 A instrução ALTER ASSEMBLY é usada depois que você faz alterações no código-fonte no assembly do seu UDT e o recompila. Ele copia o arquivo .dll no servidor e o associa novamente ao novo assembly. Para obter a sintaxe completa, consulte [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql).  
  
 A instrução ALTER ASSEMBLY do [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir recarregar o assembly Point.dll do local especificado no disco.  
  
```  
ALTER ASSEMBLY Point  
FROM '\\Projects\Point\bin\Point.dll'  
```  
  
### <a name="using-alter-assembly-to-add-source-code"></a>Usando ALTER ASSEMBLY para adicionar código-fonte  
 A cláusula ADD FILE na sintaxe ALTER ASSEMBLY não está presente em CREATE ASSEMBLY. Você pode usá-la para adicionar código-fonte ou outros arquivos associados a um assembly. Os arquivos serão copiados dos seus locais originais e armazenados em tabelas do sistema do banco de dados. Isso garante que você sempre tenha código-fonte ou outros arquivos à mão, se precisar recriar ou documentar a versão atual do UDT.  
  
 A [!INCLUDE[tsql](../../includes/tsql-md.md)] instrução ALTER assembly a seguir adiciona o código-fonte da classe Point.cs para o `Point` UDT. O texto contendo o arquivo Point.cs será copiado e armazenado no banco de dados com o nome "PointSource".  
  
```  
ALTER ASSEMBLY Point  
ADD FILE FROM '\\Projects\Point\Point.cs' AS PointSource;  
```  
  
 As informações do assembly são armazenadas na tabela **Sys. assembly_files** no banco de dados em que o assembly foi instalado. A tabela **Sys. assembly_files** contém as colunas a seguir.  
  
 **assembly_id**  
 O identificador definido para o assembly. Este número é atribuído a todos os objetos relacionados ao mesmo assembly.  
  
 **name**  
 O nome do objeto.  
  
 **file_id**  
 Um número que identifica cada objeto, com o primeiro objeto associado a um determinado **assembly_id** dado o valor de 1. Se houver vários objetos associados ao mesmo **assembly_id**, cada valor de **file_id** subsequente será incrementado em 1.  
  
 **content**  
 A representação hexadecimal do assembly ou arquivo.  
  
 Você pode usar a função CAST ou CONVERT para converter o conteúdo da coluna de **conteúdo** em texto legível. A consulta a seguir converte o conteúdo do arquivo Point.cs a texto legível usando o nome da cláusula WHERE para restringir o conjunto de resultados definido a uma única linha.  
  
```  
SELECT CAST(content AS varchar(8000))   
  FROM sys.assembly_files   
  WHERE name='PointSource';  
```  
  
 Se você copiar e colar os resultados em um editor de texto, verá que as quebras de linha e os espaços que existiam no original foram preservados.  
  
## <a name="managing-udts-and-assemblies"></a>Gerenciando UDTs e assemblies  
 Ao planejar a implementação de UDTs, considere quais métodos são necessários no assembly do UDT propriamente dito e quais métodos devem ser criados em assemblies separados e implementados como funções definidas pelo usuário ou procedimentos armazenados. Separar métodos em assemblies à parte permite atualizar o código sem afetar os dados que podem ser armazenados em uma coluna de UDT na tabela. A modificação dos assemblies de UDT sem descartar colunas de UDT e outros objetos dependentes só é possível quando a nova definição puder ler os valores iniciais e a assinatura do tipo não for alterada.  
  
 Separar o código de procedimento que pode ser alterado do código necessário para implementar a UDT simplifica muito a manutenção. Incluir somente do código necessário para que a UDT funcione e manter suas definições de UDT o mais simples possível reduzem o risco da necessidade de descarte do próprio UDT do banco de dados para revisões de código ou correção de bug.  
  
### <a name="the-currency-udt-and-currency-conversion-function"></a>A função Conversão de moeda e conversão de UDT  
 A **moeda** UDT no banco de dados de exemplo **AdventureWorks** fornece um exemplo útil da maneira recomendada para estruturar um UDT e suas funções associadas. O UDT de **moeda** é usado para lidar com o dinheiro com base no sistema monetário de uma cultura específica e permite o armazenamento de diferentes tipos de moeda, como dólares, euros e assim por diante. A classe do UDT expõe o nome da cultura como uma cadeia de caracteres e o valor de dinheiro como um tipo de dados `decimal`. Todos os métodos de serialização necessários são contidos no assembly que define a classe. A função que implementa a conversão de moeda de uma cultura para outra é implementada como uma função externa chamada **ConvertCurrency**, e essa função está localizada em um assembly separado. A função **ConvertCurrency** faz seu trabalho recuperando a taxa de conversão de uma tabela no banco de dados **AdventureWorks** . Se a origem das taxas de conversão precisar ser alterada ou se houver outras alterações no código existente, o assembly poderá ser facilmente modificado sem afetar o UDT da **moeda** .  
  
 A listagem de código para as funções UDT e **ConvertCurrency** de **moeda** pode ser encontrada instalando os exemplos de Common Language Runtime (CLR).  
  
### <a name="using-udts-across-databases"></a>Usando UDTs nos bancos de dados  
 Por definição, os UDTs têm escopo em um único banco de dados. Por isso, um UDT definido em um banco de dados não pode ser usado em uma definição de coluna de outro banco de dados. Para usar UDTs em vários bancos de dados, você deve executar as instruções CREATE ASSEMBLY e CREATE TYPE em cada banco de dados em assemblies idênticos. Os assemblies são considerados idênticos se tiverem os mesmos nome, nome forte, cultura, versão, conjunto de permissões e conteúdo binário.  
  
 Quando a UDT for registrado e estiver acessível nos dois bancos de dados, você poderá converter o valor de UDT de um banco de dados para o outro. UDTs idênticos podem ser usados por bancos de dados nos seguintes cenários:  
  
-   Chamar um procedimento armazenado definido em bancos de dados diferentes.  
  
-   Consultar tabelas definidas em bancos de dados diferentes.  
  
-   Selecionar dados de UDT de uma coluna de UDT da tabela do banco de dados inserindo-a em um segundo banco de dados com coluna de UDT idêntica.  
  
 Nessas situações, qualquer conversão necessária do servidor ocorre automaticamente. Você não pode executar as conversões que usam explicitamente as funções CAST ou CONVERT do [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Observe que você não precisa realizar nenhuma ação para usar UDTs quando [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] o cria tabelas de trabalho no banco de dados do sistema **tempdb** . Isso inclui a manipulação de cursores, variáveis de tabela e funções com valor de tabela definidas pelo usuário que incluem UDTs e que usam de forma transparente o **tempdb**. No entanto, se você criar explicitamente uma tabela temporária em **tempdb** que define uma coluna UDT, o UDT deverá ser registrado em **tempdb** da mesma maneira que para um banco de dados de usuário.  
  
## <a name="see-also"></a>Consulte Também  
 [Tipos CLR definidos pelo usuário](clr-user-defined-types.md)  
  
  
