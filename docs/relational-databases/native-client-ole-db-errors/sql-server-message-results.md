---
title: Resultados da mensagem do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, errors
- errors [OLE DB], SQL Server message results
- OLE DB error handling, SQL Server message results
ms.assetid: 6663c6f9-def1-4d9e-845b-2085e5efc401
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9d45654e204be862ed335d688d16294526892054
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85773393"
---
# <a name="sql-server-message-results"></a>Resultados da mensagem do SQL Server
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  As instruções a seguir [!INCLUDE[tsql](../../includes/tsql-md.md)] não geram [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de linhas do provedor de OLE DB do cliente nativo ou uma contagem de linha afetada quando executadas:  
  
-   PRINT  
  
-   RAISERROR com uma severidade de 10 ou menor  
  
-   DBCC  
  
-   SET SHOWPLAN  
  
-   SET STATISTICS  
  
 Estas instruções retornam uma ou mais mensagens informativas ou fazem o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornar mensagens informativas em vez de resultados de contagens ou conjuntos de linhas. Após a execução bem-sucedida, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo retorna S_OK e as mensagens estão disponíveis para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor de OLE DB do cliente nativo.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo retorna S_OK e tem uma ou mais mensagens informativas disponíveis após a execução de muitas [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções ou a execução do consumidor de uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] função de membro do provedor de OLE DB de cliente nativo.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consumidor do provedor de OLE DB de cliente nativo que permite a especificação dinâmica do texto da consulta deve verificar as interfaces de erro depois de cada execução de função de membro, independentemente do valor do código de retorno, da presença ou da ausência de uma referência de interface **IRowset** ou **IMultipleResults** retornada ou de uma contagem de linhas afetadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Erros](../../relational-databases/native-client-ole-db-errors/errors.md)  
  
  
