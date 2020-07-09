---
title: Importação e exportação em massa de dados (SQL Server) | Microsoft Docs
description: O SQL Server dá suporte à exportação de dados em massa de uma tabela do SQL Server e à importação de dados em massa para uma tabela ou uma exibição não particionada do SQL Server.
ms.custom: ''
ms.date: 09/25/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- exporting data
- bulk importing [SQL Server], about bulk importing
- data [SQL Server], bulk export and import
- transferring data
- importing data, (See also bulk importing [SQL Server])
- copying data [SQL Server]
- bulk exporting [SQL Server]
- importing data, bulk import
- copying data [SQL Server], bulk export and import
- exporting data,(See also bulk exporting [SQL Server])
- bulk exporting [SQL Server], about bulk exporting
- bulk importing [SQL Server]
- importing data
ms.assetid: 19049021-c048-44a2-b38d-186d9f9e4a65
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0f90d94a11b4e026082bd3be9f25cc7ad7246df9
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86006665"
---
# <a name="bulk-import-and-export-of-data-sql-server"></a>Importação e exportação em massa de dados (SQL Server)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte à exportação de dados em massa (*dados em massa*) de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e à importação dos dados em massa para uma exibição não particionada ou uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

- *Exportação em massa* se refere à copia de dados de uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um arquivo de dados.
- *Importação em massa* refere-se ao carregamento de dados de um arquivo de dados em uma tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Por exemplo, você pode exportar dados de um aplicativo Excel do [!INCLUDE[msCoName](../../includes/msconame-md.md)] para um arquivo de dados e então importar em massa dados em uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

## <a name="methods-for-bulk-importing-and-exporting-data"></a><a name="MethodsForBuliIE"></a> Métodos para importação e exportação em massa de dados

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte à exportação de dados em massa de uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e à importação de dados em massa em uma tabela ou exibição não particionada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os métodos básicos a seguir estão disponíveis.

|Método|Descrição|Importa dados|Exporta dados|
|------------|-----------------|------------------|------------------|
|[utilitário bcp](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)|Um utilitário de linha de comando (Bcp.exe) que exporta e importa dados em massa e gera arquivos de formato.|Sim|Sim|
|[instrução BULK INSERT](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|Uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que importa dados diretamente de um arquivo de dados para uma tabela de banco de dados ou exibição não particionada.|Sim|Não|
|[Instrução INSERT ... Instrução SELECT * FROM OPENROWSET(BULK...)](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|Uma instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] que usa o provedor de conjunto de linhas em massa OPENROWSET para importação em massa dos dados para uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificando a função OPENROWSET(BULK…) para selecionar dados em uma instrução INSERT.|Sim|Não|
|[Assistente de Importação e Exportação do SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)|O assistente cria pacotes simples que importam e exportam dados entre vários formatos de dados populares, incluindo bancos de dados, planilhas e arquivos de texto.|Sim|Sim|

> [!IMPORTANT]
> Para obter as regras sobre como usar um arquivo CSV (valores separados por vírgula) como o arquivo de dados para uma importação em massa de dados para o SQL Server, confira [Preparar dados para exportação ou importação em massa (SQL Server)](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).

> [!NOTE]
> Há suporte apenas para o utilitário BCP no SQL DW do Azure para importação e exportação de arquivos delimitados.

## <a name="format-files"></a><a name="FFs"></a> Arquivos de formato

O [utilitário bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e [INSERT... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) dão suporte ao uso de um *arquivo de formato* especializado que armazena informações de formato para cada campo em um arquivo de dados. Um arquivo de formato também pode conter informações sobre a tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] correspondente. O arquivo de formato pode ser usado para fornecer todas as informações de formato necessárias para exportar e importar dados em massa para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

> [!IMPORTANT]
> Não é possível usar o BCP para importar ou exportar dados bidirecionalmente no Armazenamento de Blobs do Azure para o Banco de Dados SQL do Azure. Use [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) ou [OPENROWSET](../../t-sql/functions/openrowset-transact-sql.md) para importação ou exportação no Armazenamento de Blobs do Azure.

Os arquivos de formato fornecem um modo flexível para interpretar dados como eles são no arquivo de dados durante a importação, e também formatar dados no arquivo de dados durante a exportação. Essa flexibilidade elimina a necessidade de gravar um código com finalidade especial para interpretar os dados ou reformatar os dados segundo requisitos específicos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou o aplicativo externo. Por exemplo, se você estiver exportando dados em massa para serem carregados em um aplicativo que exige valores separados por vírgula, use um arquivo de formato para inserir vírgulas como terminadores de campo nos dados exportados.

O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a dois tipos de arquivos de formato: arquivos de formatos XML e arquivos não no formato XML.

O [utilitário bcp](../../tools/bcp-utility.md) é a única ferramenta que pode gerar um arquivo de formato. Para obter mais informações, consulte [Criar um arquivo de formato &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md). Para obter mais informações sobre os arquivos de formato, consulte [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).

> [!NOTE]
> Se um arquivo de formato não for fornecido durante uma operação de exportação ou importação em massa, você poderá substituir a formatação padrão na linha de comando.

|Tópicos Relacionados|
|---|
|[Preparar dados para exportação ou importação em massa (SQL Server)](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)|
|[Formatos de dados para importar ou exportar em massa (SQL Server)](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar o formato nativo para importar ou exportar dados (SQL Server)](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar o formato de caractere para importar ou exportar dados (SQL Server)](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar o formato nativo Unicode para importar ou exportar dados (SQL Server)](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar o formato de caractere Unicode para importar ou exportar dados (SQL Server)](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Importar dados de formato de caractere e nativos de versões anteriores do SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)|
|[Especificar formatos de dados para compatibilidade usando bcp (SQL Server)](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[Especificar tipo de armazenamento de arquivo usando bcp (SQL Server)](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[Especificar o tamanho de prefixo em arquivos de dados usando bcp (SQL Server)](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[Especificar tamanho do campo usando bcp (SQL Server)](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[Especificar terminadores de campo e linha (SQL Server)](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)|
|[Manter valores nulos ou use os valores padrão durante a importação em massa (SQL Server)](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)|
|[Manter valores de identidade ao importar dados em massa (SQL Server)](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)|
|[Arquivos de formato para importação ou exportação de dados (SQL Server)](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Criar um formato de arquivo (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar um arquivo de formato para importação em massa de dados (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar um arquivo de formato para ignorar uma coluna de tabela (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar um arquivo de formato para ignorar um campo de dados (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)<br />&emsp;&#9679;&emsp;[Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)|

## <a name="more-information"></a>Mais informações

- [Pré-requisitos para registro mínimo em log na importação em massa](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)
- [Exemplos de importação e exportação em massa de documentos XML &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)
- [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)
- [Copiar bancos de dados para outros servidores](../../relational-databases/databases/copy-databases-to-other-servers.md)
- [Como executar o carregamento em massa de dados XML &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)
- [Executando operações de cópia em massa](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)
