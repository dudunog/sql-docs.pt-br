---
title: O elemento &lt;xsd:redefine&gt; | Microsoft Docs
description: Saiba mais sobre o suporte para o elemento redefine do W3C XSD e como atualizar um esquema XML ou seus componentes.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- xsd:redefine element
ms.assetid: 5f3e9b65-f10e-4db2-a62c-b270ac11d04e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4f2791ea8a8cae425ae7839a7af2d722e8cfe8a6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729859"
---
# <a name="the-ltxsdredefinegt-element"></a>O elemento &lt;xsd:redefine&gt;
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  O elemento **redefine** do W3C XSD fornece suporte para redefinição de componentes de esquema. No entanto, o suporte para essa diretiva é potencialmente caro para o desempenho e também exige que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] revalide todas as instâncias do tipo de dados **xml** associadas ao esquema redefinido. Portanto o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não oferece suporte a esse elemento. Esquemas XML que incluem o elemento **\<xsd:redefine>** são rejeitados pelo servidor.  
  
 Para atualizar um esquema ou seus componentes, é possível fazer o seguinte:  
  
1.  Crie uma nova coleção de esquema XML com os componentes do esquema modificado.  
  
2.  Redefina o tipo de todos os tipos de dados **xml** (XML DT) que usam a coleção de esquema XML a serem redefinidos para usarem a nova coleção de esquema XML. Para isso, use a opção ALTER COLUMN do comando ALTER TABLE para redefinir o tipo das colunas ou altere as restrições da coleção de esquema XML sobre variáveis ou parâmetros.  
  
3.  Descarte a versão antiga da coleção de esquema XML.  

## <a name="see-also"></a>Consulte Também  
 [Requisitos e limitações para o uso de Coleções de Esquemas XML no servidor](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
