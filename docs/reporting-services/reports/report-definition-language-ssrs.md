---
title: Linguagem de definição de relatório | Microsoft Docs
description: Saiba mais detalhes sobre a RDL (Linguagem de Definição de Relatório). Você aprenderá que a RDL é uma declaração XML de uma definição de relatório do SQL Server Reporting Services.
ms.date: 01/24/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
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
ms.openlocfilehash: 04c220383ef14fe6bd05b690e5c27ae73b4289a4
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "79510077"
---
# <a name="report-definition-language-ssrs"></a>Linguagem RDL (SSRS)
  A linguagem RDL é uma representação XML de uma definição de relatório do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Uma definição de relatório contém informações de layout e recuperação de dados de um relatório. A linguagem RDL é composta por elementos XML que correspondem a uma gramática XML criada para o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Você pode adicionar suas próprias funções personalizadas para controlar valores de itens de relatório, estilos e formatação com o acesso a assemblies de código de arquivos de definição de relatório.  
  
 A linguagem RDL promove a interoperabilidade de produtos de relatórios comerciais definindo um esquema comum que habilita o intercâmbio de definições de relatório. Qualquer protocolo ou interface programática que funcione com o XML pode ser usada com a linguagem RDL. A linguagem RDL é:  
  
-   Um esquema XML para definições de relatório.  
  
-   Um formato de intercâmbio para negócios e terceiros.  
  
-   Um esquema extensível e aberto que dá suporte a namespaces adicionais e elementos personalizados.  
  
