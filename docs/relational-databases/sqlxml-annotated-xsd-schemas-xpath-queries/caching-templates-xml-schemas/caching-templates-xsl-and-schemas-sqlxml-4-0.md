---
title: Caching de modelos, XSL e esquemas (SQLXML)
description: Exiba informações sobre como armazenar em cache modelos, XSL e esquemas no SQLXML 4,0.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, caching
- cache [SQLXML]
- memory [SQLXML]
ms.assetid: 80b4fa79-243f-442c-9f22-74ad66186501
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 96dddb725447b8dfaecb41a85489e5071459faa0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97415043"
---
# <a name="caching-templates-xsl-and-schemas-sqlxml-40"></a>Armazenando modelos, XSL e esquemas em cache (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  Para melhorar o desempenho, o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] SQLXML 4.0 dá suporte ao cache de modelos, XSL e esquemas.  
  
 Todos os esquemas, modelos e arquivos XSL (exceto os arquivos de um local https://ou ftp://) são armazenados em cache. Os arquivos armazenados em cache permanecem na memória enquanto o processo está em execução. Quando o processo é encerrado, todo o cache é perdido. Assim, se você executar um processo por consulta, talvez a vantagem do cache não seja notável.  
  
 Os tópicos nesta seção fornecem mais informações sobre o cache.  
  
## <a name="in-this-section"></a>Nesta seção  
 [Cache de modelos &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/template-caching-sqlxml-4-0.md)  
 Descreve e fornece uma chave do Registro o cache de modelos.  
  
 [Cache XSL &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/xsl-caching-sqlxml-4-0.md)  
 Descreve e fornece uma chave do Registro o cache de XSL.  
  
 [Cache de esquema &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/caching-templates-xml-schemas/schema-caching-sqlxml-4-0.md)  
 Discute problemas de instalação lado a lado do SQLXML relacionados ao cache de esquemas e fornece chaves do Registro para o cache de esquemas.  
  
  
