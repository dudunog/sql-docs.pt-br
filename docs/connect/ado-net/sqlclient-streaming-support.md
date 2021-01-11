---
title: Suporte a streaming no SqlClient
description: Explica como criar aplicativos que transmitem dados do SQL Server sem precisar carregá-los completamente na memória.
ms.date: 12/04/2020
ms.assetid: c449365b-470b-4edb-9d61-8353149f5531
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: c5ae05856f3f1e01d5831a6e80338f19e3994966
ms.sourcegitcommit: 4419e99d77ee2c73f9da1559c7944f7702f2de30
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/23/2020
ms.locfileid: "97744330"
---
# <a name="sqlclient-streaming-support"></a>Suporte a streaming no SqlClient

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

O suporte a streaming entre o SQL Server e um aplicativo aplica-se a dados não estruturados no servidor (documentos, imagens e arquivos de mídia). Um banco de dados do SQL Server pode armazenar BLOBs (objetos binários grandes), mas a recuperação de BLOBS pode usar muita memória.

O suporte a streaming no SQL Server simplifica a escrita de aplicativos que fazem streaming de dados, sem precisar carregar completamente os dados na memória, resultando em menos exceções de estouro de memória.

O suporte a streaming também permitirá que os aplicativos de camada intermediária sejam mais bem escalados, especialmente em cenários em que os objetos empresariais se conectam ao SQL do Azure para enviar, recuperar e manipular BLOBs grandes.

> [!WARNING]
> Os membros que dão suporte a streaming são usados para recuperar dados de consultas e transmitir parâmetros para consultas e procedimentos armazenados. O recurso de streaming aborda os cenários básicos de OLTP e migração de dados e é aplicável a ambientes de migração de dados locais e externos.

## <a name="streaming-support-from-sql-server"></a>Suporte a streaming do SQL Server

O suporte a streaming do SQL Server apresenta uma nova funcionalidade no <xref:System.Data.Common.DbDataReader> e nas classes <xref:Microsoft.Data.SqlClient.SqlDataReader> para obter os objetos <xref:System.IO.Stream>, <xref:System.Xml.XmlReader> e <xref:System.IO.TextReader> e fornecer uma resposta a eles. Essas classes são usadas para recuperar dados de consultas. Como resultado, o suporte a streaming do SQL Server aborda cenários de OLTP e aplica-se a ambientes locais e externos.

Os seguintes membros foram adicionados ao <xref:Microsoft.Data.SqlClient.SqlDataReader> para habilitar o suporte a streaming do SQL Server:

- <xref:Microsoft.Data.SqlClient.SqlDataReader.IsDBNullAsync%2A>

- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetFieldValue%2A?displayProperty=nameWithType>

- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetFieldValueAsync%2A>

- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetStream%2A>

- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetTextReader%2A>

- <xref:Microsoft.Data.SqlClient.SqlDataReader.GetXmlReader%2A>

Os seguintes membros foram adicionados ao <xref:System.Data.Common.DbDataReader> para habilitar o suporte a streaming do SQL Server:

- <xref:System.Data.Common.DbDataReader.GetFieldValue%2A>

- <xref:System.Data.Common.DbDataReader.GetStream%2A>

- <xref:System.Data.Common.DbDataReader.GetTextReader%2A>

## <a name="streaming-support-to-sql-server"></a>Suporte a streaming para o SQL Server

O suporte a streaming para o SQL Server está na classe <xref:Microsoft.Data.SqlClient.SqlParameter> de modo que ele possa aceitar objetos <xref:System.Xml.XmlReader>, <xref:System.IO.Stream> e <xref:System.IO.TextReader> e responder a eles. <xref:Microsoft.Data.SqlClient.SqlParameter> é usado para transmitir parâmetros para consultas e procedimentos armazenados.

> [!NOTE]
> Descartar um objeto <xref:Microsoft.Data.SqlClient.SqlCommand> ou chamar <xref:Microsoft.Data.SqlClient.SqlCommand.Cancel%2A> deve cancelar qualquer operação de streaming. Se um aplicativo enviar <xref:System.Threading.CancellationToken>, o cancelamento não será garantido.

Os seguintes tipos de <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A> aceitarão um <xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A> de <xref:System.IO.Stream>:

- **Binary**

- **VarBinary**

Os seguintes tipos de <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A> aceitarão um <xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A> de <xref:System.IO.TextReader>:

