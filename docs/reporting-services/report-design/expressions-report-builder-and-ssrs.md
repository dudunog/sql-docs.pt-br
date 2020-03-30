---
title: Expressões (Construtor de Relatórios) | Microsoft Docs
ms.date: 09/06/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 76d3ac86-650c-46fe-8086-8b3edcea3882
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8cff1f3e79c383dbcbfe365ab36d9fa6912d6e28
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77080365"
---
# <a name="expressions-report-builder-and-ssrs"></a>Expressões (Construtor de Relatórios e SSRS)
  As expressões são amplamente usadas em todos os relatórios paginados do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] para recuperar, calcular, exibir, agrupar, classificar, filtrar, parametrizar e formatar dados. 
  
  Várias propriedades de item de relatório podem ser definidas para uma expressão. Expressões ajudam a controlar o conteúdo, o design e a interatividade do seu relatório. As expressões são escritas em [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)], salvas na definição de relatório e avaliadas pelo processador de relatórios quando você executa o relatório.  
  
 Em aplicativos como o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel, você trabalha com dados diretamente em uma planilha. Já em um relatório, você trabalha com expressões que são espaços reservados de dados. Para ver os dados reais das expressões avaliadas, visualize o relatório. Quando você executa o relatório, o processador de relatório avalia cada expressão pois combina dados de relatório e elementos de layout de relatório, tais como tabelas e gráficos.  
  
 À medida que você cria um relatório, muitas expressões para itens de relatório são definidas. Por exemplo, quando você arrasta um campo do painel de dados para uma célula da tabela na superfície de design de relatório, o valor da caixa de texto é definido como uma expressão simples para o campo. Na figura a seguir, o painel Dados do Relatório exibe os campos do conjunto de dados ID, Name, SalesTerritory, Code e Sales. Três campos foram adicionados à tabela: [Name], [Code] e [Sales]. A notação [Name] na superfície de design representa a expressão subjacente `=Fields!Name.Value`.  
  
 ![rs_DataDesignandPreview](../../reporting-services/report-data/media/rs-datadesignandpreview.gif "rs_DataDesignandPreview")  
  
 Quando você visualiza o relatório, o processador de relatório combina a região de dados da tabela com os dados reais da conexão de dados e exibe uma linha na tabela para cada linha no conjunto de resultados.  
  
 Para inserir expressões manualmente, selecione um item na superfície de design, e use menus de atalho e caixas de diálogo para definir as propriedades do item. Quando você visualiza o botão ***(fx)*** ou o valor `<Expression>` em uma lista suspensa, sabe que pode definir a propriedade para uma expressão. Para obter mais informações, consulte [Adicionar uma expressão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-an-expression-report-builder-and-ssrs.md).  
  
 Para desenvolver expressões complexas ou expressões que usam código personalizado ou assemblies personalizados, recomendamos o uso do Designer de Relatórios no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para obter mais informações, consulte [Referências a código personalizado e assemblies em expressões no Designer de Relatórios &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="understanding-simple-and-complex-expressions"></a><a name="Types"></a> Compreendendo expressões simples e complexas  
 As expressões começam com o sinal de igual (=) e são gravadas no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. Elas podem incluir uma combinação de constantes, operadores e referências para valores internos (campos, coleções e funções) e para o código externo ou personalizado.  
  
 Você pode usar expressões para especificar o valor de muitas propriedades de item de relatório. As propriedades mais comuns são valores para caixas de texto e texto do espaço reservado. Normalmente, se uma caixa de texto contiver só uma expressão, a expressão será o valor da propriedade de caixa de texto. Se uma caixa de texto contiver várias expressões, cada expressão será o valor de texto do espaço reservado na caixa de texto.  
  
 Por padrão, expressões aparecem na superfície de design de relatório como *expressões simples* ou *expressões complexas*.  
  
-   **Simples** Uma expressão simples contém uma referência a um único item em uma coleção interna, como, por exemplo, um campo do conjunto de dados, um parâmetro ou um campo interno. Na superfície de design, uma expressão simples aparece entre colchetes. Por exemplo, `[FieldName]` corresponde à expressão subjacente `=Fields!FieldName.Value`. Expressões simples são criadas automaticamente à medida que você cria o layout de relatório e arrasta itens do painel de dados do relatório para a superfície de design. Para obter mais informações sobre os símbolos que representam coleções internas diferentes, consulte [Compreendendo símbolos de prefixo de expressões simples](#DisplayText).  
  
-   **Complexa** Uma expressão complexa contém referências a várias referências internas, operadores e chamadas de função. Uma expressão complexa é exibida como <\<Expr>> quando o valor de expressão inclui mais que uma referência simples. Para exibir a expressão, passe o mouse sobre ela e use a dica de ferramenta. Para editar a expressão, abra-a na caixa de diálogo **Expressão** .  
  
 A figura a seguir mostra expressões simples e complexas típicas para caixas de texto e texto do espaço reservado.  
  
 ![rs_ExpressionDefaultFormat](../../reporting-services/report-design/media/rs-expressiondefaultformat.gif "rs_ExpressionDefaultFormat")  
  
 Para exibir valores de exemplo em vez de texto para expressões, aplique a formatação à caixa de texto ou texto do espaço reservado. A seguinte figura mostra a superfície de design de relatório alternada para mostrar valores de exemplo:  
  
 ![rs_ExpressionSampleValuesFormat](../../reporting-services/report-design/media/rs-expressionsamplevaluesformat.gif "rs_ExpressionSampleValuesFormat")  
  
 Para obter mais informações, consulte [Formatando texto e espaços reservados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md).  
  
## <a name="understanding-prefix-symbols-in-simple-expressions"></a><a name="DisplayText"></a> Compreendendo símbolos de prefixo em expressões simples  

As expressões simples usam símbolos para indicar se a referência destina-se a um campo, a um parâmetro, a uma coleção interna ou à coleção ReportItems. A seguinte tabela mostra exemplos de texto de expressão e de exibição:  
  
|Item|Exemplo de texto de exibição|Exemplo de texto de expressão|  
|----------|--------------------------|-----------------------------|  
|Campos de conjunto de dados|`[Sales]`<br /><br /> `[SUM(Sales)]`<br /><br /> `[FIRST(Store)]`|`=Fields!Sales.Value`<br /><br /> `=Sum(Fields!Sales.Value)`<br /><br /> `=First(Fields!Store.Value)`|  
|Parâmetros de relatório|`[@Param]`<br /><br /> `[@Param.Label]`|`=Parameters!Param.Value`<br /><br /> `=Parameters!Param.Label`|  
|Campos internos|`[&ReportName]`|`=Globals!ReportName.Value`|  
|Caracteres literais usados no texto para exibição|`\[Sales\]`|`[Sales]`|  
  
##  <a name="writing-complex-expressions"></a><a name="References"></a> Escrevendo expressões complexas  
 Expressões podem incluir referências a funções, operadores, constantes, campos, parâmetros, itens das coleções internas, e ao código personalizado interno ou assemblies personalizados.  
  
> [!NOTE]
>  Para desenvolver expressões complexas ou expressões que usam código personalizado ou assemblies personalizados, recomendamos o uso do Designer de Relatórios no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para obter mais informações, consulte [Referências a código personalizado e assemblies em expressões no Designer de Relatórios &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
 A seguinte tabela lista os tipos de referências que podem ser incluídos em uma expressão:  
  
|Referências|DESCRIÇÃO|Exemplo|  
|----------------|-----------------|-------------|  
|[Constantes](../../reporting-services/report-design/constants-in-expressions-report-builder-and-ssrs.md)|Descreve as constantes acessadas interativamente para propriedades que exigem valores de constantes, tais como cores de fontes.|`="Blue"`|  
|[Operadores](../../reporting-services/report-design/operators-in-expressions-report-builder-and-ssrs.md)|Descreve os operadores a serem usados para combinar referências em uma expressão. Por exemplo, o operador **&** é usado para concatenar cadeias de caracteres.|`="The report ran at: " & Globals!ExecutionTime & "."`|  
|[Coleções internas](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)|Descreve as coleções internas que podem ser incluídas em uma expressão, tais como `Fields`, `Parameters`e `Variables`.|`=Fields!Sales.Value`<br /><br /> `=Parameters!Store.Value`<br /><br /> `=Variables!MyCalculation.Value`|  
|[Relatório interno e funções de agregação](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md)|Descreve as funções internas, tais como `Sum` ou `Previous`, que podem ser acessadas de uma expressão.|`=Previous(Sum(Fields!Sales.Value))`|  
|[Referências a código personalizado e assemblies em expressões no Designer de Relatórios &#40;SSRS&#41;](../../reporting-services/report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md)|Descreve como é possível acessar as classes CLR internas <xref:System.Math> e <xref:System.Convert>, outras classes CLR, funções da biblioteca em tempo de execução do [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] ou métodos de um assembly externo.<br /><br /> Descreve como é possível acessar o código personalizado que é inserido no relatório, ou que é compilado e instalado como um assembly personalizado no cliente de relatório e no servidor de relatório.|`=Sum(Fields!Sales.Value)`<br /><br /> `=CDate(Fields!SalesDate.Value)`<br /><br /> `=DateAdd("d",3,Fields!BirthDate.Value)`<br /><br /> `=Code.ToUSD(Fields!StandardCost.Value)`|  
   
##  <a name="validating-expressions"></a><a name="Valid"></a> Validando expressões  
 Quando você cria uma expressão para uma propriedade de item de relatório específica, as referências que podem ser incluídas em uma expressão dependem dos valores que a propriedade de item de relatório pode aceitar e do escopo em que a propriedade é avaliada. Por exemplo:  
  
-   Por padrão, a expressão [Sum] calcula a soma de dados que estão no escopo quando a expressão é avaliada. Para uma célula de tabela, o escopo depende das associações de grupo de linhas e colunas. Para obter mais informações, consulte [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
-   Para o valor de uma propriedade Font, o valor deve ser avaliado como o nome de uma fonte.  
  
-   A sintaxe da expressão é validada no tempo de design. A validação do escopo da expressão ocorre quando você publica o relatório. Para a validação que depende dos dados reais, erros só podem ser detectados no tempo de execução. Algumas dessas expressões geram #Error como uma mensagem de erro no relatório renderizado. Para ajudar a determinar os problemas desse tipo de erro, use o Designer de Relatórios no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. O Designer de Relatórios fornece uma janela de Saída que fornece mais informações sobre esses erros.  
  
 Para obter mais informações, consulte [Referência de expressões &#40;Construtor de Relatórios e SSRS &#41;](../../reporting-services/report-design/expression-reference-report-builder-and-ssrs.md).  
  
##  <a name="in-this-section"></a><a name="Section"></a> Nesta seção  
 [Adicionar uma expressão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add-an-expression-report-builder-and-ssrs.md)  
  
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)  
  
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
 [Referência de expressões &#40;Construtor de Relatórios e SSRS &#41;](../../reporting-services/report-design/expression-reference-report-builder-and-ssrs.md)  

## <a name="see-also"></a>Consulte Também
 Para obter mais informações e exemplos, consulte os seguintes tópicos:  
  
-   [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)  
-   [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)  
-   [Exemplos de equações de filtro &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md)  
-   [Exemplos de expressões de grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/group-expression-examples-report-builder-and-ssrs.md)  
-   [Tutorial: Apresentação de expressões](Tutorial:%20Introducing%20Expressions.md)
-   [Exemplos de relatório (Construtor de Relatórios e SSRS)](https://go.microsoft.com/fwlink/?LinkId=198283)  
  
