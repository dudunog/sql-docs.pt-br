---
title: Coleções de esquemas comuns
description: Descreve todas as coleções de esquemas comuns compatíveis com todos os provedores gerenciados do .NET.
ms.date: 11/30/2020
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-chmalh
ms.openlocfilehash: 09e1a159d0b0ad1cb58c43bd23b1e7be500e7ae3
ms.sourcegitcommit: c938c12cf157962a5541347fcfae57588b90d929
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/25/2020
ms.locfileid: "97771646"
---
# <a name="common-schema-collections"></a>Coleções de esquemas comuns

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../includes/driver_adonet_download.md)]

As coleções de esquemas comuns são as coleções de esquemas que são implementadas por todos os provedores gerenciados do .NET. Consulte um provedor gerenciado do .NET para determinar a lista de coleções de esquemas compatíveis chamando o método **GetSchema** sem argumentos ou com o nome da coleção de esquemas "MetaDataCollections". Isso retornará uma <xref:System.Data.DataTable> com uma lista de coleções de esquemas compatíveis, o número de restrições ao qual cada uma dá suporte e o número de partes de identificador usado por elas. Essas coleções descrevem todas as colunas necessárias. Os provedores são livres para adicionar mais colunas se desejado. Por exemplo, o Provedor de Dados Microsoft SqlClient para SQL Server adiciona ParameterName à coleção de restrições.  

Se um provedor não puder determinar o valor de uma coluna necessária, ele retornará nulo.  
  
Para obter mais informações sobre como usar os métodos **GetSchema**, confira [GetSchema e coleções de esquemas](getschema-and-schema-collections.md).  

## <a name="metadatacollections"></a>MetaDataCollections  

Essa coleção de esquemas expõe informações sobre todas as coleções de esquemas compatíveis com o Provedor de Dados Microsoft SqlClient para SQL Server que é usado atualmente para se conectar ao banco de dados.  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|CollectionName|string|O nome da coleção a ser transmitida para o método **GetSchema** para retornar a coleção.|  
|NumberOfRestrictions|INT|O número de restrições que podem ser especificadas para a coleção.|  
|NumberOfIdentifierParts|INT|O número de partes no nome do objeto de banco de dados/identificador composto. Por exemplo, em SQL Server, isso seria três para tabelas e quatro para colunas.|  

## <a name="datasourceinformation"></a>DataSourceInformation  

