---
title: Especificando valores XML como parâmetros
description: Demonstra como passar dados XML como um parâmetro para um comando.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 2c4d08b8-fc29-4614-97fa-29c8ff7ca5b3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: b4d0f31c8f5fbb282c880abaee62f05dc190bbfc
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896655"
---
# <a name="specifying-xml-values-as-parameters"></a>Especificando valores XML como parâmetros

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

Se uma consulta exigir um parâmetro cujo valor é uma cadeia de caracteres XML, os desenvolvedores poderão fornecer esse valor usando uma instância do tipo de dados **SqlXml**. Não há nenhuma pegadinha: as colunas XML no SQL Server aceitam valores de parâmetro exatamente da mesma maneira que outros tipos de dados.  
  
## <a name="example"></a>Exemplo  
O aplicativo de console a seguir cria uma tabela no banco de dados **AdventureWorks**. A nova tabela inclui uma coluna chamada **SalesID** e uma coluna XML denominada **SalesInfo**.  
  
> [!NOTE]
>  O banco de dados **AdventureWorks** de exemplo não é instalado por padrão quando você instala o SQL Server. Você pode instalá-lo executando a Instalação do SQL Server.  
  
O exemplo prepara um objeto <xref:Microsoft.Data.SqlClient.SqlCommand> para inserir uma linha na nova tabela. Um arquivo salvo fornece os dados XML necessários para a coluna **SalesInfo**.  
  
Para criar o arquivo necessário para que o exemplo seja executado, crie um arquivo de texto na mesma pasta que o seu projeto. Nomeie o arquivo MyTestStoreData.xml. Abra o arquivo no bloco de notas e copie e cole o seguinte texto:  
  
```xml  
<StoreSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
  <AnnualSales>300000</AnnualSales>  
  <AnnualRevenue>30000</AnnualRevenue>  
  <BankName>International Bank</BankName>  
  <BusinessType>BM</BusinessType>  
  <YearOpened>1970</YearOpened>  
  <Specialty>Road</Specialty>  
  <SquareFeet>7000</SquareFeet>  
  <Brands>3</Brands>  
  <Internet>T1</Internet>  
  <NumberEmployees>2</NumberEmployees>  
</StoreSurvey>  
```  
  
```csharp  
using System;  
using System.Data;  
using Microsoft.Data.SqlClient;  
using System.Xml;  
using System.Data.SqlTypes;  
  
class Class1  
{  
    static void Main()  
    {  
        using (SqlConnection connection = new SqlConnection(GetConnectionString()))  
       {  
        connection.Open();  
        //  Create a sample table (dropping first if it already  
        //  exists.)  
  
        string commandNewTable =   
            "IF EXISTS (SELECT * FROM dbo.sysobjects " +   
            "WHERE id = " +  
                  "object_id(N'[dbo].[XmlDataTypeSample]') " +   
            "AND OBJECTPROPERTY(id, N'IsUserTable') = 1) " +   
            "DROP TABLE [dbo].[XmlDataTypeSample];" +   
            "CREATE TABLE [dbo].[XmlDataTypeSample](" +   
            "[SalesID] [int] IDENTITY(1,1) NOT NULL, " +   
            "[SalesInfo] [xml])";  
        SqlCommand commandAdd =   
                   new SqlCommand(commandNewTable, connection);  
        commandAdd.ExecuteNonQuery();  
        string commandText =   
            "INSERT INTO [dbo].[XmlDataTypeSample] " +   
            "([SalesInfo] ) " +   
            "VALUES(@xmlParameter )";  
        SqlCommand command =   
                  new SqlCommand(commandText, connection);  
  
        //  Read the saved XML document as a   
        //  SqlXml-data typed variable.  
        SqlXml newXml =   
            new SqlXml(new XmlTextReader("MyTestStoreData.xml"));  
  
        //  Supply the SqlXml value for the value of the parameter.  
        command.Parameters.AddWithValue("@xmlParameter", newXml);  
  
        int result = command.ExecuteNonQuery();  
        Console.WriteLine(result + " row was added.");  
        Console.WriteLine("Press Enter to continue.");  
        Console.ReadLine();  
    }  
  }  
  
    private static string GetConnectionString()  
    {  
        // To avoid storing the connection string in your code,              
        // you can retrieve it from a configuration file.   
        return "Data Source=(local);Integrated Security=true;" +  
        "Initial Catalog=AdventureWorks; ";  
    }  
}  
```  
  
## <a name="next-steps"></a>Próximas etapas
- <xref:System.Data.SqlTypes.SqlXml>
- [Dados XML no SQL Server](xml-data-sql-server.md)
