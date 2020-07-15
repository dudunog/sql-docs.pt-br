---
title: Esquema de FileTable | Microsoft Docs
description: Saiba mais sobre o esquema predefinido e fixo de FileTables, um recurso do SQL Server que usa uma estrutura de diretório para armazenar arquivos.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], table schema
ms.assetid: e1cb3880-cfda-40ac-91fc-d08998287f44
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 49199c617f916413e79a5c6ffc71e6c4f21a69e0
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85767972"
---
# <a name="filetable-schema"></a>Esquema da FileTable
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Descreve o esquema predefinido e fixo de uma FileTable.  
  
|Nome do atributo do arquivo|type|Tamanho|Padrão|Descrição|Acessibilidade do sistema de arquivos|  
|-------------------------|----------|----------|-------------|-----------------|-------------------------------|  
|**path_locator**|**hierarchyid**|variável|Um **hierarchyid** que identifica a posição desse item.|A posição deste nó no FileNamespace hierárquico.<br /><br /> Chave primária da tabela.|Pode ser criada e modificada por meio da definição de valores de caminho do Windows.|  
|**stream_id**|**[uniqueidentifier] rowguidcol**||Um valor retornado pela função **NEWID()** .|Uma ID exclusiva para os dados FILESTREAM.|Não aplicável.|  
|**file_stream**|**varbinary(max)**<br /><br /> **fluxo de arquivos**|variável|NULO|Contém os dados de FILESTREAM.|Não aplicável.|  
|**file_type**|**nvarchar(255)**|variável|NULL.<br /><br /> Uma operação de criação e renomeação no sistema de arquivos popula o valor da extensão do arquivo a partir do nome.|Representa o tipo do arquivo.<br /><br /> Essa coluna pode ser usada como **COLUNA DE TIPO** para criar um índice de texto completo.<br /><br /> **file_type** é uma coluna computada persistente.|Calculado automaticamente. Não pode ser definido.|  
|**Nome**|**nvarchar(255)**|variável|Valor do GUID.|O nome do arquivo ou do diretório.|Pode ser criado ou modificado por meio de APIs do Windows.|  
|**parent_path_locator**|**hierarchyid**|variável|Um **hierarchyid** que identifica o diretório que contém esse item.|O **hierarchyid** do diretório que o contém.<br /><br /> **parent_path_locator** é uma coluna computada persistente.|Calculado automaticamente. Não pode ser definido.|  
|**cached_file_size**|**bigint**|||O tamanho em bytes dos dados FILESTREAM.<br /><br /> **cached_file_size** é uma coluna computada persistente.|Embora o tamanho de arquivo armazenado em cache seja mantido atualizado automaticamente, ele pode ficar fora de sincronia em circunstâncias incomuns. Para calcular o tamanho exato, use a função **DATALENGTH()** .|  
|**creation_time**|**datetime2(4)**<br /><br /> **not null**|8 bytes|Hora atual.|A data e a hora em que o arquivo foi criado.|Calculado automaticamente. Também pode ser definido por meio de APIs do Windows.|  
|**last_write_time**|**datetime2(4)**<br /><br /> **not null**|8 bytes|Hora atual.|Data e hora em que o arquivo foi atualizado pela última vez.|Calculado automaticamente. Também pode ser definido por meio de APIs do Windows.|  
|**last_access_time**|**datetime2(4)**<br /><br /> **not null**|8 bytes|Hora atual.|Data e hora em que o arquivo foi acessado pela última vez.|Calculado automaticamente. Também pode ser definido por meio de APIs do Windows.|  
|**is_directory**|**bit**<br /><br /> **not null**|1 byte|FALSE|Indica se a linha representa um diretório. Esse valor é calculado automaticamente e não pode ser definido.|Calculado automaticamente. Não pode ser definido.|  
|**is_offline**|**bit**<br /><br /> **not null**|1 byte|FALSE|Atributo de arquivo offline.|Calculado automaticamente. Também pode ser definido por meio de APIs do Windows.|  
|**is_hidden**|**bit**<br /><br /> **not null**|1 byte|FALSE|Atributo de arquivo oculto.|Calculado automaticamente. Também pode ser definido por meio de APIs do Windows.|  
|**is_readonly**|**bit**<br /><br /> **not null**|1 byte|FALSE|Atributo de arquivo somente leitura.|Calculado automaticamente. Também pode ser definido por meio de APIs do Windows.|  
|**is_archive**|**bit**<br /><br /> **not null**|1 byte|FALSE|Atributo de arquivo morto.|Calculado automaticamente. Também pode ser definido por meio de APIs do Windows.|  
|**is_system**|**bit**<br /><br /> **not null**|1 byte|FALSE|Atributo de arquivo do sistema.|Calculado automaticamente. Também pode ser definido por meio de APIs do Windows.|  
|**is_temporary**|**bit**<br /><br /> **not null**|1 byte|FALSE|Atributo de arquivo temporário.|Calculado automaticamente. Também pode ser definido por meio de APIs do Windows.|  
  
## <a name="see-also"></a>Consulte Também  
 [Criar, alterar e remover FileTables](../../relational-databases/blob/create-alter-and-drop-filetables.md)  
  
  