Essa coleção de esquemas expõe informações sobre a fonte de dados à qual o Provedor de Dados Microsoft SqlClient para SQL Server está conectado no momento.  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|CompositeIdentifierSeparatorPattern|string|A expressão regular usada para corresponder os separadores compostos em um identificador composto. Por exemplo, "\\". (para o SQL Server).<br /><br /> Um identificador composto normalmente é o que é usado para um nome de objeto de banco de dados, por exemplo: pubs.dbo.authors ou pubs\@dbo.authors.<br /><br /> Para o SQL Server, use a expressão regular "\\.". |  
|DataSourceProductName|string|O nome do produto acessado pelo provedor, como "SQLServer".|  
|DataSourceProductVersion|string|Indica a versão do produto acessada pelo provedor, no formato nativo de fontes de dados e não no formato da Microsoft.<br /><br /> Em alguns casos, DataSourceProductVersion e DataSourceProductVersionNormalized terão o mesmo valor. |  
|DataSourceProductVersionNormalized|string|Uma versão normalizada para a fonte de dados, de modo que ela possa ser comparada com `String.Compare()`. O formato disso é consistente para todas as versões do provedor a fim de impedir que a versão 10 seja classificada entre a versão 1 e a versão 2.<br /><br /> Por exemplo, o SQL Server usa o formato típico da Microsoft "nn.nn.nnnn".<br /><br /> Em alguns casos, DataSourceProductVersion e DataSourceProductVersionNormalized terão o mesmo valor. |  
|GroupByBehavior|<xref:System.Data.Common.GroupByBehavior>|Especifica a relação entre as colunas em uma cláusula GROUP BY e as colunas não agregadas na lista de seleção.|  
|IdentifierPattern|string|Uma expressão regular que corresponde a um identificador e tem um valor de correspondência do identificador. Por exemplo, "[A-Za-z0-9_#$]".|  
|IdentifierCase|<xref:System.Data.Common.IdentifierCase>|Indica se identificadores que não estão entre aspas são tratados como diferenciando maiúsculas de minúsculas.|  
|OrderByColumnsInSelect|bool|Especifica se as colunas em uma cláusula ORDER BY precisam estar na lista de seleção. Um valor igual a true indica que elas devem estar na lista de seleção, e um valor igual a false indica que elas não devem estar na lista de seleção.|  
|ParameterMarkerFormat|string|Uma cadeia de caracteres de formato que representa como formatar um parâmetro.<br /><br /> Se os parâmetros nomeados forem compatíveis com a fonte de dados, o primeiro espaço reservado nessa cadeia de caracteres deverá ser o local em que o nome do parâmetro deve ser formatado.<br /><br /> Por exemplo, se a fonte de dados espera que os parâmetros sejam nomeados e prefixados com um ':', isso será ":{0}". Ao formatar isso com um nome de parâmetro "P1", a cadeia de caracteres resultante será ":p1".<br /><br /> Se a fonte de dados esperar que os parâmetros sejam prefixados com o '\@', mas os nomes já os incluírem, isso será '{0}', e o resultado da formatação de um parâmetro chamado "\@p1" será apenas "\@p1".<br /><br /> Para as fontes de dados que não esperam parâmetros nomeados e esperam o uso do caractere '?', a cadeia de caracteres de formato pode ser especificada simplesmente como '?', o que ignora o nome do parâmetro. |  
|ParameterMarkerPattern|string|Uma expressão regular que corresponde a um marcador de parâmetro. Ele terá um valor de correspondência do nome do parâmetro, se houver.<br /><br /> Por exemplo, se houver suporte para parâmetros nomeados com um caractere '\@' à esquerda que será incluído no nome do parâmetro, isso será "(\@[A-Za-z0-9_$#]*)".<br /><br /> No entanto, se houver suporte para parâmetros nomeados com um ':' como o caractere à esquerda e ele não fizer parte do nome do parâmetro, isso será ":([A-Za-z0-9_$#]\*)".<br /><br /> Obviamente, se a fonte de dados não der suporte a parâmetros nomeados, isso simplesmente será "?".|  
|ParameterNameMaxLength|INT|O tamanho máximo de um nome de parâmetro em caracteres. O Visual Studio espera que, se houver suporte para nomes de parâmetro, o valor mínimo para o tamanho máximo será de 30 caracteres.<br /><br /> Se a fonte de dados não der suporte a parâmetros nomeados, essa propriedade retornará zero.|  
|ParameterNamePattern|string|Uma expressão regular que corresponde aos nomes de parâmetros válidos. Fontes de dados diferentes têm regras diferentes sobre os caracteres que podem ser usados como nomes de parâmetros.<br /><br /> O Visual Studio espera que, se houver suporte para nomes de parâmetros, os caracteres "\p{Lu}\p{Ll}\p{Lt}\p{Lm}\p{Lo}\p{Nl}\p{Nd}" sejam o conjunto mínimo de caracteres compatíveis válidos para nomes de parâmetros.|  
|QuotedIdentifierPattern|string|Uma expressão regular que corresponde a um identificador entre aspas e tem um valor de correspondência do próprio identificador sem aspas. Por exemplo, se a fonte de dados usou aspas duplas para identificar identificadores entre aspas, isso será "(([^\\"]&#124;\\"\\")*)".|  
|QuotedIdentifierCase|<xref:System.Data.Common.IdentifierCase>|Indica se os identificadores entre aspas são tratados como diferenciando maiúsculas de minúsculas.|  
|StatementSeparatorPattern|string|Uma expressão regular que corresponde ao separador de instrução.|  
|StringLiteralPattern|string|Uma expressão regular que corresponde a um literal de cadeia de caracteres e tem um valor de correspondência do próprio literal. Por exemplo, se a fonte de dados usou aspas simples para identificar cadeias de caracteres, isso será "('([^']&#124;'')*')"'|  
|SupportedJoinOperators|<xref:System.Data.Common.SupportedJoinOperators>|Especifica quais tipos de instruções SQL de junção são compatíveis com a fonte de dados.|  

