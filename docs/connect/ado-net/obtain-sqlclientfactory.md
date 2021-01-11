---
title: Obter um SqlClientFactory
description: Saiba como obter um SqlClientFactory da classe DbProviderFactories para trabalhar com fontes de dados específicas no .NET.
ms.date: 12/22/2020
ms.assetid: a16e4a4d-6a5b-45db-8635-19570e4572ae
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 891cabf04bc8e63537983a91d8526a5cbdf238bf
ms.sourcegitcommit: c938c12cf157962a5541347fcfae57588b90d929
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2020
ms.locfileid: "97771748"
---
# <a name="obtain-a-sqlclientfactory"></a>Obter um SqlClientFactory

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

O processo de obter <xref:System.Data.Common.DbProviderFactory> envolve passar informações sobre um provedor de dados para a classe <xref:System.Data.Common.DbProviderFactories>. Com base nessas informações, o método <xref:System.Data.Common.DbProviderFactories.GetFactory%2A> cria uma fábrica de provedor fortemente tipada. Por exemplo, para criar um <xref:Microsoft.Data.SqlClient.SqlClientFactory>, você pode transmitir uma cadeia de caracteres para `GetFactory` com o nome do provedor especificado como "**Microsoft.Data.SqlClient**".

Outra sobrecarga de `GetFactory` utiliza <xref:System.Data.DataRow>. Uma vez que você criar a fábrica de provedor, poderá usar seus métodos para criar objetos adicionais. Alguns dos métodos de `SqlClientFactory` incluem <xref:Microsoft.Data.SqlClient.SqlClientFactory.CreateConnection%2A>, <xref:Microsoft.Data.SqlClient.SqlClientFactory.CreateCommand%2A> e <xref:Microsoft.Data.SqlClient.SqlClientFactory.CreateDataAdapter%2A>.

## <a name="register-sqlclientfactory"></a>Registrar o SqlClientFactory

Para recuperar o objeto <xref:Microsoft.Data.SqlClient.SqlClientFactory> pela classe <xref:System.Data.Common.DbProviderFactories> no .NET Framework, é necessário registrá-lo em um arquivo **App.config** ou **web.config**. O fragmento do arquivo de configuração a seguir mostra a sintaxe e o formato para <xref:Microsoft.Data.SqlClient>.  

```xml  
<system.data>
  <DbProviderFactories>
    <add name="Microsoft SqlClient Data Provider"
      invariant="Microsoft.Data.SqlClient"
      description="Microsoft SqlClient Data Provider for SQL Server"
      type="Microsoft.Data.SqlClient.SqlClientFactory, Microsoft.Data.SqlClient, Version=2.0.20168.4, Culture=neutral, PublicKeyToken=23ec7fc2d6eaa4a5"/>
  </DbProviderFactories>
</system.data>  
```  

O atributo **invariant** identifica o provedor de dados subjacente. Essa sintaxe de nomenclatura de três partes também é usada na criação de uma nova fábrica e para identificar o provedor em um arquivo de configuração de aplicativo, de forma que o nome do provedor, juntamente com a cadeia de conexão associada, possa ser recuperado em tempo de execução.  

> [!NOTE]  
> No .NET Core, como não há nenhum GAC ou suporte de configuração global, o objeto <xref:Microsoft.Data.SqlClient.SqlClientFactory> deve ser registrado chamando o método <xref:System.Data.Common.DbProviderFactories.RegisterFactory%2A> no projeto.

O exemplo a seguir mostra como usar o <xref:Microsoft.Data.SqlClient.SqlClientFactory> em um aplicativo .NET Core.

[!code-csharp[SqlClientFactory_Netcoreapp#1](~/../sqlclient/doc/samples/SqlClientFactory_Netcoreapp.cs#1)]

## <a name="see-also"></a>Consulte também

- [DbProviderFactories](dbproviderfactories.md)
- [Cadeias de conexão](connection-strings.md)
- [Como usar as classes de configuração](/previous-versions/aspnet/ms228063(v=vs.100))
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
