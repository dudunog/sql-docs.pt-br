---
title: '&lt;= (Menor ou igual a) (Expressão SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- <= (less than or equal to operator)
- less than or equal to operator (<=)
ms.assetid: 946c5630-dccf-4dae-9cfd-6ea823641ab2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 543c9580067ca94acf8c88156884d3be5c647481
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62897602"
---
# <a name="lt-less-than-or-equal-to-ssis-expression"></a>&lt;= (Menor ou igual a) (Expressão SSIS)
  Executa uma comparação para determinar se a primeira expressão é menor que ou igual à segunda. O avaliador de expressões converte automaticamente muitos tipos de dados antes de executar a comparação.  
  
> [!NOTE]  
>  Este operador não aceita comparações que usam os tipos de dados DT_TEXT, DT_NTEXT ou DT_IMAGE.  
  
 No entanto, alguns tipos de dados requerem que a expressão inclua uma conversão explícita antes de ser avaliada com êxito. Para obter mais informações sobre conversões legais entre tipos de dados, consulte [Conversão &#40;Expressão do SSIS&#41;](cast-ssis-expression.md).  
  
> [!NOTE]  
>  Não há nenhum espaço entre os dois caracteres neste operador.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
expression1 <= expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression1, expression2*  
 É qualquer expressão válida.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_BOOL  
  
## <a name="remarks"></a>Comentários  
 Se qualquer expressão na comparação for nula, o resultado da comparação será nulo. Se ambas as expressões forem nulas, o resultado será nulo.  
  
 O conjunto de expressões, *expression1* e *expression2*, deve seguir uma destas regras:  
  
-   **Numérico** Ambas *expression1* e *expression2* devem ser um tipo de dados numérico. A intersecção dos tipos de dados deve ser um tipo de dados numérico, como especificado nas regras sobre as conversões numéricas implícitas que o avaliador de expressões executa. A interseção dos dois tipos de dados numéricos não pode ser nula. Para obter mais informações, consulte [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md).  
  
-   **Character** Tanto *expression1* quanto *expression2* devem ser avaliadas como um tipo de dados DT_STR ou DT_WSTR. As duas expressões podem ser avaliadas como tipos de dados de cadeia diferentes.  
  
    > [!NOTE]  
    >  Comparações de cadeia de caracteres diferenciam maiúsculas de minúsculas, acentuação, kana e largura.  
  
-   **Date, Time, ou Date/Time** Tanto *expression1* quanto *expression2* devem ser avaliadas como um dos seguintes tipos de dados: DT_DBDATE, DT_DATE, DT_DBTIME, DT_DBTIME2, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAPMOFFSET ou DT_FILETIME.  
  
    > [!NOTE]  
    >  O sistema não aceita comparações entre uma expressão que avalia um tipo de dados de hora e uma expressão que avalia um tipo de dados de data ou data/hora. O sistema gera um erro.  
  
     Ao comparar as expressões, o sistema aplica as seguintes regras de conversão na ordem listada:  
  
    -   Quando as duas expressões avaliarem o mesmo tipo de dados, uma comparação daquele tipo de dados é executada.  
  
    -   Se uma expressão for um tipo de dados DT_DBTIMESTAMPOFFSET, a outra expressão será convertida implicitamente para DT_DBTIMESTAMPOFFSET, e uma comparação de DT_DBTIMESTAMPOFFSET será executada. Para obter mais informações, consulte [Integration Services Data Types in Expressions](integration-services-data-types-in-expressions.md).  
  
    -   Se uma expressão for um tipo de dados DT_DBTIMESTAMP2, a outra expressão será convertida implicitamente para DT_DBTIMESTAMP2, e uma comparação de DT_DBTIMESTAMP2 será executada.  
  
    -   Se uma expressão for um tipo de dados DT_DBTIME2, a outra expressão será convertida implicitamente para DT_DBTIME2, e uma comparação de DT_DBTIME2 será executada.  
  
    -   Se uma expressão for de um tipo diferente de DT_DBTIMESTAMPOFFSET, DT_DBTIMESTAMP2 ou DT_DBTIME2, as expressões serão convertidas para o tipo de dados DT_DBTIMESTAMP antes de serem comparadas.  
  
     Ao comparar as expressões, o sistema faz as seguintes suposições:  
  
    -   Se cada expressão for um tipo de dados que inclui segundos fracionais, o sistema assumirá que o tipo de dados com o número de dígitos mínimo para os segundos fracionais tem zeros nos dígitos restantes.  
  
    -   Se cada expressão for um tipo de dados de data, mas somente um tiver um deslocamento de fuso horário, o sistema assumirá que o tipo de dados de data sem o deslocamento de fuso horário estará em UTC (Tempo Universal Coordenado).  
  
 Para obter mais informações sobre tipos de dados, consulte [Integration Services Data Types](../data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Exemplos de expressões  
 Este exemplo será avaliado como TRUE se a data atual for 4 de julho de 2003 ou posterior. Para obter mais informações, consulte [GETDATE &#40;Expressão SSIS&#41;](getdate-ssis-expression.md).  
  
```  
"7/4/2003" <= GETDATE()  
```  
  
 Este exemplo será avaliado como TRUE se o valor na coluna **ListPrice** for menor que ou igual a 500.  
  
```  
ListPrice <= 500  
```  
  
 Este exemplo avalia a variável **LPrice** e será avaliado como TRUE se o valor for menor que ou igual a 500. O tipo de dados **LPrice** deve ser numérico para que a expressão seja analisada.  
  
```  
@LPrice <= 500  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#62; &#40;Maior que&#41; &#40;Expressão SSIS&#41;](greater-than-ssis-expression.md)   
 [&#60; &#40;Menor que&#41; &#40;Expressão SSIS&#41;](less-than-ssis-expression.md)   
 [&#62;= &#40;Maior ou igual a&#41; &#40;Expressão SSIS&#41;](greater-than-or-equal-to-ssis-expression.md)   
 [Precedência de operador e capacidade de associação](operator-precedence-and-associativity.md)   
 [Operadores &#40;Expressão do SSIS&#41;](operators-ssis-expression.md)  
  
  
