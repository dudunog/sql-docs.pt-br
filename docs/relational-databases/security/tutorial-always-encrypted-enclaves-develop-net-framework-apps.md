---
description: 'Tutorial: Desenvolver um aplicativo .NET Framework usando o Always Encrypted com enclaves seguros'
title: 'Tutorial: Desenvolver um aplicativo .NET Framework usando o Always Encrypted com enclaves seguros | Microsoft Docs'
ms.custom: ''
ms.date: 01/15/2021
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15'
ms.openlocfilehash: 092220a2ef2715b8d5cd414ab5a4bc3e3493acb5
ms.sourcegitcommit: 8ca4b1398e090337ded64840bcb8d6c92d65c29e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2021
ms.locfileid: "98534735"
---
# <a name="tutorial-develop-a-net-framework-application-using-always-encrypted-with-secure-enclaves"></a>Tutorial: Desenvolver um aplicativo .NET Framework usando o Always Encrypted com enclaves seguros

[!INCLUDE [sqlserver2019-windows-only-asdb](../../includes/applies-to-version/sqlserver2019-windows-only-asdb.md)]

Este tutorial ensina como desenvolver um aplicativo que emite consultas de banco de dados que usam um enclave seguro no lado do servidor para o [Always Encrypted com enclaves seguros](encryption/always-encrypted-enclaves.md). 

## <a name="prerequisites"></a>Pré-requisitos
Conclua um dos tutoriais abaixo antes de seguir as etapas deste tutorial:

- [Tutorial: Introdução ao Always Encrypted com enclaves seguros no SQL Server](tutorial-getting-started-with-always-encrypted-enclaves.md)
- [Tutorial: Introdução ao Always Encrypted com enclaves seguros no Banco de Dados SQL do Azure](/azure/azure-sql/database/always-encrypted-enclaves-getting-started)

