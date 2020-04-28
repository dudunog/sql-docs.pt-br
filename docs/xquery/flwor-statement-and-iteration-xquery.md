---
title: Instrução e iteração de FLWOR (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- return clause
- FLWOR statement
- effective Boolean value [XQuery]
- multiple variable binding
- order by clause [XQuery]
- for clause [XQuery]
- where clause [XQuery]
- iterations [XQuery]
- XQuery, FLWOR statement
- EBV
ms.assetid: d7cd0ec9-334a-4564-bda9-83487b6865cb
author: rothja
ms.author: jroth
ms.openlocfilehash: 9deb87d506e167d3de3439e0a07cfbb8bc040fac
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68038906"
---
# <a name="flwor-statement-and-iteration-xquery"></a>Iteração e instrução FLWOR (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  O XQuery define uma sintaxe de iteração FLWOR. FLWOR é o acrônimo para `for`, `let`, `where`, `order by` e `return`.  
  
 Uma instrução FLWOR é composta pelas seguintes partes:  
  
-   Uma ou mais cláusulas FOR que associam uma ou mais variáveis de iterador para sequências de entrada.  
  
     As sequências de entrada podem ser outras expressões XQuery, como expressões XPath. Elas são sequências de nós ou sequências de valores atômicos. Podem ser construídas sequências de valor atômico usando funções literais ou de construtor. Os nós XML construídos não são permitidos como sequências de entrada no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Uma cláusula `let` opcional. Essa cláusula atribui um valor à determinada variável para uma iteração específica. A expressão atribuída pode ser uma expressão Xquery, como uma expressão Xpath, e pode retornar uma sequência de nós ou uma sequência de valores atômicos. As sequências de valor atômico podem ser construídas usando funções literais ou de construtor. Os nós XML construídos não são permitidos como sequências de entrada no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   Uma variável de iterador. Essa variável pode ter uma asserção de tipo opcional usando a palavra-chave `as`.  
  
-   Uma cláusula `where` opcional. Essa cláusula aplica um predicado de filtro na iteração.  
  
-   Uma cláusula `order by` opcional.  
  
-   Uma expressão `return`. A expressão na cláusula `return` constrói o resultado da instrução FLWOR.  
  
 Por exemplo, a consulta a seguir itera sobre o <`Step`> elementos no primeiro local de fabricação e retorna o valor de cadeia de caracteres `Step` do <nós>:  
  
```sql
declare @x xml  
set @x='<ManuInstructions ProductModelID="1" ProductModelName="SomeBike" >  
<Location LocationID="L1" >  
  <Step>Manu step 1 at Loc 1</Step>  
  <Step>Manu step 2 at Loc 1</Step>  
  <Step>Manu step 3 at Loc 1</Step>  
</Location>  
<Location LocationID="L2" >  
  <Step>Manu step 1 at Loc 2</Step>  
  <Step>Manu step 2 at Loc 2</Step>  
  <Step>Manu step 3 at Loc 2</Step>  
</Location>  
</ManuInstructions>'  
SELECT @x.query('  
   for $step in /ManuInstructions/Location[1]/Step  
   return string($step)  
')  
```  
  
 Este é o resultado:  
  
```  
Manu step 1 at Loc 1 Manu step 2 at Loc 1 Manu step 3 at Loc 1  
```  
  
 A consulta a seguir é semelhante à anterior, exceto que é especificada em relação à coluna Instructions, uma coluna xml digitada, da tabela ProductModel. A consulta itera em todas as etapas de fabricação, <`step` elementos de>, no primeiro local do centro de trabalho para um produto específico.  
  
```sql
SELECT Instructions.query('  
   declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $Step in //AWMI:root/AWMI:Location[1]/AWMI:step  
      return  
           string($Step)   
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A `$Step` é a variável de iterador.  
  
-   A [expressão](../xquery/path-expressions-xquery.md)de caminho `//AWMI:root/AWMI:Location[1]/AWMI:step`,, gera a sequência de entrada. Essa sequência é a sequência do <`step` nó de elemento> filhos do primeiro <`Location` nó de elemento>.  
  
-   A cláusula de predicado opcional, `where`, não é usada.  
  
-   A `return` expressão retorna um valor de cadeia de caracteres `step` do elemento <>.  
  
 A [função de cadeia de caracteres (XQuery)](../xquery/data-accessor-functions-string-xquery.md) é usada para recuperar o valor da `step` cadeia de caracteres do <> nó.  
  
 Este é o resultado parcial:  
  
```  
Insert aluminum sheet MS-2341 into the T-85A framing tool.   
Attach Trim Jig TJ-26 to the upper and lower right corners of   
the aluminum sheet. ....         
```  
  
 Estes são exemplos de sequências de entrada adicionais permitidas:  
  
```sql
declare @x xml  
set @x=''  
SELECT @x.query('  
for $a in (1, 2, 3)  
  return $a')  
-- result = 1 2 3   
  
declare @x xml  
set @x=''  
SELECT @x.query('  
for $a in   
   for $b in (1, 2, 3)  
      return $b  
return $a')  
-- result = 1 2 3  
  
declare @x xml  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('  
  for $a in (xs:string( "test"), xs:double( "12" ), data(/ROOT/a ))  
  return $a')  
-- result test 12 111  
```  
  
 No [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], não são permitidas sequências heterogêneas. Especificamente, não são permitidas sequências que tenham uma combinação de valores atômicos e nós.  
  
 A iteração é frequentemente usada junto com a sintaxe de [construção XML](../xquery/xml-construction-xquery.md) na transformação de formatos XML, conforme mostrado na próxima consulta.  
  
 No banco de dados de exemplo AdventureWorks, as instruções de fabricação armazenadas na coluna **instruções** da tabela **Production. ProductModel** têm o seguinte formato:  
  
```xml
<Location LocationID="10" LaborHours="1.2"   
            SetupHours=".2" MachineHours=".1">  
  <step>describes 1st manu step</step>  
   <step>describes 2nd manu step</step>  
   ...  
</Location>  
...  
```  
  
 A consulta a seguir constrói um novo XML que tem os `Location` elementos de> de <com os atributos de local do centro de trabalho retornados como elementos filho:  
  
```xml
<Location>  
   <LocationID>10</LocationID>  
   <LaborHours>1.2</LaborHours>  
   <SetupHours>.2</SetupHours>  
   <MachineHours>.1</MachineHours>  
</Location>  
...  
```  
  
 Esta é a consulta:  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $WC in /AWMI:root/AWMI:Location  
        return  
          <Location>  
            <LocationID> { data($WC/@LocationID) } </LocationID>  
            <LaborHours>   { data($WC/@LaborHours) }   </LaborHours>  
            <SetupHours>   { data($WC/@SetupHours) }   </SetupHours>  
            <MachineHours> { data($WC/@MachineHours) } </MachineHours>  
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A instrução FLWOR recupera uma sequência de <`Location`> elementos para um produto específico.  
  
-   A [função de dados (XQuery)](../xquery/data-accessor-functions-data-xquery.md) é usada para extrair o valor de cada atributo, de modo que eles serão adicionados ao XML resultante como nós de texto em vez de como atributos.  
  
-   A expressão na cláusula RETURN constrói o XML desejado.  
  
 Este é um resultado parcial:  
  
```xml
<Location>  
  <LocationID>10</LocationID>  
  <LaborHours>2.5</LaborHours>  
  <SetupHours>0.5</SetupHours>  
  <MachineHours>3</MachineHours>  
</Location>  
<Location>  
   ...  
<Location>  
...  
```  
  
## <a name="using-the-let-clause"></a>Usando a cláusula let  
 Você pode usar a cláusula `let` para nomear expressões repetidas as quais é possível fazer referência quando referir-se à variável. A expressão atribuída a uma variável `let` é inserida na consulta toda vez que a variável é referenciada na consulta. Isso significa que a instrução será executada tantas vezes quantas forem as referências à expressão.  
  
 No banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)], as instruções de fabricação contêm informações sobre as ferramentas necessárias e o local em que elas são usadas. A consulta a seguir usa a cláusula `let` para listar as ferramentas necessárias para construir o modelo de produção, assim como os locais em que cada ferramenta é necessária.  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
        for $T in //AWMI:tool  
            let $L := //AWMI:Location[.//AWMI:tool[.=data($T)]]  
        return  
          <tool desc="{data($T)}" Locations="{data($L/@LocationID)}"/>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
