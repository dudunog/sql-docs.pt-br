---
title: XML (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- xml_TSQL
- xml
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], about xml data type
ms.assetid: 9198f671-8e61-4ca4-9c3a-859f84020e62
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 66e49e14785f3e99bde79c1de987ea5ac38d06d2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85754790"
---
# <a name="xml-transact-sql"></a>xml (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  É o tipo de dados que armazena dados XML. É possível armazenar instâncias de **XML** em uma coluna ou em uma variável do tipo **XML**.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
xml ( [ CONTENT | DOCUMENT ] xml_schema_collection )  
```  
  
## <a name="arguments"></a>Argumentos  
 CONTENT  
 Restringe a instância de **XML** a ser um fragmento XML bem formado. Os dados XML podem conter vários zeros ou mais elementos no nível superior. Também são permitidos nós de texto no nível superior.  
  
 Esse é o comportamento padrão.  
  
 DOCUMENT  
 Restringe a instância de **XML** a ser um documento XML bem formado. Os dados XML devem ter um, e somente um, elemento raiz. Nós de texto não são permitidos no nível superior.  
  
 *xml_schema_collection*  
 É o nome de uma coleção de esquema XML. Para criar uma coluna ou variável **XML** tipada, opcionalmente, é possível especificar o nome da coleção de esquemas XML. Para obter mais informações sobre XML tipado e não tipado, confira [Comparar XML tipado com XML não tipado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
## <a name="remarks"></a>Comentários  
 A representação armazenada de instâncias do tipo de dados **XML** não pode exceder 2 gigabytes (GB) de tamanho.  
  
 As facetas CONTENT e DOCUMENT se aplicam apenas a XML com tipo. Para obter mais informações, confira [Comparar XML tipado com XML não tipado](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md).  
  
## <a name="examples"></a>Exemplos  
  
```  
USE AdventureWorks;  
GO  
DECLARE @DemographicData xml (Person.IndividualSurveySchemaCollection);  
SET @DemographicData =  (SELECT TOP 1 Demographics FROM Person.Person);  
SELECT @DemographicData;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Conversão de tipo de dados &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Métodos de tipos de dados xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  
