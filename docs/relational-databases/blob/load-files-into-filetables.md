---
title: Carregar arquivos em FileTables | Microsoft Docs
description: Descubra como carregar e migrar arquivos em FileTables no SQL Server quando os arquivos estão armazenados de várias maneiras. Leia sobre operações de carregamento em massa.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], migrating files
- FileTables [SQL Server], bulk loading
- FileTables [SQL Server], loading files
ms.assetid: dc842a10-0586-4b0f-9775-5ca0ecc761d9
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8be4fbed43f4d54fb199b687a3409337ded3ff3b
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767964"
---
# <a name="load-files-into-filetables"></a>Carregar arquivos em FileTables
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Descreve como carregar ou migrar arquivos para FileTables.  
  
##  <a name="loading-or-migrating-files-into-a-filetable"></a><a name="BasicsLoadNew"></a> Carregando ou migrando arquivos para um FileTable  
 O método que você escolhe para carregar ou migrar arquivos para uma FileTable depende em onde os arquivos estão armazenados atualmente.  
  
|Localização atual dos arquivos|Opções de migração|  
|-------------------------------|---------------------------|  
|Os arquivos estão atualmente armazenados no sistema de arquivos.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não tem conhecimento dos arquivos.|Como uma FileTable é semelhante a uma pasta no sistema de arquivos do Windows, você pode carregar arquivos com facilidade em uma nova FileTable usando qualquer um dos métodos disponíveis para mover ou copiar arquivos. Esses métodos incluem o Windows Explorer, opções de linha de comando, inclusive xcopy e robocopy, e scripts ou aplicativos personalizados.<br /><br /> Você não pode converter uma pasta existente em uma FileTable.|  
|Os arquivos estão atualmente armazenados no sistema de arquivos.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém uma tabela de metadados que possui ponteiros para os arquivos.|A primeira etapa é mover ou copiar os arquivos usando um dos métodos mencionados acima.<br /><br /> A segunda etapa é atualizar a tabela existente de metadados para apontar para o novo local dos arquivos.<br /><br /> Para obter mais informações, confira [Exemplo: migrando arquivos do sistema de arquivos para uma FileTable](#HowToMigrateFiles) neste artigo.|  
  
###  <a name="how-to-load-files-into-a-filetable"></a><a name="HowToLoadNew"></a> Como Carregar arquivos em uma nova FileTable  
Você pode usar os seguintes métodos para carregar arquivos em uma FileTable:  
  
-   Arrastar e soltar arquivos das pastas de origem para a pasta da nova FileTable no Windows Explorer.  
  
-   Usar opções de linha de comando, tais como MOVE, COPY, XCOPY ou ROBOCOPY, no prompt de comando ou em um script ou arquivo em lotes.  
  
-   Escrever um aplicativo personalizado para mover ou copiar os arquivos em C# ou no Visual Basic.NET. Chamar métodos do namespace **System.IO**.  
  
###  <a name="example-migrating-files-from-the-file-system-into-a-filetable"></a><a name="HowToMigrateFiles"></a> Exemplo: migrando arquivos do sistema de arquivos para uma FileTable  
 Neste cenário, seus arquivos são armazenados no sistema de arquivos, e você tem uma tabela de metadados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém ponteiros para os arquivos. Você deseja mover os arquivos para uma FileTable e, em seguida, substituir o caminho UNC original de cada arquivo dos metadados pelo caminho UNC da FileTable. A função [GetPathLocator & #40. O Transact-SQL e 41;](../../relational-databases/system-functions/getpathlocator-transact-sql.md) ajuda você a atingir esse objetivo.  
  
 Para este exemplo, suponha que haja uma tabela de banco de dados existente, **PhotoMetadata**, que contém dados sobre fotografias. Esta tabela tem uma coluna **UNCPath** do tipo **varchar**(512) que contém o caminho UNC real para um arquivo .jpg.  
  
 Para migrar os arquivos de imagem do sistema de arquivos para uma FileTable, você deve fazer o seguinte:  
  
1.  Crie uma nova FileTable para armazenar os arquivos. Este exemplo usa o nome de tabela **dbo.PhotoTable**, mas não mostra o código para criar a tabela.  
  
2.  Use xcopy ou uma ferramenta semelhante para copiar os arquivos .jpg, com a respectiva estrutura de diretórios, no diretório raiz da FileTable.  
  
3.  Corrija os metadados na tabela **PhotoMetadata** usando código semelhante ao seguinte exemplo:  

```sql  
--  Add a path locator column to the PhotoMetadata table.  
ALTER TABLE PhotoMetadata ADD pathlocator hierarchyid;  
  
-- Get the root path of the Photo directory on the File Server.  
DECLARE @UNCPathRoot varchar(100) = '\\RemoteShare\Photographs';  
  
-- Get the root path of the FileTable.  
DECLARE @FileTableRoot varchar(1000);  
SELECT @FileTableRoot = FileTableRootPath('dbo.PhotoTable');  
  
-- Update the PhotoMetadata table.  
  
-- Replace the File Server UNC path with the FileTable path.  
UPDATE PhotoMetadata  
    SET UNCPath = REPLACE(UNCPath, @UNCPathRoot, @FileTableRoot);  
  
-- Update the pathlocator column to contain the pathlocator IDs from the FileTable.  
UPDATE PhotoMetadata  
    SET pathlocator = GetPathLocator(UNCPath);  
```  
  
##  <a name="bulk-loading-files-into-a-filetable"></a><a name="BasicsBulkLoad"></a> Carregando arquivos em massa em uma FileTable  
 Um FileTable tem o comportamento semelhante ao de uma tabela normal para operações em massa, com as qualificações a seguir:  
  
 Uma FileTable tem restrições definidas pelo sistema que assegura que a integridade do namespace de arquivo e diretório seja mantida. Essas restrições têm de ser verificadas nos dados carregados em massa na FileTable. Algumas operações de inserção em massa permitem ignorar as restrições de tabela. Os requisitos a seguir são impostos.  
  
-   As operações de carregamento em massa que impõem restrições podem ser executadas em uma FileTable como em qualquer outra tabela. Essa categoria inclui as seguintes operações:  
  
    -   bcp com a cláusula CHECK_CONSTRAINTS.  
  
    -   BULK INSERT com a cláusula CHECK_CONSTRAINTS.  
  
    -   INSERT INTO... SELECT * FROM OPENROWSET(BULK ...) sem a cláusula IGNORE_CONSTRAINTS.  
  
-   Operações de carregamento de tamanho que não impõem restrições falham a menos que as restrições definidas pelo sistema da FileTable sejam desabilitadas. Essa categoria inclui as seguintes operações:  
  
    -   bcp sem a cláusula CHECK_CONSTRAINTS.  
  
    -   BULK INSERT sem a cláusula CHECK_CONSTRAINTS.  
  
    -   INSERT INTO... SELECT * FROM OPENROWSET(BULK ...) com a cláusula IGNORE_CONSTRAINTS.  
  
###  <a name="how-to-bulk-load-files-into-a-filetable"></a><a name="HowToBulkLoad"></a> Como Carregar arquivos em massa em uma nova FileTable  
 Você pode usar vários métodos para carregar arquivos em massa em uma FileTable:  
  
-   **bcp**  
  
    -   Chame com a cláusula **CHECK_CONSTRAINTS** .  
  
    -   Desabilite o namespace da FileTable e chame sem a cláusula **CHECK_CONSTRAINTS** . Em seguida, reabilite o namespace da FileTable.  
  
-   **BULK INSERT**  
  
    -   Chame com a cláusula **CHECK_CONSTRAINTS** .  
  
    -   Desabilite o namespace da FileTable e chame sem a cláusula **CHECK_CONSTRAINTS** . Em seguida, reabilite o namespace da FileTable.  
  
-   **INSERT INTO ... SELECT \* FROM OPENROWSET(BULK ...)**  
  
    -   Chame com a cláusula **IGNORE_CONSTRAINTS** .  
  
    -   Desabilite o namespace da FileTable e chame sem a cláusula **IGNORE_CONSTRAINTS** . Em seguida, reabilite o namespace da FileTable.  
  
 Para obter informações sobre como desabilitar as restrições de FileTable, consulte [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md).  
  
###  <a name="how-to-disable-filetable-constraints-for-bulk-loading"></a><a name="disabling"></a> Como Desabilitar restrições de FileTable para carregamento em massa  
 Para carregar os arquivos em massa em uma FileTable sem a sobrecarga de impor as restrições definidas pelo sistema, você pode desabilitar temporariamente as restrições. Para obter mais informações, consulte [Gerenciar FileTables](../../relational-databases/blob/manage-filetables.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Acessar FileTables com Transact-SQL](../../relational-databases/blob/access-filetables-with-transact-sql.md)   
 [Acessar FileTables com APIs de entrada e saída de arquivo](../../relational-databases/blob/access-filetables-with-file-input-output-apis.md)  
  
  
