---
title: Tipos de dados (API de Procedimento Armazenado Estendido) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
helpviewer_keywords:
- extended stored procedures [SQL Server], data types
- data types [SQL Server], extended stored procedures
ms.assetid: 37fb86b9-8819-4387-bcdc-9616968e15ad
author: rothja
ms.author: jroth
ms.openlocfilehash: b510e74d507cb540fa617b6c0da48c3090429192
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85679055"
---
# <a name="data-types-extended-stored-procedure-api"></a>Tipos de dados (API de procedimentos armazenados estendidos)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Em vez disso, use a Integração CLR.  
  
 Para usar os tipos de dados de API de procedimento armazenado estendido, inclua o arquivo de cabeçalho Srv.h em seu programa.  
  
|Tipo de dados|Tipo de dados do SQL Server|Description|  
|---------------|--------------------------|-----------------|  
|SRVBIGBINARY|**binary**|Tipo de dados **binary**, com tamanho de 0 a 8.000 bytes.|  
|SRVBIGCHAR|**char**|Tipo de dados de **caractere**, com tamanho de 0 a 8.000 bytes.|  
|SRVBIGVARBINARY|**varbinary**|Tipo de dados **binary** de comprimento variável, com tamanho de 0 a 8.000 bytes.|  
|SRVBIGVARCHAR|**varchar**|Tipo de dados de **caractere** de comprimento variável, com tamanho de 0 a 8.000 bytes.|  
|SRVBINARY|**binary**|tipo de dados **Binary** .|  
|SRVBIT|**Parte**|tipo de dados **bit** .|  
|SRVBITN|**bit null**|Tipo de dados **bit**, com valores nulos permitidos.|  
|SRVCHAR|**char**|Tipo de dados de **caractere**.|  
|SRVDATETIME|**datetime**|Tipo de dados **datetime** de 8 bytes.|  
|SRVDATETIM4|**smalldatetime**|Tipo de dados **smalldatetime** de 4 bytes.|  
|SRVDATETIMN|**datetime null**|Tipo de dados **smalldatetime** ou **datetime**, com valores nulos permitidos.|  
|SRVDECIMAL|**decimal**|tipo de dados **decimal** .|  
|SRVDECIMALN|**decimal null**|Tipo de dados **decimal**, com valores nulos permitidos.|  
|SRVFLT4|**real**|Tipo de dados **real** de 4 bytes.|  
|SRVFLT8|**float**|Tipo de dados **float** de 8 bytes.|  
|SRVFLTN|**real** &#124; **float null**|Tipo de dados **real** ou **float**, com valores nulos permitidos.|  
|SRVIMAGE|**imagem**|Tipo de dados **image**.|  
|SRVINT1|**tinyint**|Tipo de dados **tinyint** de 1 byte.|  
|SRVINT2|**smallint**|Tipo de dados **smallint** de 2 bytes.|  
|SRVINT4|**int**|Tipo de dados **int** de 4 bytes.|  
|SRVINTN|**tinyint** &#124; **smallint** &#124; **int null**|Tipo de dados **tinyint**, **smallint** ou **int**, com valores nulos permitidos.|  
|SRVMONEY4|**smallmoney**|Tipo de dados **smallmoney** de 4 bytes.|  
|SRVMONEY|**money**|Tipo de dados **money** de 8 bytes.|  
|SRVMONEYN|**money** &#124; **smallmoney null**|Tipo de dados **smallmoney** ou **money**, com valores nulos permitidos.|  
|SRVNCHAR|**nchar**|Tipo de dados de **caractere** Unicode.|  
|SRVNTEXT|**ntext**|Tipo de dados **text** Unicode.|  
|SRVNUMERIC|**numeric**|Tipo de dados **numeric**.|  
|SRVNUMERICN|**numeric null**|Tipo de dados **numeric**, com valores nulos permitidos.|  
|SRVNVARCHAR|**nvarchar**|Tipo de dados de **caractere** Unicode de comprimento variável.|  
|SRVTEXT|**text**|Tipo de dados **text**.|  
|SRVVARBINARY|**varbinary**|Tipo de dados **binary** de comprimento variável.|  
|SRVVARCHAR|**varchar**|Tipo de dados de **caractere** de comprimento variável.|  
  
> [!IMPORTANT]  
>  Você deve examinar totalmente o código-fonte de procedimentos armazenados estendidos e deve testar as DLLs compiladas antes de instalá-las em um servidor de produção. Para obter informações sobre revisão e testes de segurança, consulte este [site da Microsoft](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
  
