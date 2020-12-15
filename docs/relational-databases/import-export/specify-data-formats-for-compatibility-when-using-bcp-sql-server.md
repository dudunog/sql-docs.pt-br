---
title: Especificar formatos de dados para compatibilidade com o bcp
description: Para exportações em massa no SQL Server com o bcp, os formatos de dados podem ser incompatíveis com o layout esperado. Um arquivo de formato não XML especifica os formatos de dados de compatibilidade.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk exporting [SQL Server], compatibility
- bulk importing [SQL Server], compatibility
- compatibility [SQL Server], data formats
- data formats [SQL Server], compatibility
- bcp utility [SQL Server], compatibility
ms.assetid: cd5fc8c8-eab1-4165-9468-384f31e53f0a
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.custom: seo-lt-2019
ms.openlocfilehash: c243b1f715ecf3b6196c23250c5f52836fba8ffa
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97407732"
---
# <a name="specify-compatibility-data-formats-when-using-bcp-sql-server"></a>Especificar formatos de dados para compatibilidade usando o bcp (SQL Server)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  Este tópico descreve os atributos de formato de dados, avisos específicos de campo e armazenamento de dados campo por campo em um arquivo de formato não XML do comando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**bcp** . Conhecê-los pode ser útil para exportar dados em massa do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para importação em massa para outro programa, como outro programa de banco de dados. Os formatos de dados padrão (nativo, caractere ou Unicode) na tabela de fonte poderiam ser incompatíveis com o layout de dados esperado por outro programa. Se uma incompatibilidade existir, quando você exportar os dados você deve descrever o layout dos dados.  
  
> [!NOTE]  
>  Se você não estiver familiarizado com os formatos de dados para importar ou exportar dados, veja [Formatos de dados para importação ou exportação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md).  
  
  
##  <a name="bcp-data-format-attributes"></a><a name="bcpDataFormatAttr"></a> Atributos bcp Data-Format  
 O comando **bcp** permite especificar a estrutura de cada campo em um arquivo de dados quanto aos seguintes atributos de formato de dados:  
  
-   tipo de armazenamento de arquivo  
  
     O *tipo de armazenamento de arquivo* descreve como são armazenados os dados no arquivo de dados. Dados podem ser exportados para um arquivo de dados como seu tipo de tabela de banco de dados (formato nativo), em sua representação de caractere (formato de caractere) ou como qualquer tipo de dados em que há suporte para conversão implícita; por exemplo, copiando um **smallint** como um **int**. Os tipos de dados definidos pelo usuário como tipos básicos são exportados. Para obter mais informações, veja [Especificar tipo de armazenamento de arquivo usando bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md).  
  
-   Comprimento do prefixo  
  
     Para fornecer o armazenamento de arquivos mais compacto para a exportação de dados em massa no formato nativo para um arquivo de dados, o comando **bcp** precede cada campo com um ou mais caracteres que indicam o comprimento do campo. Esses caracteres são chamados *caracteres de prefixo de comprimento*. Para obter mais informações, veja [Especificar o tamanho de prefixo em arquivos de dados usando bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md).  
  
-   Tamanho do campo  
  
     O tamanho do campo indica o número máximo de caracteres que são exigidos para representar dados em formato de caractere. O tamanho do campo já é conhecido se os dados forem armazenados no formato nativo. Para obter mais informações, veja [Especificar tamanho do campo usando bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md).  
  
-   Terminador de campo  
  
     Para campos de dados de caractere, caracteres terminadores opcionais permitem marcar o término de cada campo em um arquivo de dados (usando um *terminador de campo*) e o término de cada linha (usando um *terminador de linha*). Os caracteres terminadores são um modo de indicar aos programas de leitura o arquivo de dados onde um campo ou uma linha termina, e a outra começa. Para obter mais informações, veja [Especificar terminadores de campo e linha &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md).  
  
  
##  <a name="overview-of-the-field-specific-prompts"></a><a name="FieldSpecificPrompts"></a> Visão geral dos prompts de campo específicos  
 Se um comando **bcp** interativo contiver a opção **in** ou **out** , mas também não contiver a opção de arquivo de formato ( **-f**) ou uma opção de formato de dados ( **-n**, **-c**, **-w** ou **-N**), cada coluna na tabela de destino ou origem, o comando solicitará cada um dos atributos precedentes, por vez. Em cada prompt, o comando **bcp** fornece um valor padrão baseado no tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da coluna de tabela. Aceitar o valor padrão de todos os prompts gera o mesmo resultado de especificar o formato nativo ( **-n**) na linha de comando. Cada prompt exibe um valor padrão entre colchetes: [*default*]. Pressionando ENTER aceita o padrão exibido. Para especificar um valor diferente do padrão, insira o valor novo no prompt.  
  
