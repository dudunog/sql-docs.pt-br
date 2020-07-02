---
title: XQuery e digitação estática | Microsoft Docs
description: Saiba mais sobre a inferência de tipos estáticos e a verificação de tipo estático no XQuery.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, static typing
- static typing
- checking static types
- inference [XQuery]
ms.assetid: d599c791-200d-46f8-b758-97e761a1a5c0
author: rothja
ms.author: jroth
ms.openlocfilehash: 1a0b9cf43331e45d4aa1253fe5ad4b90d0bbea92
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85775460"
---
# <a name="xquery-and-static-typing"></a>XQuery e digitação estática
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  O XQuery no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] é uma linguagem estaticamente digitada. Ou seja, ele gera erros de tipo durante a compilação de consulta quando uma expressão retornar um valor que tenha um tipo ou cardinalidade que não sejam aceitos por determinada função ou operador. Além disso, a verificação de tipo estático também poderá detectar se uma expressão de caminho em um documento XML digitado tiver sido digitada incorretamente. O compilador do XQuery primeiro aplica a fase de normalização que adiciona as operações implícitas, como atomização e, em seguida, executa a inferência e a verificação de tipo estático.  
  
## <a name="static-type-inference"></a>Inferência de tipo estático  
 A inferência de tipo estático determina o tipo de retorno de uma expressão. Ela determina isso considerando os tipos estáticos dos parâmetros de entrada e a semântica estática da operação e inferindo o tipo estático do resultado. Por exemplo, o tipo estático da expressão 1 + 2,3 é determinado da seguinte forma:  
  
-   O tipo estático de 1 é **xs: integer** e o tipo estático de 2,3 é **xs: decimal**. Com base na semântica dinâmica, a semântica estática da **+** operação converte o inteiro em um decimal e, em seguida, retorna um decimal. O tipo estático inferido seria então **xs: decimal**.  
  
 Para instâncias XML não digitadas, há tipos especiais para indicar que os dados não foram digitados. Essas informações são usadas durante a verificação de tipo estático e para executar determinadas conversões implícitas.  
  
 Para dados digitados, o tipo de entrada é inferido da coleção de esquemas XML que restringe a instância do tipo de dados XML. Por exemplo, se o esquema permitir apenas elementos do tipo **xs: integer**, os resultados de uma expressão de caminho usando esse elemento serão zero ou mais elementos do tipo **xs: integer**. Atualmente, isso é expresso usando uma expressão como, por exemplo, `element(age,xs:integer)*` onde o asterisco ( \* ) indica a cardinalidade do tipo resultante. Neste exemplo, a expressão pode resultar em zero ou mais elementos de Name "Age" e tipo **xs: integer**. Outras cardinalidade são exatamente uma e são expressas com o uso do nome de tipo, zero ou uma, e expressas usando um ponto de interrogação (**?**) e 1 ou mais e expressas usando um sinal de adição ( **+** ).  
  
 Às vezes, a inferência de tipo estático pode deduzir que uma expressão sempre retornará a sequência vazia. Por exemplo, se uma expressão de caminho em um tipo de dados XML tipado procurar um \<name> elemento dentro de um \<customer> elemento (/Customer/Name), mas o esquema não permitir um \<name> dentro de \<customer> , a inferência de tipo estático inferirá que o resultado estará vazio. Isso será usado para detectar consultas incorretas e será relatado como um erro estático, a menos que a expressão tenha sido () ou **dados (())**.  
  
 As regras de inferência detalhadas são fornecidas na semântica formal da especificação XQuery. A Microsoft somente as modificou levemente para que funcionem com instâncias do tipo de dados XML digitados. A mudança mais importante do padrão é que o nó de documento implícito sabe sobre o tipo da instância do tipo de dados XML. Consequentemente, uma expressão de caminho da forma /age será digitada precisamente com base nessas informações.  
  
 Usando [modelos e permissões do SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md), você pode ver os tipos estáticos retornados como parte das compilações de consulta. Para vê-los, o seu rastreamento deve incluir o evento de tipo estático do XQuery na categoria de eventos TSQL.  
  
## <a name="static-type-checking"></a>Verificação de tipo estático  
 A verificação de tipo estático assegura que a execução do tempo de execução só receberá valores que sejam o tipo apropriado para a operação. Como os tipos não precisam ser verificados no tempo de execução, os erros em potencial podem ser detectados erros precocemente na compilação. Isso ajuda a melhorar o desempenho. No entanto, a digitação estática requer que o autor da consulta tenha mais cuidado ao formular uma consulta.  
  
 A seguir, são apresentados os tipos apropriados que podem ser usados:  
  
-   Tipos explicitamente permitidos por uma função ou operação.  
  
