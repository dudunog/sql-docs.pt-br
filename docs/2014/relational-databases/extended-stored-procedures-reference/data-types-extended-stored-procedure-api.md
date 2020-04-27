---
title: Tipos de dados (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], data types
- data types [SQL Server], extended stored procedures
ms.assetid: 37fb86b9-8819-4387-bcdc-9616968e15ad
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 715cdc343e3a73781c06977fdb3d3d829d6bf533
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62511636"
---
# <a name="data-types-extended-stored-procedure-api"></a>Tipos de dados (API de procedimentos armazenados estendidos)
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Para usar os tipos de dados de API de procedimento armazenado estendido, inclua o arquivo de cabeçalho Srv.h em seu programa.  
  
|Tipo de dados|Tipo de dados do SQL Server|Descrição|  
|---------------|--------------------------|-----------------|  
|SRVBIGBINARY|`binary`|Tipo de dados `binary`, comprimento de 0 a 8000 bytes.|  
|SRVBIGCHAR|`char`|Tipo de dados `character`, comprimento de 0 a 8000 bytes.|  
|SRVBIGVARBINARY|`varbinary`|Tipo de dados `binary` de comprimento variável, comprimento de 0 a 8000 bytes.|  
|SRVBIGVARCHAR|`varchar`|Tipo de dados `character` de comprimento variável, comprimento de 0 a 8000 bytes.|  
|SRVBINARY|`binary`|Tipo de dados `binary`.|  
|SRVBIT|`Bit`|Tipo de dados `bit`.|  
|SRVBITN|`bit null`|Tipo de dados `bit`, valores nulos permitidos.|  
|SRVCHAR|`char`|Tipo de dados `character`.|  
|SRVDATETIME|`datetime`|Tipo de dados `datetime` de 8 bytes.|  
|SRVDATETIM4|`smalldatetime`|tipo de dados `smalldatetime` de 4 bytes.|  
|SRVDATETIMN|**datetime null**|Tipo de dados `smalldatetime` ou `datetime`, valores nulos permitidos.|  
|SRVDECIMAL|`decimal`|Tipo de dados `decimal`.|  
|SRVDECIMALN|`decimal null`|Tipo de dados `decimal`, valores nulos permitidos.|  
|SRVFLT4|`real`|tipo de dados `real` de 4 bytes.|  
|SRVFLT8|`float`|Tipo de dados `float` de 8 bytes.|  
|SRVFLTN|`real` &#124; `float null`|Tipo de dados `real` ou `float`, valores nulos permitidos.|  
|SRVIMAGE|`image`|Tipo de dados `image`.|  
|SRVINT1|`tinyint`|tipo de dados `tinyint` de 1 byte.|  
|SRVINT2|`smallint`|tipo de dados `smallint` de 2 bytes.|  
|SRVINT4|`int`|tipo de dados `int` de 4 bytes.|  
|SRVINTN|`tinyint` &#124; `smallint` &#124; `int null`|Tipo de dados `tinyint`, `smallint` ou `int`, valores nulos permitidos.|  
|SRVMONEY4|`smallmoney`|tipo de dados `smallmoney` de 4 bytes.|  
|SRVMONEY|`money`|Tipo de dados `money` de 8 bytes.|  
|SRVMONEYN|`money` &#124; `smallmoney null`|Tipo de dados `smallmoney` ou `money`, valores nulos permitidos.|  
|SRVNCHAR|**nchar**|Tipo de dados `character` Unicode.|  
|SRVNTEXT|`ntext`|Tipo de dados `text` Unicode.|  
|SRVNUMERIC|`numeric`|Tipo de dados `numeric`.|  
|SRVNUMERICN|`numeric null`|Tipo de dados `numeric`, valores nulos permitidos.|  
|SRVNVARCHAR|**nvarchar**|Tipo de dados `character` Unicode de comprimento variável.|  
|SRVTEXT|`text`|Tipo de dados `text`.|  
|SRVVARBINARY|`varbinary`|Tipo de dados `binary` de comprimento variável.|  
|SRVVARCHAR|`varchar`|Tipo de dados `character` de comprimento variável.|  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
