---
description: GetPathLocator (Transact-SQL)
title: Função getpathlocator (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- GetPathLocator
- GetPathLocator_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- GetPathLocator function
ms.assetid: 78b7e220-445b-4fdf-811b-7253f4f2b058
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 155921b08c936bfb758f60c65b4ad737546141f5
ms.sourcegitcommit: a9e982e30e458866fcd64374e3458516182d604c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/11/2021
ms.locfileid: "98096345"
---
# <a name="getpathlocator-transact-sql"></a>GetPathLocator (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna a ID do localizador do caminho do arquivo ou diretório especificado em uma FileTable.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
GetPathLocator(filenamespace_path)  
```  
  
## <a name="arguments"></a>Argumentos  
 *filenamespace_path*  
 Um caminho de namespace na FileTable. O caminho do namespace é do tipo **nvarchar (max)**.  
  
 Quando o banco de dados pertence a um grupo de disponibilidade Always On, a função **função getpathlocator** aceita o VNN (nome da rede virtual) ou o nome do computador.  
  
## <a name="return-type"></a>Tipo de retorno  
 **hierarchyid**  
  
## <a name="general-remarks"></a>Comentários gerais  
 Para obter mais informações, consulte [Work with Directories and Paths in FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md).  
  
## <a name="examples"></a>Exemplos  
 Você pode usar a função **função getpathlocator** ao migrar arquivos de um servidor de arquivos para uma filetable. Neste cenário, você deseja mover os arquivos para a FileTable e, em seguida, substituir o caminho UNC original de cada arquivo com o caminho UNC da FileTable. Para obter um exemplo completo, consulte [carregar arquivos em Filetables](../../relational-databases/blob/load-files-into-filetables.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhar com diretórios e caminhos em FileTables](../../relational-databases/blob/work-with-directories-and-paths-in-filetables.md)  
  
  
