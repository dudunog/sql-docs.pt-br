---
description: MSSQLSERVER_6522
title: MSSQLSERVER_6522
ms.custom: ''
ms.date: 12/25/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 6522 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 836ad79e049d7c5613755e64ca441f9ed5d73048
ms.sourcegitcommit: d819173fb91af6f20ca6ee59686c35c71b060fbc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/28/2020
ms.locfileid: "97797792"
---
# <a name="mssqlserver_6522"></a>MSSQLSERVER_6522
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|6522|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|SQLCLR_UDF_EXEC_FAILED|
|Texto da mensagem|Ocorreu um erro do .NET Framework durante a execução da agregação ou da rotina definida pelo usuário "%.*ls": %ls.|
||

## <a name="explanation"></a>Explicação

Considere os seguintes cenários.

### <a name="scenario-1"></a>Cenário 1

Você criará uma rotina do CLR (Common Language Runtime) que referencia um assembly do Microsoft .NET Framework. O assembly do .NET Framework não está documentado em [922672](/troubleshoot/sql/database-design/policy-untested-net-framework-assemblies). Em seguida, você instalará o .NET Framework 3.5 ou um hotfix baseado no .NET Framework 2.0.

### <a name="scenario-2"></a>Cenário 2

Você criará um assembly e o registrará em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Depois, você instalará outra versão do assembly no GAC (cache de assembly global).

Ao executar a rotina do CLR ou usar o assembly de um desses cenários no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], você receberá uma mensagem de erro semelhante à seguinte:

> Servidor:  Mensagem 6522, Nível 16, Estado 2, Linha 1  
Ocorreu um erro do .NET Framework durante a execução da agregação ou da rotina definida pelo usuário 'getsid':
>
> System.IO.FileLoadException: Não foi possível carregar o arquivo nem o assembly 'System.DirectoryServices, Version=2.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a' nem uma das dependências dele. O assembly no repositório do host tem uma assinatura diferente daquela do assembly no GAC. (Exceção de HRESULT: 0x80131050)

## <a name="possible-cause"></a>Causa possível

