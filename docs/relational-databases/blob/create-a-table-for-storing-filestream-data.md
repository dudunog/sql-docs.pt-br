---
title: Criar uma tabela para armazenar dados FILESTREAM | Microsoft Docs
description: Saiba como criar uma tabela para armazenar dados FILESTREAM no SQL Server. Veja quais colunas e atributos usar no código Transact-SQL.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], table storage
ms.assetid: 029c3059-5c83-43e2-a859-9027031b7de1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 98b1cdbda13816e0d118c170dd3b10dd4784f0d4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85768036"
---
# <a name="create-a-table-for-storing-filestream-data"></a>Criar uma tabela para armazenar dados FILESTREAM
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Este tópico mostra como criar uma tabela para armazenar dados FILESTREAM.  
  
 Quando o banco de dados tiver um grupo de arquivos FILESTREAM, será possível criar ou modificar tabelas para armazenar dados FILESTREAM. Para especificar que uma coluna contém dados FILESTREAM, crie a coluna **varbinary(max)** e adicione o atributo FILESTREAM.  
  
### <a name="to-create-a-table-to-store-filestream-data"></a>Para criar uma tabela para armazenar dados FILESTREAM  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], clique em **Nova Consulta** para exibir o Editor de Consultas.  
  
2.  Copie o código [!INCLUDE[tsql](../../includes/tsql-md.md)] do exemplo a seguir no Editor de Consultas. Este código [!INCLUDE[tsql](../../includes/tsql-md.md)] cria uma tabela habilitada para FILESTREAM chamada Registros.  
  
3.  Para criar a tabela, clique em **Executar**.  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir mostra como criar uma tabela chamada `Records`. A coluna `Id` é uma coluna `ROWGUIDCOL` exigida para usar dados de FILESTREAM com APIs de Win32. A coluna `SerialNumber` é uma coluna `UNIQUE INTEGER`. A coluna `Chart` é uma coluna `FILESTREAM` usada para armazenar `Chart` no sistema de arquivos.  
  
> [!NOTE]  
>  Este tópico requer o banco de dados Archive que foi criado em [Criar um banco de dados habilitado para FILESTREAM](../../relational-databases/blob/create-a-filestream-enabled-database.md).  
  
 [!code-sql[FILESTREAM#FS_CreateTable](../../relational-databases/blob/codesnippet/tsql/create-a-table-for-stori_1.sql)]  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
  
  
