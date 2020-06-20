---
title: Arquivos de formato XML (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- format files [SQL Server], XML format files
- bulk importing [SQL Server], format files
- XML format files [SQL Server]
ms.assetid: 69024aad-eeea-4187-8fea-b49bc2359849
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7cc1e8de30fa582898ef8516b9767dec14c4fa81
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050455"
---
# <a name="xml-format-files-sql-server"></a>Arquivos de formato XML (SQL Server)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] fornece um esquema XML que define a sintaxe para escrever *arquivos de formato XML* a serem usados para importar dados em massa para uma tabela do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Arquivos no formato XML devem aderir a este esquema que está definido no Schema Definition Language XML (XSDL). Os arquivos de formato XML só têm suporte quando as ferramentas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são instaladas junto com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
 Você pode usar um arquivo no formato XML com um comando **bcp**, uma instrução BULK INSERT ou INSERT ... Instrução SELECT \* FROM OPENROWSET(BULK...). O comando **bcp** permite gerar automaticamente um arquivo no formato XML para uma tabela; para obter mais informações, consulte [bcp Utility](../../tools/bcp-utility.md).  
  
> [!NOTE]  
>  Há suporte a dois tipos de arquivos de formato de exportação e importação em massa: *arquivos de formato não XML* e *arquivos de formato XML*. Arquivos de formato XML fornecem uma alternativa flexível e poderosa para arquivos de formato não XML. Para obter informações sobre arquivos de formato não XML, veja [Arquivos de formato não XML &#40;SQL Server&#41;](xml-format-files-sql-server.md).  
  

  
##  <a name="benefits-of-xml-format-files"></a><a name="BenefitsOfXmlFFs"></a> Benefícios de arquivos de formato XML  
  
-   Arquivos de formato XML são autodescritivos, o que facilita sua leitura, criação e extensão. Eles são legíveis, tornando fácil compreender como são os dados são interpretados durante operações em massa.  
  
-   Arquivos no formato XML contêm os tipos de dados das colunas de destino.  A codificação XML descreve claramente os tipos de dados e elementos de dados do arquivo de dados e também o mapeamento entre elementos de dados e colunas de tabela.  
  
     Isso permite a separação entre como os dados são representados no arquivo de dados e quais tipos de dados são associados a cada campo no arquivo. Por exemplo, se um arquivo de dados contiver uma representação de caracteres dos dados, o tipo de coluna SQL correspondente será perdido.  
  
-   Um arquivo no formato XML permite carregar um campo contendo um único tipo de dado de objeto grande (LOB) de um arquivo de dados.  
  
-   Um arquivo de formato XML pode ser aprimorado e ainda permanecer compatível com suas versões anteriores. Além disso, a clareza da codificação XML facilita a criação de arquivos em formatos múltiplos para um determinado arquivo de dados. Isto será útil se você tiver que mapear tudo ou alguns dos campos de dados para colunas em tabelas ou exibições diferentes.  
  
-   A sintaxe de um arquivo de formato é independente da direção da operação; ou seja, a sintaxe é a mesma para exportação ou importação em massa.  
  
-   Você pode usar arquivos no formato XML para importar em massa dados em tabelas ou visualizações não particionadas e para exportar em massa dados.  
  
-   Para a função OPENROWSET (BULK...), a especificação de uma tabela de destino é opcional. Isso ocorre porque a função depende do arquivo de formato XML para ler dados de um arquivo de dados.  
  
    > [!NOTE]  
    >  Uma tabela de destino é necessária com o comando **bcp** e a instrução BULK INSERT, que usa as colunas da tabela de destino para fazer a conversão do tipo.  
  
##  <a name="structure-of-xml-format-files"></a><a name="StructureOfXmlFFs"></a> Estrutura de arquivos no formato não XML  
 Como um arquivo de formato não XML, um arquivo de formato XML define o formato e a estrutura dos campos de dados em um arquivo de dados e mapeia esses campos de dados a colunas em uma única tabela de destino.  
  
 Um arquivo de formato XML possui dois componentes principais \<RECORD> e \<ROW> :  
  
-   \<RECORD>Descreve os dados conforme eles são armazenados no arquivo de dados.  
  
     Cada \<RECORD> elemento contém um conjunto de um ou mais \<FIELD> elementos. Estes elementos correspondem a campos no arquivo de dados. A sintaxe básica é a seguinte:  
  
     \<RECORD>  
  
     \<FIELD .../>[ ... *n* ]  
  
     \</RECORD>  
  
     Cada \<FIELD> elemento descreve o conteúdo de um campo de dados específico. Um campo só pode ser mapeado para uma coluna na tabela. Nem todos os campos precisam ser mapeados para colunas.  
  
     Um campo em um arquivo de dados pode ser de comprimento fixo/variável ou terminado em caractere. Um *valor de campo* pode ser representado como: um caractere (usando representação do byte único), um caractere largo (usando representação Unicode de dois bytes), formato de banco de dados nativo ou um nome de arquivo. Se um valor de campo for representado como um nome de arquivo, o nome de arquivo apontará ao arquivo que contém o valor de uma coluna de BLOB na tabela destino.  
  
-   \<ROW>Descreve como construir linhas de dados de um arquivo de dados quando os dados do arquivo são importados para uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabela.  
  
     Um \<ROW> elemento contém um conjunto de \<COLUMN> elementos. Esses elementos correspondem a colunas de tabela. A sintaxe básica é a seguinte:  
  
     \<ROW>  
  
     \<COLUMN .../>[ ... *n* ]  
  
     \</ROW>  
  
     Cada \<COLUMN> elemento pode ser mapeado para apenas um campo no arquivo de dados. A ordem dos \<COLUMN> elementos no \<ROW> elemento define a ordem na qual eles são retornados pela operação em massa. O arquivo de formato XML atribui a cada \<COLUMN> elemento um nome local que não tem nenhuma relação com a coluna na tabela de destino de uma operação de importação em massa.  
  
##  <a name="schema-syntax-for-xml-format-files"></a><a name="SchemaSyntax"></a> Sintaxe de esquema para arquivos de formato XML  
 Esta seção contém um resumo dos elementos e atributos do esquema XML para arquivos no formato XML. A sintaxe de um arquivo de formato é independente da direção da operação; ou seja, a sintaxe é a mesma para exportação ou importação em massa. Esta seção também considera como a importação em massa usa os \<ROW> \<COLUMN> elementos e e como colocar o valor xsi: Type de um elemento em um conjunto de dados.  
  
 Para ver como a sintaxe corresponde aos arquivos de formato XML atuais, consulte [Arquivos de formato XML de exemplo](#SampleXmlFFs), mais adiante neste tópico.  
  
> [!NOTE]  
>  Você pode modificar um arquivo de formato para importar em massa de um arquivo de dados no qual o número e/ou a ordem dos campos difere do número e/ou da ordem das colunas na tabela. Para obter mais informações, consulte [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md).  
  
  
  
###  <a name="basic-syntax-of-the-xml-schema"></a><a name="BasicSyntax"></a> Sintaxe básica de esquema XML  
 Essas instruções de sintaxe mostram apenas os elementos (,,, \<BCPFORMAT> \<RECORD> \<FIELD> \<ROW> e \<COLUMN> ) e seus atributos básicos.  
  
 \<BCPFORMAT ...>  
  
 \<RECORD>  
  
 \<FIELD ID = "*fieldID*" xsi:type = "*fieldType*" [...]  
  
 />  
  
 \</RECORD>  
  
 \<ROW>  
  
 \<COLUMN SOURCE = "*fieldID*" NAME = "*columnName*" xsi:type = "*columnType*" [...]  
  
 />  
  
 \</ROW>  
  
 \</BCPFORMAT>  
  
> [!NOTE]  
>  Atributos adicionais associados ao valor de xsi: Type em um \<FIELD> \<COLUMN> elemento ou são descritos posteriormente neste tópico.  
  

  
####  <a name="schema-elements"></a><a name="SchemaElements"></a> Elementos de esquema  
 Esta seção resume a finalidade de cada elemento que o esquema XML define para os arquivos de formato XML. Os atributos são descritos em seções separadas posteriormente neste tópico.  
  
 \<BCPFORMAT>  
 É o elemento de formato de arquivo que define a estrutura do registro de um determinado arquivo de dados e sua correspondência às colunas de uma linha de tabela na tabela.  
  
 \<RECORD .../>  
 Define um elemento complexo que contém um ou mais \<FIELD> elementos. A ordem na qual os campos são declarados no arquivo de formato é a ordem na qual esses campos aparecem no arquivo de dados.  
  
 \<FIELD .../>  
 Define um campo no arquivo de dados que contém dados.  
  
 Os atributos desse elemento são discutidos em [atributos do \<FIELD> elemento](#AttrOfFieldElement), mais adiante neste tópico.  
  
 \<ROW .../>  
 Define um elemento complexo que contém um ou mais \<COLUMN> elementos. A ordem dos \<COLUMN> elementos é independente da ordem dos \<FIELD> elementos em uma definição de registro. Em vez disso, a ordem dos \<COLUMN> elementos em um arquivo de formato determina a ordem da coluna do conjunto de linhas resultante. Os campos de dados são carregados na ordem em que os \<COLUMN> elementos correspondentes são declarados no \<COLUMN> elemento.  
  
 Para obter mais informações, consulte [como a importação em massa usa o \<ROW> elemento](#HowUsesROW), mais adiante neste tópico.  
  
 \<COLUMN>  
 Define uma coluna como um elemento ( \<COLUMN> ). Cada \<COLUMN> elemento corresponde a um \<FIELD> elemento (cuja ID é especificada no atributo de origem do \<COLUMN> elemento).  
  
 Os atributos desse elemento são discutidos em [atributos do \<COLUMN> elemento](#AttrOfColumnElement), mais adiante neste tópico. Além disso, veja [como a importação em massa usa o \<COLUMN> elemento](#HowUsesColumn), mais adiante neste tópico.  
  
 \</BCPFORMAT>  
 Obrigatório para finalizar o arquivo de formato.  
  
####  <a name="attributes-of-the-field-element"></a><a name="AttrOfFieldElement"></a>Atributos do \<FIELD> elemento  
 Esta seção descreve os atributos do \<FIELD> elemento, que são resumidos na seguinte sintaxe de esquema:  
  
 Valores de <FIELD  
  
 ID **= " *`fieldID`* "**  
  
 xsi **:** Type **= " *`fieldType`* "**  
  
 [ LENGTH **="*`n`*"** ]  
  
 [PREFIX_LENGTH **= " *`p`* "** ]  
  
 [MAX_LENGTH **= " *`m`* "** ]  
  
 [COLLATION **= " *`collationName`* "** ]  
  
 [TERMINAdor **= " *`terminator`* "** ]  
  
 />  
  
 Cada \<FIELD> elemento é independente dos outros. Um campo é descrito em termos dos seguintes atributos:  
  
|Atributo FIELD|Descrição|Opcional /<br /><br /> Obrigatório|  
|---------------------|-----------------|------------------------------|  
|ID **= " *`fieldID`* "**|Especifica o nome lógico do campo no arquivo de dados. A ID de um campo é a chave para fazer referência ao campo.<br /><br /> <ID do campo **= " *`fieldID`* "**/> mapeia para <origem da coluna **= " *`fieldID`* "**/>|Obrigatório|  
|xsi: Type **= " *`fieldType`* "**|Essa é uma construção XML (usada como um atributo) que identifica o tipo da instância do elemento. O valor de *fieldType* determina de quais atributos opcionais (abaixo) você necessita em determinada instância.|Obrigatório (dependendo do tipo de dados)|  
|COMPRIMENTO **= " *`n`* "**|Esse atributo define o comprimento de uma instância de um tipo de dados de comprimento fixo.<br /><br /> O valor de *n* deve ser um inteiro positivo.|Opcional, a menos que exigido pelo valor xsi:type|  
|PREFIX_LENGTH **= " *`p`* "**|Esse atributo define o comprimento do prefixo para uma representação de dados binária. O valor PREFIX_LENGTH, *p*, deve ser um dos seguintes: 1, 2, 4 ou 8.|Opcional, a menos que exigido pelo valor xsi:type|  
|MAX_LENGTH **= " *`m`* "**|Esse atributo é o número máximo de bytes que pode ser armazenado em um determinado campo. Sem uma tabela de destino, o comprimento máximo da coluna é conhecido. O atributo MAX_LENGTH restringe o comprimento máximo de uma coluna de caracteres de saída, limitando o armazenamento alocado para o valor da coluna. Isso é especialmente conveniente ao usar a opção BULK da função OPENROWSET em uma cláusula SELECT FROM.<br /><br /> O valor de *m* deve ser um inteiro positivo. Por padrão, o comprimento máximo é 8.000 caracteres para uma coluna **char** e 4.000 caracteres para uma coluna **nchar** .|Opcional|  
|COLLATION **= " *`collationName`* "**|COLLATION só é permitido para campos de caracteres. Para obter uma lista dos nomes de ordenação do SQL, veja [Nome de ordenação do SQL Server &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql).|Opcional|  
|TERMINAdor **= " *`terminator`* "**|Esse atributo especifica o terminador de um campo de dados. O terminador pode ser qualquer caractere. O terminador deve ser um caractere exclusivo que não faça parte dos dados.<br /><br /> Por padrão, o terminador de campo é o caractere de tabulação (representado como \t). Para representar uma marca de parágrafo, use \r\n.|Usado somente com um xsi:type de dados de caracteres, que requer esse atributo|  
  
#####  <a name="xsitype-values-of-the-field-element"></a><a name="XsiTypeValuesOfFIELD"></a>Valores de xsi: Type do \<FIELD> elemento  
 O valor de xsi:type é uma construção XML (usada como um atributo) que identifica o tipo de dados de uma instância de um elemento. Para obter informações sobre como usar o valor de xsi:type, consulte "Colocando o valor de xsi:type em um conjunto de dados", posteriormente nesta seção.  
  
 O valor de xsi: Type do \<FIELD> elemento dá suporte aos seguintes tipos de dados.  
  
|\<FIELD>valores de xsi: Type|Atributos XML obrigatórios<br /><br /> para tipo de dados|Atributos XML opcionais<br /><br /> para tipo de dados|  
|-------------------------------|---------------------------------------------------|---------------------------------------------------|  
|**NativeFixed**|`LENGTH`|Nenhum.|  
|**NativePrefix**|`PREFIX_LENGTH`|MAX_LENGTH|  
|**CharFixed**|`LENGTH`|COLLATION|  
|**NCharFixed**|`LENGTH`|COLLATION|  
|**CharPrefix**|`PREFIX_LENGTH`|MAX_LENGTH, COLLATION|  
|**NCharPrefix**|`PREFIX_LENGTH`|MAX_LENGTH, COLLATION|  
|**CharTerm**|`TERMINATOR`|MAX_LENGTH, COLLATION|  
|**NCharTerm**|`TERMINATOR`|MAX_LENGTH, COLLATION|  
  
 Para obter mais informações sobre tipos de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], confira [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql).  
  
####  <a name="attributes-of-the-column-element"></a><a name="AttrOfColumnElement"></a>Atributos do \<COLUMN> elemento  
 Esta seção descreve os atributos do \<COLUMN> elemento, que são resumidos na seguinte sintaxe de esquema:  
  
 \<COLUMN  
  
 SOURCE = "*fieldID*"  
  
 NAME = "*columnName*"  
  
 xsi:type = "*columnType*"  
  
 [ LENGTH = "*n*" ]  
  
 [ PRECISION = "*n*" ]  
  
 [ SCALE = "*value*" ]  
  
 [ NULLABLE = { "YES"  
  
 "NO" } ]  
  
 />  
  
 Um campo é mapeado para uma coluna na tabela de destino usando os seguintes atributos:  
  
|Atributo COLUMN|Descrição|Opcional /<br /><br /> Obrigatório|  
|----------------------|-----------------|------------------------------|  
|ORIGEM **= " *`fieldID`* "**|Especifica a ID do campo que é mapeado para a coluna.<br /><br /> <coluna Source **= " *`fieldID`* "**/> mapeia para <campo ID **= " *`fieldID`* "**/>|Obrigatório|  
|NAME = "*columnName*"|Especifica o nome da coluna no conjunto de linhas representado pelo arquivo de formato. Esse nome de coluna é usado para identificar a coluna no conjunto de resultados e não precisa corresponder ao nome da coluna usado na tabela de destino.|Obrigatório|  
|xsi **:** Type **= " *`ColumnType`* "**|Essa é uma construção XML (usada como um atributo) que identifica o tipo de dados da instância do elemento. O valor de *ColumnType* determina de quais atributos opcionais (abaixo) você necessita em uma determinada instância.<br /><br /> Observação: os valores possíveis de *ColumnType* e seus atributos associados são listados na tabela a seguir.|Opcional|  
|COMPRIMENTO **= " *`n`* "**|Define o comprimento de uma instância de um tipo de dados de comprimento fixo. LENGTH só é usado quando xsi:type é um tipo de dados de cadeia de caracteres.<br /><br /> O valor de *n* deve ser um inteiro positivo.|Opcional (disponível somente se xsi:type for um tipo de dados de cadeia de caracteres)|  
|PRECISION **="*`n`*"**|Indica o número de dígitos em um número. Por exemplo, o número 123,45 tem uma precisão de 5.<br /><br /> O valor deve ser um inteiro positivo.|Opcional (disponível somente se xsi:type for um tipo de dados de número variável)|  
|SCALE **= " *`int`* "**|Indica o número de dígitos à direita da casa decimal em um número. Por exemplo, o número 123,45 tem uma escala de 2.<br /><br /> O valor deve ser um inteiro.|Opcional (disponível somente se xsi:type for um tipo de dados de número variável)|  
|NULLABLE **=** { **"** YES **"**<br /><br /> **"** NO **"** }|Indica se uma coluna pode assumir valores NULL. Esse atributo é completamente independente de FIELDS. Porém, se uma coluna não for NULLABLE e campo especificar NULL (não especificando nenhum valor), ocorrerá erro em tempo de execução.<br /><br /> O atributo NULLABLE será usado apenas se você executar uma instrução SELECT FROM OPENROWSET (BULK...) simples.|Opcional (disponível para qualquer tipo de dados)|  
  
#####  <a name="xsitype-values-of-the-column-element"></a><a name="XsiTypeValuesOfCOLUMN"></a>Valores de xsi: Type do \<COLUMN> elemento  
 O valor de xsi:type é uma construção XML (usada como um atributo) que identifica o tipo de dados de uma instância de um elemento. Para obter informações sobre como usar o valor de xsi:type, consulte "Colocando o valor de xsi:type em um conjunto de dados", posteriormente nesta seção.  
  
 O \<COLUMN> elemento oferece suporte a tipos de dados SQL nativos, da seguinte maneira:  
  
|Categoria do tipo|\<COLUMN>Tipos de dados|Atributos XML obrigatórios<br /><br /> para tipo de dados|Atributos XML opcionais<br /><br /> para tipo de dados|  
|-------------------|---------------------------|---------------------------------------------------|---------------------------------------------------|  
|Correção|`SQLBIT`, `SQLTINYINT`, `SQLSMALLINT`, `SQLINT`, `SQLBIGINT`, `SQLFLT4`, `SQLFLT8`, `SQLDATETIME`, `SQLDATETIM4`, `SQLDATETIM8`, `SQLMONEY`, `SQLMONEY4`, `SQLVARIANT`, e `SQLUNIQUEID`|Nenhum.|NULLABLE|  
|Número variável|`SQLDECIMAL` e `SQLNUMERIC`|Nenhum.|NULLABLE, PRECISION, SCALE|  
|LOB|`SQLIMAGE`, `CharLOB`, `SQLTEXT` e `SQLUDT`|Nenhum.|NULLABLE|  
|LOB caractere|`SQLNTEXT`|Nenhum.|NULLABLE|  
|Cadeia de caracteres binária|`SQLBINARY` e `SQLVARYBIN`|Nenhum.|NULLABLE, LENGTH|  
|Cadeia de caracteres|`SQLCHAR`, `SQLVARYCHAR`, `SQLNCHAR` e `SQLNVARCHAR`|Nenhum.|NULLABLE, LENGTH|  
  
> [!IMPORTANT]  
>  Para exportar ou importar dados SQLXML em massa, use um dos tipos de dados a seguir em seu arquivo de formato: SQLCHAR ou SQLVARYCHAR (os dados são enviados na página de código do cliente ou na página de código implícita pela ordenação), SQLNCHAR ou SQLNVARCHAR (os dados são enviados como Unicode), ou SQLBINARY ou SQLVARYBIN (os dados são enviados sem nenhuma conversão).  
  
 Para obter mais informações sobre os tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , veja [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql).  
  
###  <a name="how-bulk-import-uses-the-row-element"></a><a name="HowUsesROW"></a>Como a importação em massa usa o \<ROW> elemento  
 O \<ROW> elemento é ignorado em alguns contextos. Se o \<ROW> elemento afeta uma operação de importação em massa depende de como a operação é executada:  
  
-   o comando **bcp**  
  
     Quando os dados são carregados em uma tabela de destino, o **bcp** ignora o \<ROW> componente. Em vez disso, o **bcp** carrega os dados com base nos tipos de coluna da tabela de destino.  
  
-   [!INCLUDE[tsql](../../../includes/tsql-md.md)] Instruções (BULK INSERT e o provedor de conjuntos de linhas em massa OPENROWSET)  
  
     Ao importar dados em massa para uma tabela, [!INCLUDE[tsql](../../../includes/tsql-md.md)] as instruções usam o \<ROW> componente para gerar o conjunto de linhas de entrada. Além disso, as [!INCLUDE[tsql](../../../includes/tsql-md.md)] instruções executam conversões de tipo apropriadas com base nos tipos de coluna especificados em \<ROW> e na coluna correspondente na tabela de destino. Se houver uma incompatibilidade entre os tipos de coluna como especificado no arquivo de formato e na tabela de destino, ocorrerá uma conversão extra de tipo. Essa conversão extra do tipo pode levar a alguma discrepância (ou seja, uma perda de precisão) de comportamento no provedor do conjunto de linhas em massa do BULK INSERT ou do OPENROWSET quando comparado com o **bcp**.  
  
     As informações no \<ROW> elemento permitem que uma linha seja construída sem a necessidade de nenhuma informação adicional. Por isso, você pode gerar um conjunto de linhas com a instrução SELECT (SELECT \* FROM OPENROWSET(BULK *datafile* FORMATFILE=*xmlformatfile*).  
  
    > [!NOTE]  
    >  A cláusula OPENROWSET BULK requer um arquivo de formato (observe que a conversão do tipo de dados de campo ao tipo de dados de uma coluna só é disponibilizada com um arquivo de formato XML).  
  
###  <a name="how-bulk-import-uses-the-column-element"></a><a name="HowUsesColumn"></a>Como a importação em massa usa o \<COLUMN> elemento  
 Para a importação em massa de dados em uma tabela, os \<COLUMN> elementos em um arquivo de formato mapeiam um campo de arquivo de dados para colunas de tabela especificando:  
  
-   A posição de cada campo dentro de uma linha no arquivo de dados.  
  
-   O tipo de coluna usado para converter o tipo de dados de campo ao tipo de dados de coluna desejado.  
  
 Se nenhuma coluna for mapeada para um campo, o campo não será copiado na(s) linha(s) gerada(s). Esse comportamento permite que um arquivo de dados gere linhas com colunas diferentes (em tabelas diferentes).  
  
 Da mesma forma, para exportar dados em massa de uma tabela, cada um \<COLUMN> no arquivo de formato mapeia a coluna da linha da tabela de entrada para seu campo correspondente no arquivo de dados de saída.  
  
###  <a name="putting-the-xsitype-value-into-a-data-set"></a><a name="PutXsiTypeValueIntoDataSet"></a> Colocando o valor de xsi:type em um conjunto de dados  
 Quando um documento XML é validado com a linguagem XSD (XML Schema Definition), o valor de xsi:type não é colocado no conjunto de dados. Porém, você pode colocar a informações de xsi:type no conjunto de dados carregando o arquivo de formato XML em um documento XML (por exemplo, `myDoc`), como ilustrado no snippet de código seguinte:  
  
```  
...;  
myDoc.LoadXml(xmlFormat);  
XmlNodeList ColumnList = myDoc.GetElementsByTagName("COLUMN");  
for(int i=0;i<ColumnList.Count;i++)  
{  
   Console.Write("COLUMN: xsi:type=" +ColumnList[i].Attributes["type",  
      "http://www.w3.org/2001/XMLSchema-instance"].Value+"\n");  
}  
```  
  
##  <a name="sample-xml-format-files"></a><a name="SampleXmlFFs"></a> Arquivos de formato XML de exemplo  
 Esta seção contém informações sobre como usar arquivos no formato XML em uma variedade de casos, inclusive um exemplo de [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] .  
  
> [!NOTE]  
>  Nos arquivos de dados mostrados nos exemplos a seguir, `<tab>` indica um caractere de tabulação em um arquivo de dados e `<return>` indica um retorno de carro.  
  

  
> [!NOTE]  
>  Para obter informações sobre como criar arquivos de formato, veja [Criar um arquivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md).  
  
###  <a name="a-ordering-character-data-fields-the-same-as-table-columns"></a><a name="OrderCharFieldsSameAsCols"></a> A. Ordenar campos de dados de caracteres da mesma forma que colunas de tabelas  
 O exemplo a seguir mostra um arquivo de formato XML que descreve um arquivo de dados com três campos de dados de caracteres. O arquivo de formato mapeia o arquivo de dados para uma tabela que contém três colunas. Os campos de dados correspondem um a um às colunas da tabela.  
  
 **Tabela (linha):** Person (Age int, FirstName varchar(20), LastName varchar(30))  
  
 **Arquivo de dados (registro):** \<tab>Sobrenome do nome da idade \<tab>\<return>  
  
 O arquivo de formato XML a seguir grava do arquivo de dados na tabela.  
  
 No elemento `<RECORD>` , o arquivo de formato representa os valores de dados em todos os três campos como dados de caracteres. Para cada campo, o atributo `TERMINATOR` indica o terminador que segue o valor dos dados.  
  
 Os campos de dados correspondem um a um às colunas da tabela. No elemento `<ROW>` , o arquivo de formato mapeia a coluna `Age` para o primeiro campo, a coluna `FirstName` para o segundo campo e a coluna `LastName` para o terceiro campo.  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT   
xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <RECORD>  
    <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t"   
      MAX_LENGTH="12"/>   
    <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\t"   
      MAX_LENGTH="20" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
    <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n"   
      MAX_LENGTH="30"   
      COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  </RECORD>  
  <ROW>  
    <COLUMN SOURCE="1" NAME="age" xsi:type="SQLINT"/>  
    <COLUMN SOURCE="2" NAME="firstname" xsi:type="SQLVARYCHAR"/>  
    <COLUMN SOURCE="3" NAME="lastname" xsi:type="SQLVARYCHAR"/>  
  </ROW>  
</BCPFORMAT>  
```  
  
> [!NOTE]  
>  Para obter um exemplo equivalente de [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] , veja [Criar um arquivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md).  
  
###  <a name="b-ordering-data-fields-and-table-columns-differently"></a><a name="OrderFieldsAndColsDifferently"></a> B. Ordenar campos de dados e colunas de tabela diferentemente  
 O exemplo a seguir mostra um arquivo de formato XML que descreve um arquivo de dados com três campos de dados de caracteres. O arquivo de formato mapeia o arquivo de dados para uma tabela que contém três colunas ordenadas diferentemente dos campos do arquivo de dados.  
  
 **Tabela (linha):** Person (Age int, FirstName varchar(20), LastName varchar(30))  
  
 **Arquivo de dados** (registro): \<tab> nome sobrenome da idade \<tab>\<return>  
  
 No elemento `<RECORD>` , o arquivo de formato representa os valores de dados em todos os três campos como dados de caracteres.  
  
 No elemento `<ROW>` , o arquivo de formato mapeia a coluna `Age` para o primeiro campo, a coluna `FirstName` para o terceiro campo e a coluna `LastName` para o segundo campo.  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT   
xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <RECORD>  
    <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t"   
      MAX_LENGTH="12"/>  
    <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\t" MAX_LENGTH="20"   
      COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
    <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n"   
      MAX_LENGTH="30" COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  </RECORD>  
  <ROW>  
    <COLUMN SOURCE="1" NAME="age" xsi:type="SQLINT"/>  
    <COLUMN SOURCE="3" NAME="firstname" xsi:type="SQLVARYCHAR"/>  
    <COLUMN SOURCE="2" NAME="lastname" xsi:type="SQLVARYCHAR"/>  
  </ROW>  
</BCPFORMAT>  
```  
  
> [!NOTE]  
>  Para obter um exemplo equivalente de [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] , veja [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md).  
  
### <a name="c-omitting-a-data-field"></a>C. Omitir um campo de dados  
 O exemplo a seguir mostra um arquivo de formato XML que descreve um arquivo de dados com quatro campos de dados de caracteres. O arquivo de formato mapeia o arquivo de dados para uma tabela que contém três colunas. O segundo campo de dados não corresponde a nenhuma coluna de tabela.  
  
 **Tabela (linha):** Person (Age int, FirstName Varchar(20), LastName Varchar(30))  
  
 **Arquivo de dados (registro):** Nome do funcionário da idade \<tab> \<tab> \<tab> sobrenome\<return>  
  
 No elemento `<RECORD>` , o arquivo de formato representa os valores de dados em todos os quatro campos como dados de caractere. Para cada campo, o atributo TERMINATOR indica o terminador que segue o valor dos dados.  
  
 No elemento `<ROW>` , o arquivo de formato mapeia a coluna `Age` para o primeiro campo, a coluna `FirstName` para o terceiro campo e a coluna `LastName` para o quarto campo.  
  
```  
<BCPFORMAT   
xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <RECORD>  
    <FIELD ID="1" xsi:type="CharTerm" TERMINATOR="\t"   
      MAX_LENGTH="12"/>  
    <FIELD ID="2" xsi:type="CharTerm" TERMINATOR="\t"   
      MAX_LENGTH="10"   
      COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
    <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\t"   
      MAX_LENGTH="20"   
      COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
    <FIELD ID="4" xsi:type="CharTerm" TERMINATOR="\r\n"   
      MAX_LENGTH="30"   
      COLLATION="SQL_Latin1_General_CP1_CI_AS"/>  
  </RECORD>  
  <ROW>  
    <COLUMN SOURCE="1" NAME="age" xsi:type="SQLINT"/>  
    <COLUMN SOURCE="3" NAME="firstname" xsi:type="SQLVARYCHAR"/>  
    <COLUMN SOURCE="4" NAME="lastname" xsi:type="SQLVARYCHAR"/>  
  </ROW>  
</BCPFORMAT>  
```  
  
> [!NOTE]  
>  Para obter um exemplo equivalente de [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] , veja [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md).  
  
###  <a name="d-mapping-field-xsitype-to-column-xsitype"></a><a name="MapXSItype"></a> D. Mapeando \<FIELD> xsi: Type para \<COLUMN> xsi: Type  
 O exemplo a seguir mostra tipos diferentes de campos e seu mapeamento para colunas.  
  
```  
<?xml version = "1.0"?>  
<BCPFORMAT  
xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
   <RECORD>  
      <FIELD xsi:type="CharTerm" ID="C1" TERMINATOR="\t"   
            MAX_LENGTH="4"/>  
      <FIELD xsi:type="CharFixed" ID="C2" LENGTH="10"   
         COLLATION="SQL_LATIN1_GENERAL_CP1_CI_AS"/>  
      <FIELD xsi:type="CharPrefix" ID="C3" PREFIX_LENGTH="2"   
         MAX_LENGTH="32" COLLATION="SQL_LATIN1_GENERAL_CP1_CI_AS"/>  
      <FIELD xsi:type="NCharTerm" ID="C4" TERMINATOR="\t"   
         MAX_LENGTH="4"/>  
      <FIELD xsi:type="NCharFixed" ID="C5" LENGTH="10"   
         COLLATION="SQL_LATIN1_GENERAL_CP1_CI_AS"/>  
      <FIELD xsi:type="NCharPrefix" ID="C6" PREFIX_LENGTH="2"   
         MAX_LENGTH="32" COLLATION="SQL_LATIN1_GENERAL_CP1_CI_AS"/>  
      <FIELD xsi:type="NativeFixed" ID="C7" LENGTH="4"/>  
   </RECORD>  
   <ROW>  
      <COLUMN SOURCE="C1" NAME="Age" xsi:type="SQLTINYINT"/>  
      <COLUMN SOURCE="C2" NAME="FirstName" xsi:type="SQLVARYCHAR"   
      LENGTH="16" NULLABLE="NO"/>  
      <COLUMN SOURCE="C3" NAME="LastName" />  
      <COLUMN SOURCE="C4" NAME="Salary" xsi:type="SQLMONEY"/>  
      <COLUMN SOURCE="C5" NAME="Picture" xsi:type="SQLIMAGE"/>  
      <COLUMN SOURCE="C6" NAME="Bio" xsi:type="SQLTEXT"/>  
      <COLUMN SOURCE="C7" NAME="Interest"xsi:type="SQLDECIMAL"   
      PRECISION="5" SCALE="3"/>  
   </ROW>  
</BCPFORMAT>  
```  
  
###  <a name="e-mapping-xml-data-to-a-table"></a><a name="MapXMLDataToTbl"></a> E. Mapear dados XML para uma tabela  
 O exemplo a seguir cria uma tabela de duas colunas vazias (`t_xml`), na qual a primeira coluna mapeia para o tipo de dados `int` e a segunda coluna mapeia para o tipo de dados `xml` .  
  
```  
CREATE TABLE t_xml (c1 int, c2 xml)  
```  
  
 O arquivo de formato XML a seguir carrega um arquivo de dados na tabela `t_xml`.  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
 <RECORD>  
  <FIELD ID="1" xsi:type="NativePrefix" PREFIX_LENGTH="1"/>  
  <FIELD ID="2" xsi:type="NCharPrefix" PREFIX_LENGTH="8"/>  
 </RECORD>  
 <ROW>  
  <COLUMN SOURCE="1" NAME="c1" xsi:type="SQLINT"/>  
  <COLUMN SOURCE="2" NAME="c2" xsi:type="SQLNCHAR"/>  
 </ROW>  
</BCPFORMAT>  
```  
  
###  <a name="f-importing-fixed-length-or-fixed-width-fields"></a><a name="ImportFixedFields"></a> F. Importar campos de comprimento fixo ou de largura fixa  
 O exemplo a seguir descreve campos fixos de `10` ou de `6` caracteres cada. O arquivo de formato representa o comprimento/largura desses campos como `LENGTH="10"` e `LENGTH="6"`, respectivamente. Cada linha dos arquivos de dados termina com uma combinação de alimentação de linha de retorno de carro, {CR}{LF}, que o arquivo de formato representa como `TERMINATOR="\r\n"`.  
  
```  
<?xml version="1.0"?>  
<BCPFORMAT  
       xmlns="https://schemas.microsoft.com/sqlserver/2004/bulkload/format"  
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  <RECORD>  
    <FIELD ID="1" xsi:type="CharFixed" LENGTH="10"/>  
    <FIELD ID="2" xsi:type="CharFixed" LENGTH="6"/>  
    <FIELD ID="3" xsi:type="CharTerm" TERMINATOR="\r\n"  
  </RECORD>  
  <ROW>  
    <COLUMN SOURCE="1" NAME="C1" xsi:type="SQLINT" />  
    <COLUMN SOURCE="2" NAME="C2" xsi:type="SQLINT" />  
  </ROW>  
</BCPFORMAT>  
```  
  
###  <a name="additional-examples"></a><a name="AdditionalExamples"></a> Exemplos adicionais  
 Para obter exemplos adicionais de arquivos de formato não XML e arquivos de formato XML, consulte os seguintes tópicos:  
  
-   [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Tarefas relacionadas  
  
-   [Criar um arquivo de formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [Usar um arquivo de formato para importação em massa de dados &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar uma coluna de tabela &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
-   [Usar um arquivo de formato para ignorar um campo de dados &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Usar um arquivo de formato para mapear colunas de uma tabela para campos de arquivo de dados &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
##  <a name="related-content"></a><a name="RelatedContent"></a> Conteúdo relacionado  
 Nenhum.  
  
## <a name="see-also"></a>Consulte Também  
 [Importação e exportação em massa de dados &#40;SQL Server&#41;](bulk-import-and-export-of-data-sql-server.md)   
 [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [Arquivos de formato não XML &#40;SQL Server&#41;](xml-format-files-sql-server.md)   
 [Arquivos de formato para importação ou exportação de dados &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)  
  
  
