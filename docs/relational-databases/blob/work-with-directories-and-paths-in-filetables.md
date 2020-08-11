---
title: Trabalhar com diretórios e caminhos em FileTables | Microsoft Docs
description: O recurso FileTables usa uma estrutura de diretório para armazenar arquivos. Saiba como trabalhar com seus diretórios, caminhos, restrições e semântica.
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], directories
ms.assetid: f1e45900-bea0-4f6f-924e-c11e1f98ab62
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 28c1d78a4def2b3549957715c754e55b0d91e743
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87246315"
---
# <a name="work-with-directories-and-paths-in-filetables"></a>Trabalhar com diretórios e caminhos em FileTables
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Descreve a estrutura de diretórios na qual os arquivos são armazenados em FileTables.  
  
##  <a name="how-to-work-with-directories-and-paths-in-filetables"></a><a name="HowToDirectories"></a> Como Trabalhar com diretórios e caminhos em FileTables  
 É possível usar as 3 funções a seguir para trabalhar com diretórios FileTable no [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
|Para obter este resultado|Use esta função|  
|------------------------|-----------------------|  
|Obtém o caminho UNC no nível raiz de uma FileTable específica ou do banco de dados atual.|[FileTableRootPath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filetablerootpath-transact-sql.md)|  
|Obtém um caminho UNC absoluto ou relativo de um arquivo ou diretório em uma FileTable.|[GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)|  
|Obtém a ID do localizador do caminho do arquivo ou diretório especificado em uma FileTable, fornecendo o caminho.|[GetPathLocator &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md)|  
  
##  <a name="how-to-use-relative-paths-for-portable-code"></a><a name="BestPracticeRelativePaths"></a> Como usar caminhos relativos para código portátil  
 Para manter código e aplicativos independentes do computador e do banco de dados atuais, evite escrever código baseado em caminhos de arquivo absolutos. Em vez disso, obtenha o caminho completo para um arquivo em tempo de execução usando as funções [FileTableRootPath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filetablerootpath-transact-sql.md) e [GetFileNamespacePath &#40;Transact-SQL&#41;](../../relational-databases/system-functions/getfilenamespacepath-transact-sql.md)juntas, conforme mostrado no exemplo a seguir. Por padrão, a função **GetFileNamespacePath** retorna o caminho relativo do arquivo sob o caminho raiz do banco de dados.  
  
```sql  
USE database_name;  
DECLARE @root nvarchar(100);  
DECLARE @fullpath nvarchar(1000);  
  
SELECT @root = FileTableRootPath();  
SELECT @fullpath = @root + file_stream.GetFileNamespacePath()  
    FROM filetable_name  
    WHERE name = N'document_name';  
  
PRINT @fullpath;  
GO  
```  
  
##  <a name="important-restrictions"></a><a name="restrictions"></a> Restrições importantes  
  
###  <a name="nesting-level"></a><a name="nesting"></a> Nível de aninhamento  
  
> **IMPORTANTE:** Você não pode armazenar mais de 15 níveis de subdiretórios no diretório FileTable. Quando você armazenar 15 níveis de subdiretórios, o nível mais baixo não poderá conter arquivos, pois esses arquivos representariam um nível adicional.  
  
###  <a name="length-of-full-path-name"></a><a name="fqnlength"></a> Comprimento do nome do caminho completo  
  
> **IMPORTANTE:** O sistema de arquivos NTFS oferece suporte a nomes do caminho maiores do que o limite de 260 caracteres do shell do Windows e da maioria das APIs do Windows. Portanto, é possível criar arquivos na hierarquia de arquivos de um FileTable usando Transact-SQL que você não poderá exibir ou abrir com o Windows Explorer ou com muitos outros aplicativos do Windows, porque o nome do caminho completo excede 260 caracteres. Entretanto, é possível continuar a acessar esses arquivos usando o Transact-SQL.  
  
##  <a name="the-full-path-to-an-item-stored-in-a-filetable"></a><a name="fullpath"></a> O caminho completo para um item armazenado em uma FileTable  
 O caminho completo para um arquivo ou diretório armazenado em uma FileTable começa com os seguintes elementos:  
  
1.  O compartilhamento habilitado para acesso de E/S de arquivos FILESTREAM no nível da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  O **DIRECTORY_NAME** especificado no nível do banco de dados.  
  
3.  O **FILETABLE_DIRECTORY** especificado no nível de FileTable.  

 A hierarquia resultante será semelhante a esta:  
  
 `\\<machine>\<instance-level FILESTREAM share>\<database-level directory>\<FileTable directory>\`  
  
 Essa hierarquia de diretórios forma a raiz de um namespace de arquivo da FileTable. Sob essa hierarquia de diretórios, os dados do FILESTREAM da FileTable são armazenados como arquivos e subdiretórios que também podem conter arquivos e subdiretórios.  
  
 É importante ter em mente que a hierarquia de diretórios criada sob o compartilhamento do FILESTREAM no nível da instância é uma hierarquia de diretórios virtuais. Essa hierarquia é armazenada no banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e não é representada fisicamente no sistema de arquivos NTFS. Todas as operações que acessam arquivos e diretórios sob o compartilhamento do FILESTREAM e nas FileTables são interceptadas e tratadas por um componente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inserido no sistema de arquivos.  
  
##  <a name="the-semantics-of-the-root-directories-at-the-instance-database-and-filetable-levels"></a><a name="roots"></a> A semântica dos diretórios raiz nos níveis de instância, banco de dados e FileTable  
 Essa hierarquia de diretórios observa a seguinte semântica:  
  
-   O compartilhamento do FILESTREAM do nível da instância é configurado por um administrador e armazenado como propriedade do servidor. Você pode renomear esse compartilhamento usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. Uma operação de renomeação não entra em vigor até que o servidor seja reiniciado.  
  
-   O nível do banco de dados **DIRECTORY_NAME** é nulo por padrão quando você cria um novo banco de dados. Um administrador pode definir ou alterar esse nome usando a instrução **ALTER DATABASE** . O nome deve ser exclusivo (em uma comparação sem diferenciação de maiúsculas e minúsculas) nessa instância.  
  
-   Normalmente, você fornece o nome **FILETABLE_DIRECTORY** como parte da instrução **CREATE TABLE** quando você cria uma FileTable. Você pode alterar esse nome usando o comando **ALTER TABLE** .  
  
-   Você não pode renomear esses diretórios raiz por operações de E/S de arquivos.  
  
-   Você não pode abrir esses diretórios raiz com identificadores de arquivo exclusivos.  
  
##  <a name="the-is_directory-column-in-the-filetable-schema"></a><a name="is_directory"></a> A coluna is_directory no esquema de FileTable  
 A tabela a seguir descreve a interação entre a coluna **is_directory** e a coluna **file_stream** que contém os dados do FILESTREAM em uma FileTable.  
  
|is_directory value|file_stream value|Comportamento|  
|-|-|-|    
|FALSE|NULO|Esta é uma combinação inválida que será capturada por uma restrição definida por sistema.|  
|FALSE|\<value>|O item representa um arquivo.|  
|TRUE|NULO|O item representa um diretório.|  
|TRUE|\<value>|Esta é uma combinação inválida que será capturada por uma restrição definida por sistema.|  
  
##  <a name="using-virtual-network-names-vnns-with-alwayson-availability-groups"></a><a name="alwayson"></a> Usando VNNs (nomes de rede virtual) com grupos de disponibilidade AlwaysOn  
 Quando o banco de dados que contém dados FILESTREAM ou FileTable pertence a um grupo de disponibilidade AlwaysOn:  
  
-   As funções FILESTREAM e FileTable aceitam ou retornam VNNs (nomes de rede virtual) em vez de nomes de computadores. Para obter mais informações sobre essas funções, veja [Funções Filestream e FileTable &#40;Transact-SQL&#41;](../../relational-databases/system-functions/filestream-and-filetable-functions-transact-sql.md).  
  
-   Todo o acesso aos dados FILESTREAM ou FileTable pelas APIs do sistema de arquivos deve usar VNNs em vez de nomes de computadores. Para obter mais informações, consulte [FILESTREAM e FileTable com Grupos de Disponibilidade AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Habilitar os pré-requisitos para FileTable](../../relational-databases/blob/enable-the-prerequisites-for-filetable.md)   
 [Criar, alterar e remover FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)   
 [Acessar FileTables com Transact-SQL](../../relational-databases/blob/access-filetables-with-transact-sql.md)   
 [Acessar FileTables com APIs de entrada e saída de arquivo](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)  
  
  