Quando o CLR carrega um assembly, ele verifica se o mesmo assembly está no GAC. Se o mesmo assembly estiver no GAC, o CLR verificará se as MVIDs (IDs de Versão do Módulo) desses assemblies são correspondentes. Se as MVIDs desses assemblies não forem correspondentes, você receberá a mensagem de erro informando uma menção disso na seção [Explicação](#explanation).

Quando um assembly é recompilado, a MVID do assembly é alterada. Portanto, se você atualizar o .NET Framework, os assemblies do .NET Framework terão MVIDs diferentes, porque esses assemblies serão recompilados. Além disso, se você atualizar seu assembly, ele será recompilado. Portanto, o assembly também tem outra MVID.

## <a name="user-action"></a>Ação do usuário

### <a name="action-1"></a>Action 1

Para resolver o cenário 1 na seção [Explicação](#explanation), você precisará atualizar manualmente os assemblies do .NET Framework no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para fazer isso, use a instrução `ALTER ASSEMBLY` de modo que ela aponte para a nova versão do assembly do .NET Framework na seguinte pasta:

`%Windir%\Microsoft.NET\Framework\Version`

> [!NOTE]
> **Versão** representa a versão do .NET Framework instalada ou atualizada.

### <a name="action-2"></a>Ação 2

Para resolver o cenário 2 na seção [Explicação](#explanation), use a instrução `ALTER ASSEMBLY` para atualizar o assembly no banco de dados.

Se o problema ainda existir depois que você fizer isso, remova o assembly do banco de dados e registre a nova versão do assembly no banco de dados.

## <a name="more-information"></a>Mais informações

Não recomendamos que você use assemblies do .NET Framework que não estejam documentados em [Política de suporte para assemblies do .NET Framework não testados no ambiente hospedado pelo CLR do SQL Server](/troubleshoot/sql/database-design/policy-untested-net-framework-assemblies). O artigo lista os assemblies que foram testados no ambiente hospedado no CLR do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

### <a name="description-of-clr-routines"></a>Descrição das rotinas do CLR

As rotinas do CLR incluem os seguintes objetos que são implementados usando a integração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao CLR do .NET Framework:

- Funções definidas pelo usuário com valor escalar (UDFs escalares)
- Funções definidas pelo usuário com valor de tabela (TVFs)
- Procedimentos definidos pelo usuário (UDPs)
- Gatilhos definidos pelo usuário
- Tipos de dados definidos pelo usuário
- Agregações definidas pelo usuário

### <a name="assemblies-to-update-after-you-install-the-net-framework-35"></a>Assemblies a serem atualizados após a instalação do .NET Framework 3.5

Depois de instalar o .NET Framework 3.5, você precisará usar a instrução ALTER ASSEMBLY para atualizar os seguintes assemblies:

- Accessibility.dll
- AspNetMMCExt.dll
- Cscompmgd.dll
- IEExecRemote.dll
- IEHost.dll
- IIEHost.dll
- Microsoft.Build.Conversion.dll
- Microsoft.Build.Engine.dll
- Microsoft.Build.Framework.dll
- Microsoft.Build.Tasks.dll 
- Microsoft.Build.Utilities.dll 
- Microsoft.CompactFramework.Build.Tasks.dll 
- Microsoft.JScript.dll 
- Microsoft.VisualBasic.Vsa.dll 
- Microsoft.Vsa.dll 
- Microsoft.Vsa.Vb.CodeDOMProcessor.dll 
- Microsoft_VsaVb.dll 
- Sysglobl.dll 
- System.Configuration.Install.dll 
- System.Design.dll 
- System.DirectoryServices.dll 
- System.DirectoryServices.Protocols.dll 
- System.Drawing.dll 
- System.Drawing.Design.dll 
- System.EnterpriseServices.dll 
- System.Management.dll 
- System.Messaging.dll 
- System.Runtime.Serialization.Formatters.Soap.dll 
- System.ServiceProcess.dll 
- System.Web.dll 
- System.Web.Mobile.dll 
- System.Web.RegularExpressions.dll 

Esses assemblies estão na seguinte pasta:

`%Windir%\Microsoft.NET\Framework\v2.0.50727`

### <a name="how-to-preserve-the-data-from-user-defined-data-types-after-you-drop-an-assembly"></a>Como preservar os dados de tipos de dados definidos pelo usuário depois de remover um assembly

Se você remover um assembly usado por um tipo de dados definido pelo usuário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use um dos métodos a seguir para preservar os dados.

Imagine o seguinte cenário:

- Você cria um assembly cujo nome é *MyAssembly.dll*.
- O assembly MyAssembly referencia o assembly `System.DirectoryServices.dll`.
- Você tem um tipo de dados definido pelo usuário cujo nome é *MyDateTime*.
- O tipo de dados *MyDateTime* usa o assembly *MyAssembly.dll*.
- Você cria uma tabela cujo nome é *MyTable*.
- A tabela *MyTable* contém os dados do tipo de dados *MyDateTime*.

#### <a name="method-1-use-the-bcpexe-utility"></a>Método 1: Usar o utilitário bcp.exe

1. Use o utilitário bcp.exe junto com a opção -n para copiar os dados da tabela MyTable para um arquivo. Por exemplo, execute o seguinte comando em um prompt de comando:

    ```console
    bcp MyDatabase.dbo.MyTable out C:\MyFile.bcp -n -SSQLServerName -T
    ```

2. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio, siga estas etapas:
   1. Remova a tabela MyTable.
   2. Remova o tipo de dados MyDateTime.
   3. Remova o assembly `System.DirectoryServices.dll`.
   4. Remova o assembly MyAssembly.
3. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio, siga estas etapas:

   1. Registre o assembly `System.DirectoryServices.dll`.
   2. Registre o assembly MyAssembly.
   3. Crie o tipo de dados MyDateTime.
   4. Crie uma tabela que tenha a mesma estrutura da tabela MyTable.
4. Use o utilitário bcp.exe junto com a opção -n para importar os dados do arquivo para a tabela MyTable. Por exemplo, execute o seguinte comando em um prompt de comando:
  
    ```console
    bcp MyDatabase.dbo.MyTable in C:\MyFile.bcp -n -SSQLServerName -T
    ```

#### <a name="method-2-use-the-insert--select-statement"></a>Método 2: Use a instrução INSERT... Instrução SELECT

Suponha que o tipo de dados MyDateTime ocupe 9 bytes no armazenamento.

1. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio, crie uma tabela que contenha uma coluna do tipo de dados `VARBINARY(9)` executando a seguinte instrução:

    ```sql
    CREATE TABLE TempTable (c1 VARBINARY(9));
    ```

2. Execute a instrução INSERT... SELECT para preencher a tabela TempTable:

    ```sql
    INSERT INTO TempTable SELECT CAST(c1 as VARBINARY(9)) FROM MyTable;
    ```

3. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio, siga estas etapas:
   1. Remova a tabela MyTable.
   2. Remova o tipo de dados MyDateTime.
   3. Remova o assembly System.DirectoryServices.dll.
   4. Remova o assembly MyAssembly.
4. No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio, siga estas etapas:
   1. Registre o assembly System.DirectoryServices.dll.
   2. Registre o assembly MyAssembly.
   3. Crie o tipo de dados MyDateTime.
   4. Crie uma tabela que tenha a mesma estrutura da tabela MyTable.
5. Execute a instrução INSERT... SELECT para preencher a tabela MyTable:

    ```sql
    INSERT INTO MyTable SELECT c1 FROM TempTable;
    ```

## <a name="references"></a>Referências

- Para obter mais informações sobre a versão do assembly, confira [Documentação sobre a desativação do Visual Studio 2005](https://www.microsoft.com/download/details.aspx?id=55984).
- Para obter mais informações sobre como atualizar um assembly, confira [ALTER ASSEMBLY (Transact-SQL)](/sql/t-sql/statements/alter-assembly-transact-sql).
- Para obter mais informações sobre como remover um assembly, confira [DROP ASSEMBLY (Transact-SQL)](/sql/t-sql/statements/drop-assembly-transact-sql).
- Para obter mais informações sobre como registrar um assembly em um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], confira [CREATE ASSEMBLY (Transact-SQL)](/sql/t-sql/statements/create-assembly-transact-sql).
- Para obter mais informações sobre o utilitário bcp.exe, confira [https://msdn2.microsoft.com/library/ms162802.aspx](/sql/tools/bcp-utility).
