---
title: Obter o esquema e as coleções de esquemas
description: Descreve o uso do método GetSchema para recuperar e restringir informações de esquema de um banco de dados.
ms.date: 11/26/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 113ff460017cb5fabddd4763b28294ef6f19954c
ms.sourcegitcommit: 2add15a99df7b85d271adb261523689984dfd134
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97051248"
---
# <a name="get-schema-and-schema-collections"></a>Obter o esquema e as coleções de esquemas

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

As classes **SqlConnection** no Provedor de Dados Microsoft SqlClient para SQL Server implementa um método **GetSchema** que é usado para recuperar informações de esquema sobre o banco de dados que está conectado no momento, e as informações de esquema retornadas do método **GetSchema** são fornecidas na forma de uma <xref:System.Data.DataTable>. O método **GetSchema** é um método sobrecarregado que fornece parâmetros opcionais para especificar a coleção de esquemas a ser retornada e restringir a quantidade de informações retornada.

## <a name="specifying-the-schema-collections"></a>Como especificar as coleções de esquemas

O primeiro parâmetro opcional do método **GetSchema** é o nome da coleção que é especificado como uma cadeia de caracteres. Há dois tipos de coleções de esquemas: as coleções de esquemas que são comuns a todos os provedores e as coleções de esquemas específicas de cada provedor.  

Consulte o Provedor de Dados Microsoft SqlClient para SQL Server para determinar a lista de coleções de esquemas compatíveis chamando o método **GetSchema** sem argumentos ou com o nome da coleção de esquemas "MetaDataCollections". Isso retornará uma <xref:System.Data.DataTable> com uma lista de coleções de esquemas compatíveis, o número de restrições ao qual cada uma dá suporte e o número de partes de identificador usado por elas.  

### <a name="retrieving-schema-collections-example"></a>Exemplo de recuperação de coleções de esquemas

Os seguintes exemplos demonstram como usar o método <xref:Microsoft.Data.SqlClient.SqlConnection.GetSchema%2A> da classe <xref:Microsoft.Data.SqlClient.SqlConnection> do Provedor de Dados Microsoft SqlClient para SQL Server a fim de recuperar informações de esquema sobre todas as tabelas contidas no banco de dados **AdventureWorks** de exemplo:  

[!code-csharp[SqlClient GetSchema#1](~/../sqlclient/doc/samples/SqlConnection_GetSchema_Tables.cs#1)]  

## <a name="see-also"></a>Confira também

- [Recuperar informações de esquema de banco de dados](retrieving-database-schema-information.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
