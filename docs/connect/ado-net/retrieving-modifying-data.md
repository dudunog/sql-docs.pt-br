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
ms.openlocfilehash: 4275b7de0f31d03aa36ef31d8801fcdc0e9ec853
ms.sourcegitcommit: c938c12cf157962a5541347fcfae57588b90d929
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2020
ms.locfileid: "97771527"
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

[Transações e simultaneidade](transactions-and-concurrency.md)  
Contém os tópicos que descrevem como executar transações locais, transações distribuídas e trabalho com concorrência otimista.

[Recuperar informações de esquema de banco de dados](retrieving-database-schema-information.md)  
Descreve como obter bancos de dados ou catálogos disponíveis, tabelas e modos de exibição em um banco de dados, restrições existentes para tabelas e outras informações de esquema de uma fonte de dados.

[DbProviderFactories](dbproviderfactories.md)  
Descreve o modelo de fábrica do provedor e demonstra como usar as classes base no namespace `System.Data.Common`.  

[Recuperar valores de identidade ou numeração automática](retrieve-identity-or-autonumber-values.md)  
Fornece um exemplo de mapeamento dos valores gerados para uma coluna de **identidade** em uma tabela do SQL Server para uma coluna de uma linha inserida em uma tabela. Discute como mesclar valores de identidade em `DataTable`.  
  
[Recuperar dados binários](retrieve-binary-data.md)  
Descreve como recuperar dados binários ou grandes estruturas de dados usando o `CommandBehavior`.`SequentialAccess` para modificar o comportamento padrão de um `DataReader`.  
  
[Modificar dados com procedimentos armazenados](modify-data-with-stored-procedures.md)  
Descreve como usar parâmetros de entrada e de saída de procedimentos armazenados para inserir uma linha em um banco de dados, retornando um novo valor de identidade.  

[Rastreamento de dados no SqlClient](data-tracing.md)  
Descreve como o Provedor de Dados do Microsoft SqlClient para o SQL Server fornece a funcionalidade interna de rastreamento de dados.  
  
[Contadores de desempenho do SqlClient](performance-counters.md)  
Descreve os contadores de desempenho disponíveis para o Provedor de Dados do Microsoft SqlClient para o SQL Server.  
  
[Programação assíncrona](asynchronous-programming.md)  
Descreve o suporte à programação assíncrona do Provedor de Dados do Microsoft SqlClient do SQL Server.  
  
[Suporte a streaming no SqlClient](sqlclient-streaming-support.md)  
Explica como criar aplicativos que transmitem dados do SQL Server sem precisar carregá-los completamente na memória.  

## <a name="see-also"></a>Confira também

- [Mapeamentos de tipo de dados no ADO.NET](data-type-mappings-ado-net.md)
- [SQL Server e ADO.NET](./sql/index.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
