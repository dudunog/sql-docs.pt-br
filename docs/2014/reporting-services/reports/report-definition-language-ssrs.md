---
title: Linguagem RDL (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Reporting Services, RDL
- Reporting Services, RDL
- RDL [Reporting Services], about Report Definition Language
- SSRS, RDL
- Report Definition Language, about Report Definition Language
- Report Definition Language
- RDL [Reporting Services]
- reports [Reporting Services], definitions
ms.assetid: b18b025e-f4bd-4744-8f86-0ac9fb967548
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 6480a8cefee9b71149c61bf952896a739526cf55
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66102503"
---
# <a name="report-definition-language-ssrs"></a>Linguagem RDL (SSRS)
  O RDL (linguagem de definição de relatório) é uma representação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] XML de uma definição de relatório. Uma definição de relatório contém informações de layout e recuperação de dados de um relatório. A linguagem RDL é composta por elementos XML que correspondem a uma gramática XML criada para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Você pode adicionar suas próprias funções personalizadas para controlar valores de itens de relatório, estilos e formatação com o acesso a assemblies de código de arquivos de definição de relatório.  
  
 A linguagem RDL promove a interoperabilidade de produtos de relatórios comerciais definindo um esquema comum que habilita o intercâmbio de definições de relatório. Qualquer protocolo ou interface programática que funcione com o XML pode ser usada com a linguagem RDL. A linguagem RDL é:  
  
-   Um esquema XML para definições de relatório.  
  
-   Um formato de intercâmbio para negócios e terceiros.  
  
-   Um esquema extensível e aberto que dá suporte a namespaces adicionais e elementos personalizados.  
  