## <a name="datatypes"></a>DataTypes  

Essa coleção de esquemas expõe informações sobre os tipos de dados compatíveis com o banco de dados ao qual o Provedor de Dados Microsoft SqlClient para SQL Server está atualmente conectado.  

|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|TypeName|string|O nome de tipo de dados específico do provedor.|  
|ProviderDbType|INT|O valor do tipo específico do provedor que deve ser usado ao especificar o tipo de um parâmetro. Por exemplo, SqlDbType.Money.|  
|ColumnSize|long|O tamanho de uma coluna não numérica ou um parâmetro se refere ao máximo ou ao tamanho definido para esse tipo pelo provedor.<br /><br /> Para dados de caractere, esse é o máximo ou o tamanho definido em unidades, definido pela fonte de dados. <br /><br /> Para tipos de dados de data/hora, esse é o tamanho da representação de cadeia de caracteres (supondo que o máximo permitiu a precisão do componente em segundos fracionários).<br /><br /> Se o tipo de dados for numérico, esse será o limite superior na precisão máxima do tipo de dados.|  
|CreateFormat|string|Cadeia de caracteres de formato que representa como adicionar essa coluna a uma instrução de definição de dados, como CREATE TABLE. Cada elemento da matriz CreateParameter deve ser representado por um "marcador de parâmetro" na cadeia de caracteres de formato.<br /><br /> Por exemplo, o tipo de dados SQL DECIMAL exige uma precisão e uma escala. Nesse caso, a cadeia de caracteres de formato será "DECIMAL({0},{1})".|  
|CreateParameters|string|Os parâmetros de criação que precisam ser especificados ao criar uma coluna desse tipo de dados. Cada parâmetro de criação é listado na cadeia de caracteres, separado por uma vírgula na ordem em que deve ser fornecido.<br /><br /> Por exemplo, o tipo de dados SQL DECIMAL exige uma precisão e uma escala. Nesse caso, os parâmetros de criação devem conter a cadeia de caracteres "precisão, escala".<br /><br /> Em um comando de texto, para criar uma coluna DECIMAL com uma precisão igual a 10 e uma escala igual a 2, o valor da coluna CreateFormat poderá ser DECIMAL({0},{1})" e a especificação de tipo completa será DECIMAL(10,2).|  
|Tipo de dados|string|O nome do tipo .NET do tipo de dados.|  
|IsAutoincrementable|bool|true: os valores desse tipo de dados podem ser incrementados automaticamente.<br /><br /> false: os valores desse tipo de dados podem não ser incrementados automaticamente.<br /><br /> Observe que isso apenas indica se uma coluna desse tipo de dados pode ser incrementada automaticamente, não que todas as colunas desse tipo sejam incrementadas automaticamente.|  
|IsBestMatch|bool|true: o tipo de dados é a melhor correspondência entre todos os tipos de dados do armazenamento de dados e o tipo de dados .NET indicado pelo valor na coluna DataType.<br /><br /> false: o tipo de dados não é a melhor correspondência.<br /><br /> Para cada conjunto de linhas no qual o valor da coluna DataType é idêntico, a coluna IsBestMatch é definida como true em apenas uma linha.|  
|IsCaseSensitive|bool|true: o tipo de dados é um tipo de caractere e diferencia maiúsculas de minúsculas.<br /><br /> false: o tipo de dados não é um tipo de caractere ou não diferencia maiúsculas de minúsculas.|  
|IsFixedLength|bool|true: colunas desse tipo de dados criadas pela DDL (linguagem de definição de dados) terão um comprimento fixo.<br /><br /> false: colunas desse tipo de dados criadas pela DDL terão um comprimento variável.<br /><br /> DBNull.Value: é desconhecido se o provedor mapeará esse campo com uma coluna de comprimento fixo ou variável.|  
|IsFixedPrecisionScale|bool|true: o tipo de dados tem uma precisão e uma escala fixas.<br /><br /> false: o tipo de dados não tem uma precisão e uma escala fixas.|  
|IsLong|bool|true: o tipo de dados contém dados muito longos; a definição de dados muito longos é específica do provedor.<br /><br /> false: o tipo de dados não contém dados muito longos.|  
|IsNullable|bool|true: o tipo de dados permite valor nulo.<br /><br /> false: o tipo de dados não permite valor nulo.<br /><br /> DBNull.Value: é desconhecido se o tipo de dados permite valores nulos.|  
|IsSearchable|bool|true: o tipo de dados pode ser usado em uma cláusula WHERE com qualquer operador, exceto o predicado LIKE.<br /><br /> false: o tipo de dados não pode ser usado em uma cláusula WHERE com nenhum operador, exceto o predicado LIKE.|  
|IsSearchableWithLike|bool|true: o tipo de dados pode ser usado com o predicado LIKE<br /><br /> false: o tipo de dados não pode ser usado com o predicado LIKE.|  
|IsUnsigned|bool|true: o tipo de dados é sem sinal.<br /><br /> false: o tipo de dados é com sinal.<br /><br /> DBNull.Value: não aplicável ao tipo de dados.|  
|MaximumScale|short|Se o indicador de tipo for um tipo numérico, esse será o número máximo de dígitos permitidos à direita do ponto decimal. Caso contrário, é DBNull.Value.|  
|MinimumScale|short|Se o indicador de tipo for um tipo numérico, esse será o número mínimo de dígitos permitidos à direita do ponto decimal. Caso contrário, é DBNull.Value.|  
|IsConcurrencyType|bool|true: o tipo de dados é atualizado pelo banco de dados sempre que a linha é alterada e o valor da coluna é diferente de todos os valores anteriores<br /><br /> false: o tipo de dados não é atualizado pelo banco de dados sempre que a linha é alterada<br /><br /> DBNull.Value: o banco de dados não dá suporte a esse tipo de dados|  
|IsLiteralSupported|bool|true: o tipo de dados pode ser expresso como um literal<br /><br /> false: o tipo de dados não pode ser expresso como um literal|  
|LiteralPrefix|string|O prefixo aplicado a um literal específico.|  
|LiteralSuffix|string|O sufixo aplicado a um literal específico.|  

## <a name="restrictions"></a>Restrições 

Essa coleção de esquemas expôs informações sobre as restrições compatíveis com o Provedor de Dados Microsoft SqlClient para SQL Server que é atualmente usado para se conectar ao banco de dados.  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|CollectionName|string|O nome da coleção à qual essas restrições se aplicam.|  
|RestrictionName|string|O nome da restrição na coleção.|  
|RestrictionDefault|string|Ignorado.|  
|RestrictionNumber|INT|A localização real nas restrições de coleções em que essa restrição específica se enquadra.|  

## <a name="reservedwords"></a>ReservedWords  

Essa coleção de esquemas expõe informações sobre as palavras reservadas pelo banco de dados ao qual o Provedor de Dados Microsoft SqlClient para SQL Server está atualmente conectado.  
  
|ColumnName|Tipo de dados|Descrição|  
|----------------|--------------|-----------------|  
|ReservedWord|string|Palavra reservada específica do provedor.|  

## <a name="see-also"></a>Confira também

- [Recuperar informações de esquema de banco de dados](retrieving-database-schema-information.md)
- [As coleções de esquemas e GetSchema](getschema-and-schema-collections.md)
- [Microsoft ADO.NET for SQL Server](microsoft-ado-net-sql-server.md)