## <a name="using-the-where-clause"></a>Usando a cláusula where  
 Você pode usar a `where` cláusula para filtrar os resultados de uma iteração. Isso é ilustrado no exemplo a seguir.  
  
 Na fabricação de uma bicicleta, o processo de produção passa por uma série de locais do centro de trabalho. Cada local do centro de trabalho define uma sequência de etapas de produção. A consulta a seguir recupera somente os locais do centro de trabalho que fabricam um modelo de bicicleta e têm menos de três etapas de produção. Ou seja, eles têm menos de três <`step` elementos de>.  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location  
      where count($WC/AWMI:step) < 3  
      return  
          <Location >  
           { $WC/@LocationID }   
          </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A `where` palavra-chave usa a função **Count ()** para contar o número `step` de <> elementos filho em cada local do centro de trabalho.  
  
-   A expressão `return` constrói o XML desejado a partir dos resultados da iteração.  
  
 Este é o resultado:  
  
```  
<Location LocationID="30"/>   
```  
  
 O resultado da expressão na cláusula `where` é convertido em um valor Booliano usando as regras a seguir, na ordem especificada. Essas são as mesmas regras para predicados em expressões de caminho, exceto que não são permitidos inteiros:  
  
1.  Se a expressão `where` retornar uma sequência vazia, seu valor Booliano efetivo será False.  
  