-   Um subtipo de um tipo explicitamente permitido.  
  
 Os subtipos são definidos, com base nas regras de subdigitação por usar derivação por restrição ou extensão do esquema XML. Por exemplo, um tipo S é um subtipo do tipo T, se todos os valores que tiverem o tipo S também forem instâncias do tipo T.  
  
 Além disso, todos os valores inteiros também são valores decimais com base na hierarquia do tipo de esquemas XML. No entanto, nem todos os valores decimais são inteiros. Portanto, um inteiro é um subtipo de decimal, mas não vice-versa. Por exemplo, a **+** operação só permite valores de determinados tipos, como os tipos numéricos **xs: integer**, **xs: decimal**, **xs: float**e **xs: Double**. Se os valores de outros tipos, como **xs: String**, forem passados, a operação gerará um erro de tipo. Isso será referido como digitação forte. Os valores de outros tipos, como o tipo atômico usado para indicar XML não digitado, podem ser convertidos implicitamente em um valor de um tipo que a operação aceite. Isso é referido como digitação fraca.  
  
 Se for necessário depois de uma conversão implícita, a verificação de tipo estático garantirá que somente valores dos tipos permitidos com a cardinalidade correta serão passados em uma operação. Para "String" + 1, ele reconhece que o tipo estático de "String" é **xs: String**. Como esse não é um tipo permitido para a **+** operação, um erro de tipo é gerado.  
  
 No caso de adicionar o resultado de uma expressão arbitrária E1 a uma expressão arbitrária E2 (E1 + E2), a inferência de tipo estático determina os tipos estáticos de E1 e E2 primeiro e, em seguida, verifica os tipos estáticos com os tipos permitidos para a operação. Por exemplo, se o tipo estático de E1 puder ser um **xs: String** ou um **xs: integer**, a verificação de tipo estático gerará um erro de tipo, mesmo que alguns valores em tempo de execução possam ser inteiros. O mesmo seria o caso se o tipo estático de E1 fosse **xs: integer&#42;**. Como a **+** operação aceita apenas exatamente um valor inteiro e E1 pode retornar zero ou mais de 1, a verificação de tipo estático gera um erro.  
  
 Como mencionado anteriormente, a inferência de tipo frequentemente infere um tipo que é mais amplo do que aquilo que o usuário sabe sobre o tipo de dados sendo passados. Nesses casos, o usuário precisa reescrever a consulta. Alguns casos característicos incluem o seguinte:  
  
-   O tipo infere um tipo mais geral, como um supertipo ou uma união de tipos. Se o tipo for um tipo atômico, você deve usar a expressão de conversão ou função de construtor para indicar o tipo estático real. Por exemplo, se o tipo inferido da expressão E1 for uma opção entre **xs: String** ou **xs: integer** e a adição exigir **xs: integer**, você deverá escrever `xs:integer(E1) + E2` em vez de `E1+E2` . Essa expressão poderá falhar em tempo de execução se for encontrado um valor de cadeia de caracteres que não possa ser convertido em **xs: integer**. No entanto, a expressão agora passará a verificação de tipo estático. Essa expressão é mapeada para a sequência vazia.  
  
-   O tipo infere uma cardinalidade superior àquela que os dados realmente contêm. Isso ocorre com frequência, porque o tipo de dados **XML** pode conter mais de um elemento de nível superior, e uma coleção de esquemas XML não pode restringir isso. Para reduzir o tipo estático e garantir que realmente haja um valor máximo sendo passado, você deve usar o predicado posicional `[1]`. Por exemplo, para adicionar 1 ao valor do atributo `c` do elemento `b` no elemento de nível superior, é necessário `write (/a/b/@c)[1]+1`. Além disso, uma palavra-chave DOCUMENT pode ser usada junto com uma coleção de esquemas XML.  
  
-   Algumas operações perdem informações de tipo durante a inferência. Por exemplo, se o tipo de um nó não puder ser determinado, ele se tornará **anyType**. Isso não é convertido implicitamente em qualquer outro tipo. Tais conversões ocorrem mais notavelmente durante a navegação usando o eixo pai. Você deve evitar o uso de tais operações e reescrever a consulta, se a expressão for criar um erro de tipo estático.  
  
## <a name="type-checking-of-union-types"></a>Verificação de tipo de tipos de união  
 Os tipos de união requerem o tratamento cuidadoso devido à verificação de tipo. São ilustrados dois dos problemas nos exemplos a seguir.  
  
### <a name="example-function-over-union-type"></a>Exemplo: função em relação ao tipo de união  
 Considere uma definição de elemento para <`r`> de um tipo de União:  
  
```  
<xs:element name="r">  
<xs:simpleType>  
   <xs:union memberTypes="xs:int xs:float xs:double"/>  
</xs:simpleType>  
</xs:element>  
```  
  
 No contexto do XQuery, a função "Average" `fn:avg (//r)` retorna um erro estático, pois o compilador XQuery não pode adicionar valores de tipos diferentes (**xs: int**, **xs: float** ou **xs: Double**) para o <`r`> elementos no argumento de **fn: AVG ()**. Para solucionar isso, reescreva a invocação de função como `fn:avg(for $r in //r return $r cast as xs:double ?)`.  
  
### <a name="example-operator-over-union-type"></a>Exemplo: operador em relação ao tipo de união  
 A operação de adição ('+') requer tipos precisos dos operandos. Como resultado, a expressão `(//r)[1] + 1` retorna um erro estático que tem a definição de tipo descrita anteriormente para o elemento <`r`>. Uma solução é reescrevê-la como `(//r)[1] cast as xs:int? +1`, onde o “?” " indica 0 ou 1 ocorrência. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] exige "cast as" com "?", pois qualquer conversão pode causar a sequência vazia como resultado de erros em tempo de execução.  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de linguagem XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
