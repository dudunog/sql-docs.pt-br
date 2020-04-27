---
title: Introdução ao provedor SQLXMLOLEDB (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXMLOLEDB Provider, properties
- adExecuteStream flag
- SQLXMLOLEDB Provider, about SQLXMLOLEDB Provider
ms.assetid: 2e3f3817-4209-4bf4-9f46-248c95bc6f1b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9826143c68b8c1bd3edc6472156d140a6141968b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66014383"
---
# <a name="introduction-to-the-sqlxmloledb-provider-sqlxml-40"></a>Introdução ao provedor SQLXMLOLEDB (SQLXML 4.0)
  O provedor SQLXMLOLEDB é um provedor OLE DB que expõe a funcionalidade SQLXML [!INCLUDE[msCoName](../../../includes/msconame-md.md)] através do ADO (ActiveX Data Objects). No entanto, o provedor só pode executar comandos no modo "write to an output stream" do ADO. SQLXMLOLEDB não é um provedor de conjunto de linhas. Ao executar um comando, você deve especificar o sinalizador adExecuteStream, que direciona o ADO para usar o fluxo de saída que você especificou.  
  
 O exemplo a seguir mostra a sintaxe para o comando execute no qual o sinalizador adExecuteStream é especificado:  
  
```  
Dim oTestCommand As New ADODB.Command  
...  
oTestCommand.Properties("Output Stream").Value = oTestStream  
oTestCommand.Execute , , adExecuteStream  
...  
```  
  
## <a name="sqlxmloledb-provider-specific-properties"></a>Propriedades específicas do provedor SQLXMLOLEDB  
 O provedor SQLXMLOLEDB expõe a seguinte propriedade de conexão específica do provedor:  
  
|Conexão<br /><br /> propriedade|Padrão<br /><br /> (se houver)|Descrição|  
|-----------------------------|----------------------------|-----------------|  
|Provedor de Dados||Fornece o PROGID do provedor OLE DB através do qual o SQLXMLOLEDB executa os comandos. A partir do SQLXML 4.0 e do [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], este provedor passou a fazer parte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, portanto, o valor dessa propriedade se restringe a "SQLNCLI11". Para obter mais informações, consulte [Programação do SQL Server Native Client](../../native-client/sql-server-native-client-programming.md).|  
  
 O provedor SQLXMLOLEDB expõe as seguintes propriedades de comando específicas do provedor:  
  
|Comando<br /><br /> propriedade|Padrão<br /><br /> (se houver)|Descrição|  
|--------------------------|----------------------------|-----------------|  
|Caminho base|""|Especifica o caminho do arquivo de base. O caminho do arquivo de base é usado para indicar o local dos arquivos de esquema de mapeamento ou XSL (Stylesheet Language) XML. O caminho do arquivo base também é usado para resolver os caminhos relativos de arquivos de esquema XSL ou de mapeamento que foram especificados nas propriedades do esquema XSL ou Mapping.<br /><br /> Para obter um exemplo em que essa propriedade é usada, consulte [executando consultas XPath &#40;provedor de SQLXMLOLEDB&#41;](executing-xpath-queries-sqlxmloledb-provider.md).|  
|ClientSideXML|Falso|Defina esta propriedade como True se quiser que o processo de conversão do conjunto de linhas em XML ocorra no cliente, e não no servidor. Isso é útil quando você deseja mover a carga de desempenho para a camada intermediária.<br /><br /> Para obter um exemplo em que essa propriedade é usada, consulte [executando consultas sql &#40;provedor SQLXMLOLEDB&#41;](executing-sql-queries-sqlxmloledb-provider.md) ou [executando modelos que contêm consultas SQL &#40;provedor de SQLXMLOLEDB&#41;](executing-templates-that-contain-sql-queries-sqlxmloledb-provider.md).|  
|Tipo de conteúdo||Retorna o tipo de conteúdo de saída. Esta é uma propriedade SOMENTE LEITURA.<br /><br /> Esta propriedade fornece informações ao navegador sobre o tipo de conteúdo (como TEXT/XML, TEXT/HTML, imagem/jpeg, e assim por diante). O valor dessa propriedade torna-se o campo **Content-Type** enviado ao navegador como parte do cabeçalho HTTP, que contém o tipo MIME (Multipurpose Internet Mail Extensions) do documento que está sendo enviado como o corpo.|  
|Esquema de mapeamento|NULO|Se um aplicativo cliente executar uma consulta XPath em um esquema de mapeamento (XDR ou XSD), esta propriedade será usada para especificar o nome do esquema de mapeamento.<br /><br /> O caminho especificado pode ser relativo (xyz/abc/MySchema.xml) ou absoluto (C:\MyFolder\abc\MySchema.xml).<br /><br /> Se um caminho relativo for especificado, o caminho base especificado pela propriedade caminho base será usado para resolver o caminho relativo. Se nenhum caminho tiver sido especificado na propriedade caminho base, o caminho relativo será relativo ao diretório atual.<br /><br /> Ao especificar um valor para a propriedade esquema de mapeamento, você pode especificar um caminho de diretório local ou uma URL (http://...). Se você especificar uma URL, deverá configurar o WinHTTP para acessar servidores HTTP e HTTPS por meio de um servidor proxy. Para isso, use o utilitário Proxycfg.exe. Para obter mais informações, consulte "Usando o Utilitário de Configuração do WinHTTP Proxy" na Biblioteca MSDN.<br /><br /> Para obter um exemplo em que essa propriedade é usada, consulte [executando consultas XPath &#40;provedor de SQLXMLOLEDB&#41;](executing-xpath-queries-sqlxmloledb-provider.md).|  
|namespaces||Esta propriedade permite a execução de consultas XPath que usam namespaces. Para obter um exemplo em que essa propriedade é usada, consulte [executando consultas XPath com namespaces &#40;provedor SQLXMLOLEDB&#41;](executing-xpath-queries-with-namespaces-sqlxmloledb-provider.md).|  
|ss Stream Flags||Esta propriedade é usada para definir tipos específicos de restrições de segurança. Por exemplo, talvez você não queira permitir referências URL a arquivos ou caminhos absolutos para arquivos (como sites externos). Ou você pode optar por não permitir consultas nos modelos.<br /><br /> É possível atribuir estes valores à propriedade:<br /><br /> 1 = STREAM_FLAGS_DISALLOW_URL 2 = STREAM_FLAGS_DISALLOW_ABSOLUTE_PATH 4 = STREAM_FLAGS_DISALLOW_QUERY 8 = STREAM_FLAGS_       DONTCACHEMAPPINGSCHEMA 16 = STREAM_FLAGS_DONTCACHETEMPLATE 32 = STREAM_FLAGS_DONTCACHEXSL<br /><br /> Informações adicionais sobre esses valores são fornecidas na próxima tabela.|  
|xml root||Esta propriedade é usada para definir uma marca raiz para o XML resultante. Por exemplo, se você executar consultas SQL no banco de dados e o documento XML resultante não tiver um elemento raiz, o valor da propriedade será usado para adicionar um elemento raiz ao documento.<br /><br /> Para obter um exemplo em que essa propriedade é usada, consulte [executando consultas SQL &#40;provedor de SQLXMLOLEDB&#41;](executing-sql-queries-sqlxmloledb-provider.md).|  
|xsl||Esta propriedade é usada para especificar o nome do arquivo XSL quando você deseja aplicar a transformação XSL ao documento XML retornado pela consulta.<br /><br /> O caminho especificado pode ser relativo (xyz/abc/MyXSL.xsl) ou absoluto (C:\MyFolder\abc\MyXSL.xsl).<br /><br /> Se um caminho relativo for especificado, o caminho base especificado pela propriedade caminho base será usado para resolver o caminho relativo. Se nenhum caminho tiver sido especificado na propriedade caminho base, o caminho relativo será relativo ao diretório atual.<br /><br /> Para obter um exemplo em que essa propriedade é usada, consulte aplicando um XSL Transformation (provedor SQLXMLOLEDB).|  
  
 A tabela a seguir contém descrições dos valores de propriedade de sinalizadores de fluxo de SS.  
  
|Valor da propriedade|Descrição|  
|--------------------|-----------------|  
|STREAM_FLAGS_DISALLOW_URL|Não são aceitas URLs para esquemas de mapeamento ou XSL.|  
|STREAM_FLAGS_DISALLOW_ABSOLTE_PATH|Um caminho especificado para um esquema de mapeamento ou para XSL deve ser relativo ao caminho de base do próprio modelo.|  
|STREAM_FLAGS_DISALLOW_QUERY|Não são permitidas consultas em um modelo.|  
|STREAM_FLAGS_DONTCACHEMAPPINGSCHEMA|O esquema de mapeamento não é armazenado em cache. Este valor de propriedade é útil durante a fase de desenvolvimento do banco de dados, quando esquemas de banco de dados estão sujeitos a alteração.|  
|STREAM_FLAGS_DONTCACHETEMPLATE|Os modelos não são armazenados em cache.|  
|STREAM_FLAGS_DONTCACHEXSL|XSL não é armazenada em cache.|  
  
  
