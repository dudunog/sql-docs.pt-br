---
title: FILEPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FILEPROPERTY_TSQL
- FILEPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- viewing file properties
- names [SQL Server], files
- displaying file properties
- file properties [SQL Server]
- FILEPROPERTY function
- file names [SQL Server], FILEPROPERTY
ms.assetid: b82244ed-d623-431f-aa06-8017349d847f
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 1b0c31675c5fe97d8ac1feacde12e812a6e77321
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826960"
---
# <a name="fileproperty-transact-sql"></a>FILEPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o valor de propriedade de nome de arquivo especificado quando são especificados um nome de arquivo no banco de dados atual e um nome de propriedade. Retorna NULL para arquivos que não estão no banco de dados atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
FILEPROPERTY ( file_name , property )  
```  
  
## <a name="arguments"></a>Argumentos  
 *file_name*  
 É uma expressão que contém o nome do arquivo associado ao banco de dados atual para o qual retornar as informações de propriedade. *file_name* é **nchar(128)** .  
  
 *property*  
 É uma expressão que contém o nome da propriedade do arquivo a ser retornada. *property* é **varchar(128)** e pode ser um dos valores a seguir.  
  
|Valor|DESCRIÇÃO|Valor retornado|  
|-----------|-----------------|--------------------|  
|**IsReadOnly**|O grupo de arquivos é somente leitura.|1 = True<br /><br /> 0 = False<br /><br /> NULL = A entrada não é válida.|  
|**IsPrimaryFile**|Arquivo é o arquivo primário.|1 = True<br /><br /> 0 = False<br /><br /> NULL = A entrada não é válida.|  
|**IsLogFile**|Arquivo é um arquivo de log.|1 = True<br /><br /> 0 = False<br /><br /> NULL = A entrada não é válida.|  
|**SpaceUsed**|Quantidade de espaço usado pelo arquivo especificado.|Número de páginas alocadas no arquivo|  
  
## <a name="return-types"></a>Tipos de retorno  
 **int**  
  
## <a name="remarks"></a>Comentários  
 *file_name* corresponde à coluna **name** da exibição do catálogo **sys.master_files** ou **sys.database_files**.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna a configuração para a propriedade `IsPrimaryFile` para o nome de arquivo `AdventureWorks_Data` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
  
SELECT FILEPROPERTY('AdventureWorks2012_Data', 'IsPrimaryFile')AS [Primary File];  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Primary File   
-------------  
1  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>Consulte Também  
 [FILEGROUPPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/filegroupproperty-transact-sql.md)   
 [Funções de metadados &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sp_spaceused &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