### <a name="example"></a>Exemplo  
 Os exemplos a seguir usam o comando **bcp** para exportar em massa dados da tabela `HumanResources.myTeam` para o arquivo `myTeam.txt` interativamente. Antes de executar o exemplo, é necessário criar essa tabela. Para obter informações sobre a tabela e como criá-la, veja [Tabela de exemplo HumanResources.myTeam &#40;SQL Server&#41;](../../relational-databases/import-export/humanresources-myteam-sample-table-sql-server.md).  
  
 O comando não especifica nem um arquivo de formato nem um tipo de dados, fazendo com que o **bcp** solicite informações de formato de dados. No prompt de comando do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, digite:  
  
```cmd
bcp AdventureWorks.HumanResources.myTeam out myTeam.txt -T  
```  
  
 Para cada coluna, o bcp solicita os valores de campo específicos. O exemplo seguinte mostra os prompts de campo especifico para as colunas `EmployeeID` e `Name` da tabela e sugere o tipo de armazenamento de arquivo padrão (o formato nativo) para cada coluna. Os comprimentos dos prefixos do `EmployeeID` e coluna `Name` são 0 e 2, respectivamente. O usuário especifica uma vírgula (`,`) como terminador de cada campo.  
  
 `Enter the file storage type of field EmployeeID [smallint]:`  
  
 `Enter prefix-length of field EmployeeID [0]:`  
  
 `Enter field terminator [none]:,`  
  
 `Enter the file storage type of field Name [nvarchar]:`  
  
 `Enter prefix length of field Name [2]:`  
  
 `Enter field terminator [none]:,`  
  
 `.`  
  
 `.`  
  
 `.`  
  
 São exibidos prompts equivalentes (quando necessário) para cada uma das colunas de tabela em ordem.  
  
  
##  <a name="storing-field-by-field-data-in-a-non-xml-format-file"></a><a name="FieldByFieldNonXmlFF"></a> Armazenando dados campo por campo em um arquivo de formato não XML  
 Após todas as colunas de tabela serem especificadas, o comando **bcp** solicita que você gere um arquivo de formato não XML que armazena a informações campo por campo fornecidas (veja o exemplo anterior) opcionalmente. Se você escolher gerar um arquivo de formato, você poderá sempre que exportar dados fora daquela tabela ou importar dados estruturados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Você pode usar o arquivo de formato para importação em massa de um arquivo de dados em uma instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para exportar dados em massa da tabela sem precisar especificar o formato. Para obter mais informações, consulte [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
 O exemplo a seguir cria um arquivo de formato nomeado não XML `myFormatFile.fmt`:  
  
 `Do you want to save this format information in a file? [Y/n] y`  
  
 `Host filename: [bcp.fmt]myFormatFile.fmt`  
  
 O nome padrão para o arquivo de formato é bcp.fmt, mas você poderá especificar um nome de arquivo diferente se você preferir.  
  
> [!NOTE]  
>  Para um arquivo de dados que usa um único formato de dados para seu tipo de armazenamento de arquivos, como caractere ou formato nativo, você pode criar um arquivo de formato rapidamente sem exportar ou importar dados usando a opção **format** . Esta abordagem tem a vantagem de ser fácil e de lhe permitir criar um arquivo formato XML ou um não XML. Para obter mais informações, consulte [Criar um arquivo de formato &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md).  
  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Especificar tipo de armazenamento de arquivo usando bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)  
  
-   [Especificar o tamanho de prefixo em arquivos de dados usando bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
-   [Especificar tamanho do campo usando bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)  
  
-   [Especificar terminadores de campo e linha &#40;SQL Server&#41;](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
 Nenhum.  
  
## <a name="see-also"></a>Consulte Também  
 [Importação e exportação em massa de dados &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [Formatos de dados para importação ou exportação em massa &#40;SQL Server&#41;](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)   
 [Utilitário bcp](../../tools/bcp-utility.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
  