##  <a name="rdl-specifications"></a><a name="bkmk_RDL_Specifications"></a>Especificações de RDL  
 Para baixar as especificações de versões de esquema específicas, consulte [Especificação da linguagem RDL](https://go.microsoft.com/fwlink/?linkid=116865).  
  
##  <a name="rdl-xml-schema-definition"></a><a name="bkmk_RDL_XML_Schema_Definition"></a>Definição de esquema XML RDL  
 Um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] arquivo RDL (linguagem de definição de relatório) é validado usando um arquivo de definição de esquema XML (XSD). O esquema define as regras para onde os elementos RDL podem ocorrer em um arquivo .rdl. Um elemento inclui seu tipo de dados e cardinalidade, isto é, o número de ocorrências que são permitidas. Um elemento pode ser simples ou complexo. Um elemento simples não tem elementos filhos ou atributos. Um elemento complexo tem filhos e, opcionalmente, atributos.  
  
 Por exemplo, o esquema inclui o elemento RDL `ReportParameters`, que é o tipo complexo `ReportParametersType`. Por convenção, um tipo complexo para um elemento é o nome do elemento seguido da palavra `Type`. Um elemento `ReportParameters` pode ser contido pelo elemento `Report` (um tipo complexo) e pode conter elementos `ReportParameter`. Um `ReportParameterType` é um tipo simples que pode ser somente um dos seguintes valores: `Boolean`, `DateTime`, `Integer`, `Float` ou `String`. Para obter mais informações sobre os tipos de dados de Esquema XML, consulte [XML Schema Part 2: Datatypes Second Edition](https://go.microsoft.com/fwlink/?linkid=4871)(em inglês).  
  
 O RDL XSD está disponível no arquivo ReportDefinition.xsd, localizado na pasta Extras no CD-ROM do produto. Ele também está disponível no servidor de relatório por meio da seguinte URL: http://servername/reportserver/reportdefinition.xsd.  
  
##  <a name="creating-rdl"></a><a name="bkmk_Creating_RDL"></a>Criando RDL  
 Devido à natureza aberta e extensível da linguagem RDL, várias ferramentas e aplicativos podem ser criados para gerar a linguagem RDL com base em seu esquema XML.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece várias ferramentas para compilar arquivos RDL. Para obter mais informações, consulte [Ferramentas do Reporting Services](../tools/reporting-services-tools.md).  
  
 Uma das maneiras mais fáceis de gerar o RDL a partir de um aplicativo é usar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] as classes do <xref:System.Xml> namespace e <xref:System.Linq> do namespace. Uma classe específica, a classe **XmlTextWriter** , pode ser usada para gravar RDL. Com o **XmlTextWriter**, você pode gerar uma definição de relatório completa do começo ao fim em qualquer aplicativo do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] . Os desenvolvedores também podem estender a linguagem RDL adicionando itens de relatório personalizados com propriedades personalizadas. Para obter mais informações sobre a classe **XmlTextWriter** e o namespace <xref:System.Xml>, confira o Guia do Desenvolvedor do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Para obter mais informações sobre a LINQ (Language-Integrated Query, consulta integrada à linguagem), pesquise "LINQ para XML" no MSDN.  
  
 A extensão de arquivo padrão para arquivos de definição de relatório é .rdl. Você também pode desenvolver arquivos de definição de relatório de cliente que têm as extensões .rdlc. O tipo de MIME para ambas as extensões é texto/xml. Para obter mais informações sobre feeds de dados de relatórios do SQL Server Reporting Services, consulte [Relatórios do Reporting Services &#40;SSRS&#41;](reporting-services-reports-ssrs.md).  
  
##  <a name="rdl-types"></a><a name="bkmk_RDL_Types"></a>Tipos RDL  
 A tabela a seguir lista os tipos usados em elementos e atributos RDL.  
  
|Tipo|Descrição|  
|----------|-----------------|  
|`Binary`|Uma propriedade com um valor binário codificado na base 64.|  
|`Boolean`|Uma propriedade que define o valor do objeto como `true` ou `false`. A menos que seja especificado o contrário, o valor de um objeto Booliano opcional omitido é `False`.|  
|`Date`|Uma propriedade com data ou valor de data/hora completamente especificados no formato de data ISO8601: YYYY-MM-DD[THH:MM[:SS[.S]]].|  
|`Enum`|Uma propriedade com um valor de texto de cadeia de caracteres que deve estar na lista de valores designados.|  
|`Float`|Uma propriedade com um valor flutuante. O ponto (.) é usado como o separador decimal opcional.|  
|`Integer`|Uma propriedade com um valor inteiro (int32).|  
|`Language`|Uma propriedade com um valor de texto que contém linguagem e código de cultura, como "pt-br" para português do Brasil. O valor deve ser um idioma específico ou um idioma neutro para o qual um idioma padrão seja definido no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].|  
|`Name`|Uma propriedade com um valor de texto de cadeia de caracteres. Os nomes devem ser exclusivos dentro do namespace do item. Caso não seja especificado, o namespace de um item é o objeto interno que contém o nome.|  
|`NormalizedString`|Uma propriedade com um valor de texto de cadeia de caracteres que foi normalizado.|  
|`Size`|Um elemento de tamanho deve conter um número (com um caractere de período usado como um separador decimal opcional). O número deve ser seguido por um designador para uma unidade de comprimento de CSS como cm, mm, in, pc ou pt. Um espaço entre o número e o designador é opcional. Para obter mais informações sobre designadores de tamanho, consulte [Referência de Unidades de Comprimento de CSS](https://www.w3schools.com/CSSref/css_units.asp).<br /><br /> No RDL, o valor máximo de `Size` é de 160 polegadas. O tamanho mínimo é de 0 polegada.|  
|`String`|Uma propriedade com um valor de texto de cadeia de caracteres.|  
|`UnsignedInt`|Uma propriedade com um valor inteiro não atribuído (uint32).|  
|`Variant`|Uma propriedade com qualquer tipo de XML simples.|  
  
##  <a name="rdl-data-types"></a><a name="bkmk_RDL_Data_Types"></a>Tipos de dados RDL  
 A enumeração DataType define o tipo de dados de um atributo, expressão ou parâmetro no RDL. A tabela a seguir mostra como os tipos de dados CLR (Common Language Runtime) correspondem aos tipos de dados RDL.  
  
|**Tipo(s) CLR**|**Tipo de dados correspondente**|  
|-----------------------|---------------------------------|  
|Boolean|Boolean|  
|DateTime, DateTimeOffset|Datetime|  
|Int16, Int32, UInt16, Byte, SByte|Integer|  
|Single, Double|Float|  
|String, Char, GUID, Timespan|String|  
  
## <a name="see-also"></a>Consulte Também  
 [Localize a versão do esquema de definição de relatório &#40;SSRS&#41;](find-the-report-definition-schema-version-ssrs.md)   
 [Usando assemblies personalizados com relatórios](../custom-assemblies/using-custom-assemblies-with-reports.md)   
 [Itens de Relatório Personalizados](../custom-report-items/custom-report-items.md)  
  
  
