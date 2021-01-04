---
title: Recuperar e modificar dados
description: No .NET, o Provedor de Dados Microsoft SqlClient para SQL Server serve como uma ponte entre um aplicativo e uma fonte de dados para ler e atualizar dados.
ms.date: 11/30/2020
ms.assetid: 722e7f87-3691-46c6-87e8-7d159722d675
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: c3cf3766ffc6c8acf6025b58aa0adbaafafa2188
ms.sourcegitcommit: 2add15a99df7b85d271adb261523689984dfd134
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97038954"
---
# <a name="retrieving-and-modifying-data-in-adonet"></a>Recuperar e modificar dados no ADO.NET

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

A função principal de qualquer aplicativo de banco de dados é conectar-se a uma fonte de dados e recuperar os dados que ele contém. O provedor de dados SqlClient atua como ponte entre um aplicativo e uma fonte de dados, permitindo executar comandos e recuperar dados por meio de um **DataReader** ou de um **DataAdapter**. A função principal de qualquer aplicativo de banco de dados é a capacidade de atualizar os dados que estão armazenados no banco de dados. No Provedor de Dados Microsoft SqlClient para SQL Server, a atualização de dados implica o uso dos objetos **DataAdapter**, <xref:System.Data.DataSet> e **Command**. Ela também pode envolver o uso de transações.

## <a name="in-this-section"></a>Nesta seção

[Conectar-se a fontes de dados](connecting-to-data-source.md)  
Descreve como estabelecer uma conexão com uma fonte de dados e como trabalhar com eventos de conexão.

[Cadeias de conexão](connection-strings.md)  
Contém os tópicos que descrevem os vários aspectos do uso de cadeias de conexão, incluindo palavras-chave de cadeias de conexão, informações de segurança e seu respectivo armazenamento e recuperação.

[Pool de conexões](connection-pooling.md)  
Descreve o pool de conexões para o Provedor de Dados Microsoft SqlClient para SQL Server.

[Comandos e parâmetros](commands-parameters.md)  
Contém os tópicos que descrevem como criar comandos e construtores de comandos, configurar parâmetros e executar comandos para recuperar e modificar dados.

[DataAdapters e DataReaders](dataadapters-datareaders.md)  
Contém os tópicos que descrevem DataReaders, DataAdapters, parâmetros, manipulação de eventos DataAdapter e execução de operações em lote.

[Transações e simultaneidade](transactions-and-concurrency.md) Contém tópicos que descrevem como executar transações locais, transações distribuídas e trabalhar com a simultaneidade otimista.

[Como recuperar informações de esquema de banco de dados](retrieving-database-schema-information.md) descreve como obter os bancos de dados ou os catálogos, as tabelas e as exibições disponíveis em um banco de dados, restrições existentes para tabelas e outras informações de esquema de uma fonte de dados.

## <a name="see-also"></a>Confira também

- [Mapeamentos de tipo de dados no ADO.NET](data-type-mappings-ado-net.md)
- [SQL Server e ADO.NET](./sql/index.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
