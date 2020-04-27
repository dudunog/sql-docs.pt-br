---
title: Recuperar e consultar dados XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XML data [SQL Server], retrieving
- XML instance retrieval
ms.assetid: 24a28760-1225-42b3-9c89-c9c0332d9c51
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0f556bfccdd117b23db36bb9551e885f4c38614e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63241204"
---
# <a name="retrieve-and-query-xml-data"></a>Recuperar e consultar dados XML
  Este tópico descreve as opções de consulta que você tem que especificar para consultar dados XML. Também descreve as partes de instâncias XML que não são preservadas quando são armazenadas em bancos de dados.  
  
##  <a name="features-of-an-xml-instance-that-are-not-preserved"></a><a name="features"></a> Recursos de uma Instância XML que não são preservados  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] preserva o conteúdo da instância XML, mas não preserva aspectos da instância XML que não são considerados significativos no modelo de dados XML. Isso significa que uma instância XML recuperada pode não ser idêntica à instância que foi armazenada no servidor, mas conterá as mesmas informações.  
  
### <a name="xml-declaration"></a>Declaração XML  
 A declaração XML em uma instância não é preservada quando a instância é armazenada no banco de dados. Por exemplo:  
  
```  
CREATE TABLE T1 (Col1 int primary key, Col2 xml)  
GO  
INSERT INTO T1 values (1, '<?xml version="1.0" encoding="windows-1252" ?><doc></doc>')  
GO  
SELECT Col2  
FROM T1  
```  
  
 O resultado é `<doc/>`.  
  
 A declaração XML, como `<?xml version='1.0'?>`, não é preservada ao armazenar dados XML em uma instância de tipo de dados `xml`. Isso ocorre por design. A declaração XML () e seus atributos (versão/codificação/autônoma) são perdidos depois que os dados são convertidos no `xml`tipo. A declaração XML é tratada como uma diretiva para o analisador XML. Os dados XML são armazenados internamente como ucs-2. Todos os outros PIs na instância XML são preservados.  
  
  
### <a name="order-of-attributes"></a>Ordem dos atributos  
 A ordem dos atributos em uma instância XML não é preservada. Quando você consulta a instância XML armazenada na coluna de tipo `xml`, a ordem dos atributos no XML resultante pode ser diferente da instância XML original.  
  
  
### <a name="quotation-marks-around-attribute-values"></a>Aspas em torno de valores de atributos  
 Aspas simples e aspas duplas em torno de valores de atributos não são preservadas. Os valores de atributos são armazenados no banco de dados como um nome e par de valores. As aspas não são armazenadas. Quando uma XQuery é executada em uma instância XML, o XML resultante é serializado com aspas duplas em torno dos valores dos atributos.  
  
```  
DECLARE @x xml  
-- Use double quotation marks.  
SET @x = '<root a="1" />'  
SELECT @x  
GO  
DECLARE @x xml  
-- Use single quotation marks.  
SET @x = '<root a=''1'' />'  
SELECT @x  
GO  
```  
  
 As duas consultas retornam = `<root a="1" />`.  
  
  
### <a name="namespace-prefixes"></a>Prefixos de namespace  
 Prefixos de namespace não são preservados. Quando você especifica XQuery em uma coluna de tipo `xml`, o resultado de XML serializado pode retornar prefixos de namespace diferentes.  
  
```  
DECLARE @x xml  
SET @x = '<ns1:root xmlns:ns1="abc" xmlns:ns2="abc">  
            <ns2:SomeElement/>  
          </ns1:root>'  
SELECT @x  
SELECT @x.query('/*')  
GO  
```  
  
 O prefixo de namespace no resultado pode ser diferente. Por exemplo:  
  
```  
<p1:root xmlns:p1="abc"><p1:SomeElement/></p1:root>  
```  
  
  
##  <a name="setting-required-query-options"></a><a name="query"></a> A configuração solicitou opções de consulta  
 Ao consultar colunas `xml` de tipo ou variáveis usando `xml` métodos de tipo de dados, as opções a seguir devem ser definidas como mostrado.  
  
|Opções SET|Valores necessários|  
|-----------------|---------------------|  
|ANSI_NULLS|ATIVADO|  
|ANSI_PADDING|ATIVADO|  
|ANSI_WARNINGS|ATIVADO|  
|ARITHABORT|ATIVADO|  
|CONCAT_NULL_YIELDS_NULL|ATIVADO|  
|NUMERIC_ROUNDABORT|OFF|  
|QUOTED_IDENTIFIER|ATIVADO|  
  
 Se as opções não estiverem definidas como mostrado, as consultas e modificações `xml` nos métodos de tipo de dados falharão.  
  
  
## <a name="see-also"></a>Consulte Também  
 [Criar instâncias de dados XML](create-instances-of-xml-data.md)  
  
  