##  <a name="rdl-specifications"></a><a name="bkmk_RDL_Specifications"></a> Especificações de RDL  
 Para baixar as especificações de versões de esquema específicas, consulte [Especificação da linguagem RDL](https://go.microsoft.com/fwlink/?linkid=116865).  
  
##  <a name="rdl-xml-schema-definition"></a><a name="bkmk_RDL_XML_Schema_Definition"></a> Definição de esquema XML RDL  
 Um arquivo RDL (Linguagem RDL) [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é validado com o uso de um arquivo XML XSD (definição de esquema XML). O esquema define as regras para onde os elementos RDL podem ocorrer em um arquivo .rdl. Um elemento inclui seu tipo de dados e cardinalidade, isto é, o número de ocorrências que são permitidas. Um elemento pode ser simples ou complexo. Um elemento simples não tem elementos filhos ou atributos. Um elemento complexo tem filhos e, opcionalmente, atributos.  
  
 Por exemplo, o esquema inclui o elemento RDL **ReportParameters**, que é o tipo complexo **ReportParametersType**. Por convenção, um tipo complexo para um elemento é o nome do elemento seguido da palavra **Type**. Um elemento **ReportParameters** pode estar contido no elemento **Report** (um tipo complexo) e pode conter elementos **ReportParameter** . Um **ReportParameterType** é um tipo simples que só pode ter um dos seguintes valores: **Boolean**, **DateTime**, **Integer**, **Float** ou **String**. Para obter mais informações sobre os tipos de dados de Esquema XML, veja [XML Schema Part 2: Datatypes Secon Edition](https://go.microsoft.com/fwlink/?linkid=4871) (Esquema XML Parte 2: tipos de dados, segunda edição).  
  
 O RDL XSD está disponível no arquivo ReportDefinition.xsd, localizado na pasta Extras no CD-ROM do produto. Ele também está disponível no servidor de relatório por meio da seguinte URL: `https://servername/reportserver/reportdefinition.xsd`.  
  
##  <a name="creating-rdl"></a><a name="bkmk_Creating_RDL"></a> Criando RDL  
 Devido à natureza aberta e extensível da linguagem RDL, várias ferramentas e aplicativos podem ser criados para gerar a linguagem RDL com base em seu esquema XML.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornece várias ferramentas para compilar arquivos RDL. Para obter mais informações, consulte [Ferramentas do Reporting Services](../../reporting-services/tools/reporting-services-tools.md).  
  
 Uma das maneiras mais fáceis de gerar a linguagem RDL com um aplicativo é usar as classes [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] do namespace <xref:System.Xml> e do namespace <xref:System.Linq>. Uma classe específica, a classe **XmlTextWriter** , pode ser usada para gravar RDL. Com o **XmlTextWriter**, você pode gerar uma definição de relatório completa do começo ao fim em qualquer aplicativo do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] . Os desenvolvedores também podem estender a linguagem RDL adicionando itens de relatório personalizados com propriedades personalizadas. Para obter mais informações sobre a classe **XmlTextWriter** e o namespace <xref:System.Xml>, confira o Guia do Desenvolvedor do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. Para obter mais informações sobre a LINQ (Language-Integrated Query, consulta integrada à linguagem), pesquise "LINQ para XML" no MSDN.  
  
 A extensão de arquivo padrão para arquivos de definição de relatório é .rdl. Você também pode desenvolver arquivos de definição de relatório de cliente que têm as extensões .rdlc. O tipo de MIME para ambas as extensões é texto/xml. Para obter mais informações sobre feeds de dados de relatórios do SQL Server Reporting Services, consulte [Relatórios do Reporting Services &#40;SSRS&#41;](../../reporting-services/reports/reporting-services-reports-ssrs.md).  
  
##  <a name="rdl-types"></a><a name="bkmk_RDL_Types"></a> Tipos RDL  
 A tabela a seguir lista os tipos usados em elementos e atributos RDL.  
  
|Type|Descrição|  
|----------|-----------------|  
|**Binary**|Uma propriedade com um valor binário codificado na base 64.|  
|**Booliano**|Uma propriedade que define o valor do objeto como **true** ou **false** . A menos que seja especificado o contrário, o valor de um objeto Booliano opcional omitido é **False**.|  
|**Data**|Uma propriedade com data ou valor de data/hora completamente especificados no formato de data ISO8601: AAAA-MM-DD[THH:MM[:SS[.S]]].|  
|**Enum**|Uma propriedade com um valor de texto de cadeia de caracteres que deve estar na lista de valores designados.|  
|**Valor Flutuante**|Uma propriedade com um valor flutuante. O ponto (.) é usado como o separador decimal opcional.|  
|**Inteiro**|Uma propriedade com um valor inteiro (int32).|  
|**Idioma**|Uma propriedade com um valor de texto que contém linguagem e código de cultura, como "pt-br" para português do Brasil. O valor deve ser composto por uma linguagem específica ou neutra para qual a linguagem padrão possa ser definida no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].|  
|**Nome**|Uma propriedade com um valor de texto de cadeia de caracteres. Os nomes devem ser exclusivos dentro do namespace do item. Caso não seja especificado, o namespace de um item é o objeto interno que contém o nome.|  
|**NormalizedString**|Uma propriedade com um valor de texto de cadeia de caracteres que foi normalizado.|  
|**Tamanho**|Um elemento de tamanho deve conter um número (com um caractere de período usado como um separador decimal opcional). O número deve ser seguido por um designador para uma unidade de comprimento de CSS como cm, mm, in, pc ou pt. Um espaço entre o número e o designador é opcional. Para obter mais informações sobre designadores de tamanho, confira [Referência de Unidades e Valores de CSS](/previous-versions//ms537660(v=vs.85)).<br /><br /> No RDL, o valor máximo de **Size** é de 160 polegadas. O tamanho mínimo é de 0 polegada.|  
|**Cadeia de caracteres**|Uma propriedade com um valor de texto de cadeia de caracteres.|  
|**UnsignedInt**|Uma propriedade com um valor inteiro não atribuído (uint32).|  
|**Variante**|Uma propriedade com qualquer tipo de XML simples.|  
  
##  <a name="rdl-data-types"></a><a name="bkmk_RDL_Data_Types"></a> Tipos de dados RDL  
 A enumeração DataType define o tipo de dados de um atributo, expressão ou parâmetro no RDL. A tabela a seguir mostra como os tipos de dados CLR (Common Language Runtime) correspondem aos tipos de dados RDL.  
  
|**Tipo(s) CLR**|**Tipo de dados correspondente**|  
|-----------------------|---------------------------------|  
|Boolean|Boolean|  
|DateTime, DateTimeOffset|Datetime|  
|Int16, Int32, UInt16, Byte, SByte|Integer|  
|Single, Double|Float|  
|String, Char, GUID, Timespan|String|  
  
## <a name="see-also"></a>Consulte Também  
 [Localizar a versão do esquema de definição de relatório &#40;SSRS&#41;](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md)   
 [Usando assemblies personalizados com relatórios](../../reporting-services/custom-assemblies/using-custom-assemblies-with-reports.md)   
 [Itens de relatório personalizados](../../reporting-services/custom-report-items/custom-report-items.md)  
  
  