2.  Se a expressão `where` retornar um valor de tipo Booliano simples, esse valor será o valor Booliano efetivo.  
  
3.  Se a expressão `where` retornar uma sequência que contém pelo menos um nó, o valor Booliano efetivo será True.  
  
4.  Caso contrário, ele gera um erro estático.  
  
## <a name="multiple-variable-binding-in-flwor"></a>Associação de variável múltipla em FLWOR  
 Você pode ter uma única expressão FLWOR que associa diversas variáveis a sequências de entrada. No exemplo a seguir, a consulta é especificada em uma coluna xml não digitada. A expressão do FLUÍdor retorna a primeira `Step` <> filho do elemento em `Location` cada elemento de> <.  
  
```sql
declare @x xml  
set @x='<ManuInstructions ProductModelID="1" ProductModelName="SomeBike" >  
<Location LocationID="L1" >  
  <Step>Manu step 1 at Loc 1</Step>  
  <Step>Manu step 2 at Loc 1</Step>  
  <Step>Manu step 3 at Loc 1</Step>  
</Location>  
<Location LocationID="L2" >  
  <Step>Manu step 1 at Loc 2</Step>  
  <Step>Manu step 2 at Loc 2</Step>  
  <Step>Manu step 3 at Loc 2</Step>  
</Location>  
</ManuInstructions>'  
SELECT @x.query('  
   for $Loc in /ManuInstructions/Location,  
       $FirstStep in $Loc/Step[1]  
   return   
       string($FirstStep)  
')  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A `for` expressão define `$Loc` e $`FirstStep` Variables.  
  
-   As expressões `two`, `/ManuInstructions/Location` e `$FirstStep in $Loc/Step[1]`, são correlacionadas pelo fato de que os valores de `$FirstStep` dependem dos valores de `$Loc`.  
  
-   A expressão associada a `$Loc` gera uma sequência de <`Location` elementos de>. Para cada <`Location` elemento>, `$FirstStep` gera uma sequência de um <`Step` elemento>, um singleton.  
  
-   `$Loc` é especificado na expressão associada com a variável `$FirstStep`.  
  
 Este é o resultado:  
  
```  
Manu step 1 at Loc 1   
Manu step 1 at Loc 2  
```  
  
 A consulta a seguir é semelhante, exceto que é especificada na coluna instruções, coluna **XML** com tipo, da tabela **ProductModel** . A [construção XML (XQuery)](../xquery/xml-construction-xquery.md) é usada para gerar o XML desejado.  
  
```sql
SELECT Instructions.query('  
     declare default element namespace "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /root/Location,  
            $S  in $WC/step  
      return  
          <Step LocationID= "{$WC/@LocationID }" >  
            { $S/node() }  
          </Step>  
') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A cláusula `for` define duas variáveis, `$WC` e `$S`. A expressão associada com `$WC` gera uma sequência de locais de centro de trabalho na fabricação de um modelo do produto de bicicleta. A expressão de caminho atribuída à variável `$S` gera uma sequência de etapas para cada sequência de local do centro de trabalho no `$WC`.  
  
-   A instrução return constrói XML que tem um elemento <`Step`> que contém a etapa de fabricação e o **LocationID** como seu atributo.  
  
-   O **namespace de elemento padrão declare** é usado no prólogo XQuery para que todas as declarações de namespace no XML resultante apareçam no elemento de nível superior. Isso torna o resultado mais legível. Para obter mais informações sobre namespaces padrão, consulte [manipulando namespaces em XQuery](../xquery/handling-namespaces-in-xquery.md).  
  
 Este é o resultado parcial:  
  
```xml
<Step xmlns=  
    "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"     
  LocationID="10">  
     Insert <material>aluminum sheet MS-2341</material> into the <tool>T-   
     85A framing tool</tool>.   
</Step>  
...  
<Step xmlns=  
      "https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"     
    LocationID="20">  
        Assemble all frame components following blueprint   
        <blueprint>1299</blueprint>.  
</Step>  
...  
```  
  
## <a name="using-the-order-by-clause"></a>Usando a cláusula order by  
 A classificação no XQuery é executada usando a cláusula `order by` na expressão FLWOR. As expressões de classificação passadas `order by` para a cláusula devem retornar valores cujos tipos são válidos para o operador **gt** . Cada expressão de classificação deve resultar em uma sequência singleton com um item. Por padrão, a classificação é executada em ordem crescente. Você pode especificar opcionalmente a ordem crescente ou decrescente para cada expressão de classificação.  
  
> [!NOTE]  
>  A classificação de comparações em valores da cadeia de caracteres executada pela implementação do XQuery no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] sempre é realizada usando a ordenação Unicode Codepoint binário.  
  
 A consulta a seguir recupera todos os números de telefone de um determinando cliente da coluna AdditionalContactInfo. Os resultados são classificados pelo número de telefone.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT AdditionalContactInfo.query('  
   declare namespace act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes";  
   declare namespace aci="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo";  
   for $a in /aci:AdditionalContactInfo//act:telephoneNumber   
   order by $a/act:number[1] descending  
   return $a  
') As Result  
FROM Person.Person  
WHERE BusinessEntityID=291;  
```  
  
 Observe que o processo de [atomização (XQuery)](../xquery/atomization-xquery.md) recupera o valor atômico do <`number`> elementos antes de passá- `order by`lo para. Você pode escrever a expressão usando a função **Data ()** , mas isso não é necessário.  
  
```  
order by data($a/act:number[1]) descending  
```  
  
 Este é o resultado:  
  
```xml
<act:telephoneNumber xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3334</act:number>  
</act:telephoneNumber>  
<act:telephoneNumber xmlns:act="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3333</act:number>  
</act:telephoneNumber>  
```  
  
 Em vez de declarar os namespaces no prólogo da consulta, você pode declará-los usando WITH XMLNAMESPACES.  
  
```sql
WITH XMLNAMESPACES (  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo'  AS aci)  
  
SELECT AdditionalContactInfo.query('  
   for $a in /aci:AdditionalContactInfo//act:telephoneNumber   
   order by $a/act:number[1] descending  
   return $a  
') As Result  
FROM Person.Person  
WHERE BusinessEntityID=291;  
```  
  
 Também é possível a classificação por valor do atributo. Por exemplo, a consulta a seguir recupera os elementos de `Location`> <recém-criados que têm os atributos LocationID e LaborHours classificados pelo atributo LaborHours em ordem decrescente. Consequentemente, os locais do centro de trabalho com o maior número de horas de trabalho são retornados primeiro.  
  
```sql
SELECT Instructions.query('  
     declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location   
order by $WC/@LaborHours descending  
        return  
          <Location>  
             { $WC/@LocationID }   
             { $WC/@LaborHours }   
          </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7;  
```  
  
 Este é o resultado:  
  
```  
<Location LocationID="60" LaborHours="4"/>  
<Location LocationID="50" LaborHours="3"/>  
<Location LocationID="10" LaborHours="2.5"/>  
<Location LocationID="20" LaborHours="1.75"/>  
<Location LocationID="30" LaborHours="1"/>  
<Location LocationID="45" LaborHours=".5"/>  
```  
  
 Na consulta a seguir, os resultados são classificados por nome de elemento. A consulta recupera as especificações de um produto específico do catálogo de produtos. As especificações são os filhos do elemento <`Specifications`>.  
  
```sql
SELECT CatalogDescription.query('  
     declare namespace  
 pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $a in /pd:ProductDescription/pd:Specifications/*   
     order by local-name($a)  
      return $a  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19;  
```  
  
 Observe o seguinte na consulta anterior:  
  
-   A `/p1:ProductDescription/p1:Specifications/*` expressão retorna os filhos do elemento `Specifications` de <>.  
  
-   A expressão `order by (local-name($a))` classifica a sequência pela parte local do nome de elemento.  
  
 Este é o resultado:  
  
```xml
<Color>Available in most colors</Color>  
<Material>Almuminum Alloy</Material>  
<ProductLine>Mountain bike</ProductLine>  
<RiderExperience>Advanced to Professional riders</RiderExperience>  
<Style>Unisex</Style>    
```  
  
 Os nós em que a expressão de classificação retorna vazia são classificados no início da sequência, como mostrado no exemplo a seguir:  
  
```sql
declare @x xml  
set @x='<root>  
  <Person Name="A" />  
  <Person />  
  <Person Name="B" />  
</root>  
'  
select @x.query('  
  for $person in //Person  
  order by $person/@Name  
  return   $person  
')  
```  
  
 Este é o resultado:  
  
```xml
<Person />  
<Person Name="A" />  
<Person Name="B" />  
```  
  
 Você pode especificar vários critérios de classificação, como mostrado no exemplo a seguir. A consulta neste exemplo classifica <`Employee` elementos de> primeiro por título e, em seguida, por valores de atributo de administrador.  
  
```sql
declare @x xml  
set @x='<root>  
  <Employee ID="10" Title="Teacher"        Gender="M" />  
  <Employee ID="15" Title="Teacher"  Gender="F" />  
  <Employee ID="5" Title="Teacher"         Gender="M" />  
  <Employee ID="11" Title="Teacher"        Gender="F" />  
  <Employee ID="8" Title="Administrator"   Gender="M" />  
  <Employee ID="4" Title="Administrator"   Gender="F" />  
  <Employee ID="3" Title="Teacher"         Gender="F" />  
  <Employee ID="125" Title="Administrator" Gender="F" /></root>'  
SELECT @x.query('for $e in /root/Employee  
order by $e/@Title ascending, $e/@Gender descending  
  
  return  
     $e  
')  
```  
  
 Este é o resultado:  
  
```xml
<Employee ID="8" Title="Administrator" Gender="M" />  
<Employee ID="4" Title="Administrator" Gender="F" />  
<Employee ID="125" Title="Administrator" Gender="F" />  
<Employee ID="10" Title="Teacher" Gender="M" />  
<Employee ID="5" Title="Teacher" Gender="M" />  
<Employee ID="11" Title="Teacher" Gender="F" />  
<Employee ID="15" Title="Teacher" Gender="F" />  
<Employee ID="3" Title="Teacher" Gender="F" />  
```  
  
### <a name="implementation-limitations"></a>Limitações de implementação  
 Estas são as limitações:  
  
-   As expressões de classificação devem ser digitadas homogeneamente. Isso é verificado estaticamente.  
  
-   A classificação de sequências vazias não pode ser controlada.  
  
-   Não há suporte para as palavras-chave menos vazio, mais vazio e ordenação em `order by`  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões XQuery](../xquery/xquery-expressions.md)  
  
  
