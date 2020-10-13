---
description: Table Properties - SSMS
title: Tabela de propriedades – SSMS | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql13.swb.tableproperties.storage.f1
- sql13.swb.tableproperties.changetracking.f1
- sql13.swb.tableproperties.general.f1
- sql12.SWB.SELECTCOLUMNS.F1
- sql13.swb.tableproperties.filetable.f1
ms.assetid: ad8a2fd4-f092-4c0f-be85-54ce8b9d725a
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 018b1388e283541f883844daf77c68267c535a9c
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810452"
---
# <a name="table-properties---ssms"></a>Table Properties - SSMS
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa-pdw.md)]

  Este tópico descreve as propriedades de tabela que são exibidas na caixa de diálogo Propriedades da Tabela no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obter mais informações sobre como exibir essas propriedades, veja [Exibir a definição da tabela](../../relational-databases/tables/view-the-table-definition.md).  
  
 **Neste tópico**  
  
1.  [Página Geral](#GeneralPage)  
  
2.  [Página Controle de Alterações](#ChangeTracking)  
  
3.  [Página Tabela de Arquivos](#FileTable)  
  
4.  [Página Armazenamento](#Storage)  

##  <a name="general-page"></a><a name="GeneralPage"></a> Página Geral  
 **Banco de dados**  
 O nome do banco de dados que contém esta tabela.  
  
 **Servidor**  
 O nome da instância do servidor atual.  
  
 **Usuário**  
 Nome do usuário desta conexão.  
  
 **Data da Criação**  
 A data e a hora em que a tabela foi criada.  
  
 **Nome**  
 O nome da tabela.  
  
 **Esquema**  
 O esquema que possui a tabela.  
  
 **Objeto do sistema**  
 Indica que esta é uma tabela do sistema, usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conter informações internas. Os usuários não devem alterar ou fazer referência diretamente a tabelas do sistema.  
  
 **ANSI NULLs**  
 Indica se o objeto foi criado com a opção ANSI NULLs definida como ON. Para obter mais informações, veja [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)  
  
 **Identificador entre aspas**  
 Indica se o objeto foi criado com a opção de identificador entre aspas definida como ON. Para obter mais informações, veja [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
 **Escalonamento de Bloqueios**  
 Indica a granularidade do escalonamento de bloqueios da tabela. Para obter mais informações sobre bloqueio no Mecanismo de Banco de Dados, consulte [Bloqueio de transação do SQL Server e guia de controle de versão de linha](../sql-server-transaction-locking-and-row-versioning-guide.md?view=sql-server-ver15). Os valores possíveis são:  
  
 AUTO  
 Essa opção permite que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] selecione a granularidade do escalonamento de bloqueios apropriado ao esquema da tabela.  
  
- Se a tabela estiver particionada, o escalonamento de bloqueios será permitido para a granularidade HoBT (pilha ou árvore B). Em outras palavras, o escalonamento será permitido no nível da partição. Depois de ser escalonado para o nível de HoBT, o bloqueio não será escalonado posteriormente para a granularidade TABLE.
- Se a tabela não estiver particionada, o escalonamento de bloqueios será feito para a granularidade TABLE. 
  
 TABLE  
 O escalonamento de bloqueios será feito na granularidade em nível de tabela independentemente de a tabela estar particionada ou não. TABLE é o valor padrão.  
  
 DISABLE  
 Impede o escalonamento de bloqueios na maioria dos casos. Os bloqueios em nível de tabela não são totalmente desautorizados. Por exemplo, quando você está verificando uma tabela que não tem nenhum índice clusterizado no nível de isolamento serializável, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] deve usar um bloqueio de tabela para proteger a integridade dos dados.  
  
 **A tabela é replicada**  
 Indica quando a tabela é replicada em outro banco de dados usando a replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Os valores possíveis são **True** ou **False**.  
  
##  <a name="change-tracking-page"></a><a name="ChangeTracking"></a> Página Controle de Alterações  
 **Controle de alterações**  
 Indica se o controle de alterações está habilitado para a tabela. O valor padrão é **Falso**.  
  
 Essa opção só estará disponível quando o controle de alterações estiver habilitado para o banco de dados.  
  
 Para habilitar o controle de alterações, a tabela deve ter uma chave primária e é necessário ter permissão para alterar a tabela. Você também pode configurar o controle de alterações usando [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
 **Colunas de Rastreamento Atualizadas**  
 Indica se o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] rastreia as colunas que foram atualizadas.  
  
 Para obter mais informações sobre o controle de alterações, veja [Sobre o controle de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-tracking-sql-server.md).  
  
##  <a name="filetable-page"></a><a name="FileTable"></a> Página FileTable  
 Exibe as propriedades da tabela relacionada a FileTables. Para obter mais informações, veja [FileTables &#40;SQL Server&#41;](../../relational-databases/blob/filetables-sql-server.md).  
  
 **Ordenação da colunas de nome FileTable**  
 A ordenação aplicada à coluna **Name** em uma FileTable. A coluna **Name** contém nomes de arquivos e diretórios.  
  
 **Nome de diretório da FileTable**  
 A pasta raiz da FileTable.  
  
 **Namespace habilitado da FileTable**  
 Quando **True**, esse valor indica que a tabela é uma FileTable. Se você alterar esse valor para **False**, estará alterando a FileTable para uma tabela de usuário comum. Se você desejar reverter novamente a tabela para FileTable, ela precisará passar em uma verificação de consistência da FileTable para que a conversão seja bem-sucedida.  
  
##  <a name="storage-page"></a><a name="Storage"></a> Página Armazenamento  
 Exibe as propriedades relacionadas ao armazenamento da tabela selecionada.  
  
### <a name="compression"></a>Compactação  
 **Tipo de compactação**  
 O tipo de compactação da tabela. Essa propriedade está disponível somente para tabelas que não são particionadas. Para saber mais, veja [Data Compression](../../relational-databases/data-compression/data-compression.md).  
  
 **Partições que usam compactação de página**  
 Os números de partição que estão usando compactação de página. Essa propriedade está disponível somente para tabelas particionadas.  
  
 **Partições não compactadas**  
 Os números das partições que não são compactadas. Essa propriedade está disponível somente para tabelas particionadas.  
  
 **Partições que usam compactação de linha**  
 Os números das partições que estão usando compactação de linha. Essa propriedade está disponível somente para tabelas particionadas.  
  
### <a name="filegroup"></a>Grupo de arquivos  
 **Grupo de arquivos de texto**  
 O nome do grupo de arquivos que contém os dados de texto para a tabela.  
  
 **Grupo de arquivos**  
 O nome do grupo de arquivos que contém a tabela.  
  
 **Tabela é particionada**  
 Os valores possíveis são **True** e **False**.  
  
 **Grupos de Arquivos do Fluxo de Arquivos**  
 Especifique o nome do grupo de arquivos de dados FILESTREAM se a tabela tiver uma coluna **varbinary(max)** com um atributo FILESTREAM. O valor padrão é o grupo de arquivos de dados padrão FILESTREAM.  
  
 Se a tabela não contiver dados FILESTREAM, o campo ficará em branco.  
  
### <a name="general"></a>Geral  
 **O formato de armazenamento VarDecimal está habilitado**  
 Quando **True**, esse valor somente leitura indica que os tipos de dados **decimal** e **numeric** são armazenados usando o formato de armazenamento vardecimal. Para alterar essa opção, use a opção **vardecimal storage format** de [sp_tableoption](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). O formato de armazenamento vardecimal foi preterido. Em vez disso, use compactação ROW.  
  
 **Espaço do índice**  
 A quantidade de espaço em megabytes que os índices ocupam na tabela. Este valor não inclui o uso do espaço de índice XML para a tabela. Se os índices XML pertencerem à tabela, use [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) .  
  
 **Contagem de linhas**  
 O número de linhas da tabela.  
  
 **Espaço de dados**  
 A quantidade de espaço em megabytes que os dados ocupam na tabela.  
  
### <a name="partitioning"></a>Particionamento  
 Esta seção estará disponível somente se a tabela estiver particionada. Para saber mais, confira [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).  
  
 **Coluna de partição**  
 O nome da coluna na qual a tabela é particionada.  
  
 **Esquema de partição**  
 Nome do esquema de partição se a tabela estiver particionada. Se a tabela não for particionada, o campo fica em branco.  
  
 **Número of partições**  
 O número de partições da tabela.  
  
 **Esquema de partição FILESTREAM**  
 O nome do esquema de partição FILESTREAM se a tabela estiver particionada. Se a tabela não for particionada, o campo fica em branco.  
  
 O esquema de partição FILESTREAM deve ser simétrico em relação ao esquema especificado na opção **Esquema de partição** .  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir a definição da tabela](../../relational-databases/tables/view-the-table-definition.md)   
 [Modificar colunas &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/tables/modify-columns-database-engine.md)  
  
