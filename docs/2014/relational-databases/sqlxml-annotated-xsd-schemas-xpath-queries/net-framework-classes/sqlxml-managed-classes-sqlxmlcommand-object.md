---
title: Objeto SqlXmlCommand (classes gerenciadas SQLXML) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- void ExecuteNonQuery() method
- namespaces property
- Stream ExecuteStream() method
- CommandType property
- RootTag property
- OutputEncoding property
- XmlReader ExecuteXmlReader() method
- Managed Classes [SQLXML], SqlXmlCommand object
- SQLXML Managed Classes, SqlXmlCommand object
- Base Path property
- void ClearParameters() method
- public void ExecuteToStream(Stream outputStream) method
- SqlXmlCommand object
- CommandText property
- XslPath property
- SchemaPath property
- SqlXmlParameter CreateParameter() method
- ClientSideXML property
- CommandStream property
ms.assetid: c1f9e0bb-a89d-4d6a-a96e-289ef516a3a6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d002208a83b58a4c8547bc6ce85db073ced70974
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66010742"
---
# <a name="sqlxmlcommand-object-sqlxml-managed-classes"></a>Objeto SqlXmlCommand (classes gerenciadas SQLXML)
  Este é o construtor para o objeto SqlXmlCommand:  
  
```  
public SqlXmlCommand(string cnString)  
```  
  
 Em `cnString` que é a cadeia de conexão ADO ou OleDb que identifica o servidor, o banco de dados e as informações de `Provider=SQLOLEDB; Server=(local); database=AdventureWorks; Integrated Security=SSPI"`logon, por exemplo,.  
  
 Na cadeia de conexão, o `Provider` precisa ser SQLOLEDB e o `Data Provider` não deve ser incluído na cadeia de caracteres do provedor.  
  
 Para obter um exemplo funcional, consulte [executando consultas SQL &#40;classes gerenciadas do SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md).  
  
## <a name="methods"></a>Métodos  
 O objeto TheSqlXmlCommand dá suporte a vários métodos, incluindo os seguintes métodos para executar um comando:  
  
 void ExecuteNonQuery ()  
 Executa o comando, mas não retorna nada. Este método será útil se você quiser executar um comando nonquery (ou seja, um comando que não retorna nada). Um exemplo é a execução de um diagrama de atualização ou um DiffGram que atualiza registros mas não retorna nada.  
  
 ExecuteStream de fluxo ()  
 Retorna um novo objeto Stream. Este método será útil quando você quiser os resultados de consulta retornados em um novo fluxo. Para obter um exemplo funcional, consulte [executando consultas SQL &#40;classes gerenciadas do SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md).  
  
 public void ExecuteToStream (Stream outputStream)  
 Escreve os resultados da consulta para um fluxo existente. Esse método é útil quando você tem um fluxo para o qual você precisa dos resultados acrescentados (por exemplo, para que os resultados da consulta sejam gravados no System. Web. HttpResponse. OutputStream). Para obter um exemplo funcional, consulte [executando consultas SQL &#40;classes gerenciadas do SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md).  
  
 XmlReader ExecuteXmlReader ()  
 Retorna um objeto XmlReader. Você pode usar esse método para manipular dados no objeto XmlReader diretamente ou conectar a arquitetura chainável do System. xml. Para obter mais informações, consulte a documentação do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework. Para obter um exemplo funcional, consulte [executando consultas SQL usando o método ExecuteXMLReader](executing-sql-queries-by-using-the-executexmlreader-method.md).  
  
 O objeto TheSqlXmlCommand também dá suporte a estes métodos adicionais:  
  
 CreateParameter SqlXmlParameter ()  
 Cria um objeto SqlXmlParameter. Você pode definir valores para os parâmetros de *nome* e *valor* deste objeto. Este método será útil se você quiser passar parâmetros para um comando. Para obter um exemplo funcional, consulte [executando consultas SQL &#40;classes gerenciadas do SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md).  
  
 void clearParameters ()  
 Desmarca o(s) parâmetro(s) que foi(ram) criado(s) para um determinado objeto de comando. Este método será útil se você quiser executar várias consultas no mesmo objeto de comando.  
  
## <a name="properties"></a>Propriedades  
 O objeto SqlXmlCommand também dá suporte a essas propriedades:  
  
 ClientSideXml  
 Quando definida como True, especifica que a conversão do conjunto de linhas em XML ocorrerá no cliente, e não no servidor. Esta propriedade será útil quando você quiser mover a carga de desempenho para a camada intermediária. A propriedade também permite envolver os procedimentos armazenados existentes com FOR XML para obter saída de XML.  
  
 SchemaPath  
 O nome do esquema de mapeamento juntamente com o caminho de diretório (por exemplo, C:\x\y\MySchema.xml). Esta propriedade será útil para especificar um esquema de mapeamento para consultas XPath. O caminho especificado pode ser absoluto ou relativo. Se o caminho for relativo, o caminho base especificado no caminho base será usado para resolver o caminho relativo. Se nenhum caminho base for especificado, o caminho relativo será relativo ao diretório atual. Para obter um exemplo funcional, consulte [acessando a funcionalidade SQLXML no ambiente .net](accessing-sqlxml-functionality-in-the-net-environment.md).  
  
 XslPath  
 O nome do arquivo XSL juntamente com o caminho de diretório. O caminho especificado pode ser absoluto ou relativo. Se o caminho for relativo, o caminho base especificado no caminho base será usado para resolver o caminho relativo. Se nenhum caminho base for especificado, o caminho relativo será relativo ao diretório atual. Para obter um exemplo funcional, consulte [aplicando um XSL Transformation &#40;classes gerenciadas SQLXML&#41;](applying-an-xsl-transformation-sqlxml-managed-classes.md).  
  
 Caminho base  
 O caminho base (um caminho de diretório). Essa propriedade é útil para resolver um caminho relativo que é especificado para um arquivo XSL (usando a propriedade XslPath), um arquivo de esquema de mapeamento (usando a propriedade SchemaPath) ou uma referência de esquema externo em um modelo XML (especificado usando o `mapping-schema` atributo).  
  
 OutputEncoding  
 Especifica a codificação para o fluxo retornado quando o comando é executado. Esta propriedade será útil para solicitar uma codificação específica para o fluxo que é retornado. Algumas codificações geralmente usadas são UTF-8, ANSI e Unicode. UTF-8 é a codificação padrão.  
  
 Namespaces  
 Habilita a execução de consultas XPath que usam namespaces. Para obter mais informações sobre consultas XPath com namespaces, consulte [executando consultas XPath com namespaces &#40;classes gerenciadas SQLXML&#41;](executing-xpath-queries-with-namespaces-sqlxml-managed-classes.md). Para obter um exemplo funcional, consulte [executando consultas XPath &#40;classes gerenciadas SQLXML&#41;](executing-xpath-queries-sqlxml-managed-classes.md).  
  
 RootTag  
 Fornece o único elemento raiz para XML gerado pela execução do comando. Um documento XML válido exige uma única marca de nível raiz. Se o comando executado gerar um fragmento XML (sem um único elemento de nível superior), você poderá especificar um elemento raiz para o XML de retorno. Para obter um exemplo funcional, consulte [aplicando um XSL Transformation &#40;classes gerenciadas SQLXML&#41;](applying-an-xsl-transformation-sqlxml-managed-classes.md).  
  
 CommandText  
 O texto do comando. Esta propriedade será usada para especificar o texto do comando que você quer executar. Para obter um exemplo funcional, consulte [executando consultas SQL &#40;classes gerenciadas do SQLXML&#41;](sqlxml-4-0-net-framework-support-managed-classes.md).  
  
 CommandStream  
 O fluxo de comando. Esta propriedade será útil se você quiser executar um comando de um arquivo (por exemplo, um modelo XML). Quando você está usando CommandStream, há suporte apenas para os valores de CommandType **"template"**, **"updategram"** e **"DiffGram"** . Para obter um exemplo funcional, consulte [executando arquivos de modelo usando a propriedade CommandStream](executing-template-files-by-using-the-commandstream-property.md).  
  
 CommandType  
 Identifica o tipo de comando. Esta propriedade será usada para especificar o tipo de comando que você quer executar. Os valores da tabela a seguir determinam o tipo do comando. Para obter um exemplo funcional, consulte [acessando a funcionalidade SQLXML no ambiente .net](accessing-sqlxml-functionality-in-the-net-environment.md).  
  
|Valor|Descrição|  
|-----------|-----------------|  
|SqlXmlCommandType. SQL|Executa um comando SQL (por exemplo, `SELECT * FROM Employees FOR XML AUTO`).|  
|SqlXmlCommandType. XPath|Executa um comando XPath (por exemplo, `Employees[@EmployeeID=1]`).|  
|SqlXmlCommandType. Template|Executa um modelo XML.|  
|SqlXmlCommandType. TemplateFile|Executa um arquivo de modelo no caminho especificado.|  
|SqlXmlCommandType. UpdateGram|Executa um diagrama de atualização.|  
|SqlXmlCommandType. DiffGram|Executa um DiffGram.|  
  
## <a name="see-also"></a>Consulte Também  
 [Objeto SqlXmlParameter &#40;classes gerenciadas SQLXML&#41;](sqlxml-managed-classes-sqlxmlparameter-object.md)   
 [Objeto SqlXmlAdapter &#40;classes gerenciadas SQLXML&#41;](sqlxml-managed-classes-sqlxmladapter-object.md)  
  
  