- **Char**

- **NChar**

- **NVarChar**

- **Xml**

O tipo **Xml**<xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A> aceitará um <xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A> de <xref:System.Xml.XmlReader>.

<xref:Microsoft.Data.SqlClient.SqlParameter.SqlValue%2A> pode aceitar valores do tipo <xref:System.Xml.XmlReader>, <xref:System.IO.TextReader> e <xref:System.IO.Stream>.

O objeto <xref:System.Xml.XmlReader>, <xref:System.IO.TextReader> e <xref:System.IO.Stream> serão transferidos até atingir o valor definido pelo <xref:Microsoft.Data.SqlClient.SqlParameter.Size%2A>.

## <a name="sample----streaming-from-sql-server"></a>Exemplo – Streaming do SQL Server

Use o seguinte Transact-SQL para criar o banco de dados de exemplo:

```sql
CREATE DATABASE [Demo]
GO
USE [Demo]
GO
CREATE TABLE [Streams] (
[id] INT PRIMARY KEY IDENTITY(1, 1),
[textdata] NVARCHAR(MAX),
[bindata] VARBINARY(MAX),
[xmldata] XML)
GO
INSERT INTO [Streams] (textdata, bindata, xmldata) VALUES (N'This is a test', 0x48656C6C6F, N'<test>value</test>')
INSERT INTO [Streams] (textdata, bindata, xmldata) VALUES (N'Hello, World!', 0x54657374696E67, N'<test>value2</test>')
INSERT INTO [Streams] (textdata, bindata, xmldata) VALUES (N'Another row', 0x666F6F626172, N'<fff>bbb</fff><fff>bbc</fff>')
GO
```

O exemplo a seguir mostra como fazer o seguinte:

- Evite fechar um thread da interface do usuário fornecendo uma maneira assíncrona de recuperar arquivos grandes.

- Transferir um arquivo de texto grande do SQL Server no .NET.

- Transferir um arquivo XML grande do SQL Server no .NET.

- Recuperar dados do SQL Server.

- Transferir arquivos grandes (BLOBs) de um banco de dados do SQL Server para outro sem ficar sem memória.

[!code-csharp[SqlClient_Streaming_FromServer#1](~/../sqlclient/doc/samples/SqlClient_Streaming_FromServer.cs#1)]

## <a name="sample----streaming-to-sql-server"></a>Exemplo – Streaming para o SQL Server

Use o seguinte Transact-SQL para criar o banco de dados de exemplo:

```sql
CREATE DATABASE [Demo2]
GO
USE [Demo2]
GO
CREATE TABLE [BinaryStreams] (
[id] INT PRIMARY KEY IDENTITY(1, 1),
[bindata] VARBINARY(MAX))
GO
CREATE TABLE [TextStreams] (
[id] INT PRIMARY KEY IDENTITY(1, 1),
[textdata] NVARCHAR(MAX))
GO
CREATE TABLE [BinaryStreamsCopy] (
[id] INT PRIMARY KEY IDENTITY(1, 1),
[bindata] VARBINARY(MAX))
GO
```

O exemplo a seguir mostra como fazer o seguinte:

- Transferir um BLOB grande para o SQL Server no .NET.

- Transferir um arquivo de texto grande para o SQL Server no .NET.

- Usando o novo recurso assíncrono para transferir um BLOB grande.

- Usando o novo recurso assíncrono e a palavra-chave await para transferir um BLOB grande.

- Cancelar a transferência de um BLOB grande.

- Streaming de um SQL Server para outro usando o recurso assíncrono.

[!code-csharp[SqlClient_Streaming_ToServer#1](~/../sqlclient/doc/samples/SqlClient_Streaming_ToServer.cs#1)]

## <a name="sample----streaming-from-one-sql-server-to-another-sql-server"></a>Exemplo – Streaming de um SQL Server para outro

Este exemplo demonstra como transmitir de modo assíncrono um BLOB grande de um SQL Server para outro, com suporte para cancelamento.

> [!NOTE]
> Antes de executar o exemplo a seguir, crie os bancos de dados Demo e Demo2.

[!code-csharp[SqlClient_Streaming_ServerToServer#1](~/../sqlclient/doc/samples/SqlClient_Streaming_ServerToServer.cs#1)]

## <a name="see-also"></a>Confira também

- [Recuperar e modificar dados no ADO.NET](retrieving-modifying-data.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