Você também precisará ter o Visual Studio (a versão 2019 é recomendada). Baixe-o em [https://visualstudio.microsoft.com/](https://visualstudio.microsoft.com). O computador de desenvolvimento de aplicativo precisa executar o .NET Framework 4.7.2 ou posterior.

## <a name="step-1-set-up-your-visual-studio-project"></a>Etapa 1: Configure seu projeto do Visual Studio

Para usar o Always Encrypted com enclaves seguros em um aplicativo .NET Framework, você precisa verificar se seu aplicativo foi compilado no .NET Framework 4.7.2 e está integrado ao [NuGet Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders). Além disso, se armazenar a chave mestra da coluna no Azure Key Vault, você também precisará integrar seu aplicativo ao [NuGet Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider), versão 2.2.0 ou posterior. 

1. Abra o Visual Studio.

2. Crie um novo projeto de Aplicativo de Console de C\# (.NET Framework).

3. Certifique-se de que seu projeto tenha como destino pelo menos o .NET Framework 4.7.2. Clique com o botão direito do mouse no projeto no Gerenciador de Soluções, selecione **Propriedades** e defina **Estrutura de destino** como .NET Framework 4.7.2.

4. Instale o seguinte pacote NuGet acessando **Ferramentas** (menu principal) > **Gerenciador de Pacotes NuGet** > **Console do Gerenciador de Pacotes**. Execute o seguinte código no Console do Gerenciador de Pacotes.

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders -IncludePrerelease
   ```

5. Se você usa o Azure Key Vault para armazenar chaves mestras de coluna, instale os seguintes pacotes NuGet acessando **Ferramentas** (menu principal) > **Gerenciador de Pacotes NuGet** > **Console do Gerenciador de Pacotes**. Execute o seguinte código no Console do Gerenciador de Pacotes.

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider -IncludePrerelease -Version 2.2.0
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```

6. Abra o arquivo de configuração do aplicativo do projeto.

7. Localize a seção `<configuration>` e adicione ou atualize as seções `<configSections>`.

   1. Se a seção de `<configuration>` **não** contiver a seção `<configSections>`, adicione o conteúdo a seguir imediatamente abaixo de `<configuration>`.

      ```xml
      <configSections>
        <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
      </configSections>
      ```

   2. Se a seção `<configuration>` já contiver a seção `<configSections>`, adicione a seguinte linha dentro da seção `<configSections>`:

      ```xml
      <section name="SqlColumnEncryptionEnclaveProviders"  type="System.   Data.SqlClient.   SqlColumnEncryptionEnclaveProviderConfigurationSection, System.   Data,  Version=4.0.0.0, Culture=neutral,    PublicKeyToken=b77a5c561934e089" />
      ```

8. Na seção `<configuration>`, abaixo de `</configSections>`, adicione uma nova seção, que especifica um provedor de enclave a ser usado para atestar o enclave seguro no lado do servidor e interagir com ele.

   1. Se você estiver usando o [!INCLUDE [ssnoversion-md](../../includes/ssnoversion-md.md)] e o HGS (Serviço Guardião de Host) (você está usando o banco de dados do [Tutorial: Introdução ao Always Encrypted com enclaves seguros no SQL Server](tutorial-getting-started-with-always-encrypted-enclaves.md)), adicione a seção abaixo.

      ```xml
      <SqlColumnEncryptionEnclaveProviders>
        <providers>
          <add name="VBS"  type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.HostGuardianServiceEnclaveProvider,  Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders,    Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91"/>
        </providers>
      </SqlColumnEncryptionEnclaveProviders>
      ```

      Veja um exemplo completo de um arquivo app.config de um aplicativo de console simples.

      ```xml
      <?xml version="1.0" encoding="utf-8" ?>
      <configuration>
        <configSections>
          <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
        </configSections>
        <SqlColumnEncryptionEnclaveProviders>
          <providers>
            <add name="VBS"  type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.HostGuardianServiceEnclaveProvider,  Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders,    Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91"/>
          </providers>
        </SqlColumnEncryptionEnclaveProviders>
        <startup> 
         <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7.2" />
        </startup>
      </configuration>
      ```

   1. Se você estiver usando o [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] e o Atestado do Microsoft Azure (você está usando o banco de dados do [Tutorial: Introdução ao Always Encrypted com enclaves seguros no Banco de Dados SQL do Azure](/azure/azure-sql/database/always-encrypted-enclaves-getting-started)), adicione a seção abaixo.

      ```xml
      <SqlColumnEncryptionEnclaveProviders>
        <providers>
          <add name="SGX" type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.AzureAttestationEnclaveProvider, Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" />
        </providers>
      </SqlColumnEncryptionEnclaveProviders>
      ```

      Veja um exemplo completo de um arquivo app.config de um aplicativo de console simples.

      ```xml
      <?xml version="1.0" encoding="utf-8" ?>
      <configuration>
        <configSections>
          <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
        </configSections>
        <SqlColumnEncryptionEnclaveProviders>
          <providers>
            <add name="SGX" type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.AzureAttestationEnclaveProvider, Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders, Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" />
          </providers>
        </SqlColumnEncryptionEnclaveProviders>
        <startup> 
         <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7.2" />
        </startup>
      </configuration>
      ```

## <a name="step-2-implement-your-application-logic"></a>Etapa 2: Implementar a lógica do aplicativo

Seu aplicativo se conectará ao banco de dados **ContosoHR** do [Tutorial: Introdução ao Always Encrypted com enclaves seguros no SQL Server](tutorial-getting-started-with-always-encrypted-enclaves.md) ou do [Tutorial: Introdução ao Always Encrypted com enclaves seguros no Banco de Dados SQL do Azure](/azure/azure-sql/database/always-encrypted-enclaves-getting-started) e executará uma consulta que contém o predicado `LIKE` na coluna **SSN** e uma comparação de intervalo na coluna **Salário**.

1. Substitua o conteúdo do arquivo Program.cs (gerado pelo Visual Studio) pelo código abaixo. Atualize a cadeia de conexão de banco de dados com o nome do servidor, as configurações de autenticação do banco de dados e a URL de atestado de enclave do seu ambiente.

    ```cs
    using System;
    using System.Data.SqlClient;
    using System.Data;

    namespace ConsoleApp1
    {
        class Program
        {
            static void Main(string[] args)
            {
    
                string connectionString = "Data Source = myserver; Initial Catalog = ContosoHR; Column Encryption Setting = Enabled;Enclave Attestation Url = http://hgs.bastion.local/Attestation; Integrated Security = true";

                //string connectionString = "Data Source = myserver.database.windows.net; Initial Catalog = ContosoHR; Column Encryption Setting = Enabled;Enclave Attestation Url = https://myattestationprovider.uks.attest.azure.net/attest/SgxEnclave; User ID=user; Password=password";

                using (SqlConnection connection = new SqlConnection(connectionString))
                {
                    connection.Open();

                    SqlCommand cmd = connection.CreateCommand();
                    cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [Salary] FROM [HR].[Employees] WHERE [SSN] LIKE @SSNPattern AND [Salary] > @MinSalary;";

                    SqlParameter paramSSNPattern = cmd.CreateParameter();

                    paramSSNPattern.ParameterName = @"@SSNPattern";
                    paramSSNPattern.DbType = DbType.AnsiStringFixedLength;
                    paramSSNPattern.Direction = ParameterDirection.Input;
                    paramSSNPattern.Value = "%9838";
                    paramSSNPattern.Size = 11;

                    cmd.Parameters.Add(paramSSNPattern);

                    SqlParameter MinSalary = cmd.CreateParameter();

                    MinSalary.ParameterName = @"@MinSalary";
                    MinSalary.DbType = DbType.Currency;
                    MinSalary.Direction = ParameterDirection.Input;
                    MinSalary.Value = 20000;

                    cmd.Parameters.Add(MinSalary);
                    cmd.ExecuteNonQuery();
    
                    SqlDataReader reader = cmd.ExecuteReader();
                    while (reader.Read())

                    {
                        Console.WriteLine(reader[0] + ", " + reader[1] + ", " + reader[2] + ", " + reader[3]);
                    }   
                    Console.ReadKey();
                }
            }
        }
    }
    ```

2. Criar e executar o aplicativo.  

## <a name="see-also"></a>Consulte Também

- [Usando o Always Encrypted com o Provedor de Dados .NET Framework para SQL Server](encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)
- [Tutorial: Desenvolver um aplicativo .NET usando o Always Encrypted com enclaves seguros](../../connect/ado-net/sql/tutorial-always-encrypted-enclaves-develop-net-apps.md)
