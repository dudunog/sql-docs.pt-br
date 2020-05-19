---
title: Suporte ao conjunto de linhas de esquema (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- schema rowsets [OLE DB]
- OLE DB, schema rowsets
- OLE DB rowsets, schema
- SQL Server Native Client OLE DB provider, schema rowsets
- rowsets [OLE DB], schema
ms.assetid: a75b4b69-b095-4690-9b31-a2b32a67489e
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9624749eff8b455c7071d395ec91c96aeae9d32a
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82704239"
---
# <a name="schema-rowset-support-ole-db"></a>Suporte a conjunto de linhas de esquema (OLE DB)
  O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo também dá suporte ao retorno de informações de esquema de um servidor vinculado ao processar [!INCLUDE[tsql](../../../includes/tsql-md.md)] consultas distribuídas.  
  
> [!NOTE]  
>  Apesar de o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] suportar sinônimos, metadados para sinônimos não são retornados pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
 As tabelas a seguir listam conjuntos de linhas de esquema e as colunas de restrição com suporte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo.  
  
|Conjunto de linhas de esquema|Colunas de restrição|  
|-------------------|-------------------------|  
|DBSCHEMA_CATALOGS|CATALOG_NAME|  
|DBSCHEMA_COLUMN_PRIVILEGES|Todas as restrições são suportadas.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME GRANTOR GRANTEE|  
|DBSCHEMA_COLUMNS|Todas as restrições são suportadas.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME COLUMN_NAME<br /><br /> As colunas adicionais a seguir são específicas ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]:<br /><br /> -COLUMN_LCID, que é a ID de localidade do agrupamento. COLUMN_LCID tem o mesmo valor de um LCID do Windows.<br />-COLUMN_COMPFLAGS define quais comparações têm suporte para o agrupamento. O formato de dados é o mesmo do DBPROB_FINDCOMPAREOPS.<br />-COLUMN_SORTID, que é o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] estilo de classificação para o agrupamento.<br />-COLUMN_TDSCOLLATION, que é o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] agrupamento para a coluna.<br />-IS_COMPUTED, que será VARIANT_TRUE se a coluna for uma coluna computada e VARIANT_FALSE caso contrário.|  
|DBSCHEMA_FOREIGN_KEYS|Há suporte para todas as restrições.<br /><br /> PK_TABLE_CATALOG PK_TABLE_SCHEMA PK_TABLE_NAME FK_TABLE_CATALOG FK_TABLE_SCHEMA FK_TABLE_NAME|  
|DBSCHEMA_INDEXES|As restrições 1, 2, 3 e 5 são suportadas.<br /><br /> TABLE_CATALOG TABLE_SCHEMA INDEX_NAME TABLE_NAME|  
|DBSCHEMA_PRIMARY_KEYS|Há suporte para todas as restrições.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|DBSCHEMA_PROCEDURE_PARAMETERS|Há suporte para todas as restrições.<br /><br /> PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME PARAMETER_NAME|  
|DBSCHEMA_PROCEDURES|As restrições 1, 2 e 3 são suportadas.<br /><br /> PROCEDURE_CATALOG PROCEDURE_SCHEMA PROCEDURE_NAME<br /><br /> DBSCHEMA_PROCEDURES só retorna procedimentos que podem ser executados pelo usuário atual, ou para os quais o usuário atual obteve permissão de VIEW DEFINITION.|  
|DBSCHEMA_PROVIDER_TYPES|Há suporte para todas as restrições.<br /><br /> DATA_TYPE BEST_MATCH|  
|DBSCHEMA_SCHEMATA|Há suporte para todas as restrições.<br /><br /> CATALOG_NAME SCHEMA_NAME SCHEMA_OWNER|  
|DBSCHEMA_STATISTICS|Há suporte para todas as restrições.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME|  
|DBSCHEMA_TABLE_CONSTRAINTS|Há suporte para todas as restrições.<br /><br /> CONSTRAINT_CATALOG CONSTRAINT_SCHEMA CONSTRAINT_NAME TABLE_CATALOG TABLE_SCHEMA TABLE_NAME CONSTRAINT_TYPE|  
|DBSCHEMA_TABLE_PRIVILEGES|Há suporte para todas as restrições.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME GRANTOR GRANTEE|  
|DBSCHEMA_TABLES|Há suporte para todas as restrições.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
|DBSCHEMA_TABLES_INFO|Há suporte para todas as restrições.<br /><br /> TABLE_CATALOG TABLE_SCHEMA TABLE_NAME TABLE_TYPE|  
  
## <a name="in-this-section"></a>Nesta seção  
 [Suporte à consulta distribuída no conjunto de linhas do esquema](schema-rowsets-distributed-query-support.md)  
  
 [Conjunto de linhas LINKEDSERVERS &#40;OLE DB&#41;](schema-rowsets-linkedservers-rowset.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;OLE DB&#41;](sql-server-native-client-ole-db.md)   
 [Usando tipos definidos pelo usuário](../features/using-user-defined-types.md)  
  
  
