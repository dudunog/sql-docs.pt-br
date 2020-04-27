---
title: 'Tutorial: Formatar texto (Construtor de Relatórios) | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 67d8513e-8a70-464b-b87f-e91d010cfd82
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dc58232ed3025063fb329392b58895ed667465f4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66098897"
---
# <a name="tutorial-format-text-report-builder"></a>Tutorial: Formatar texto (Construtor de Relatórios)
  Neste tutorial, você pode praticar a formatação de texto de várias maneiras. Depois de configurar o relatório em branco com a fonte de dados e o conjunto de dados, é possível escolher e selecionar as etapas que você deseja explorar.  
  
 A ilustração a seguir mostra um relatório semelhante ao que você criará.  
  
 ![rs_FormatTextFinal](../../2014/tutorials/media/rs-formattextfinal.gif "rs_FormatTextFinal")  
  
 Em uma etapa, você comete um erro de propósito, para poder ver o porquê do erro. Em seguida, você corrige o erro para obter o efeito desejado.  
  
 Uma versão aprimorada do relatório criado por você neste tutorial está disponível como um relatório de exemplo do Construtor de Relatórios da [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Para obter mais informações sobre como baixar este relatório de exemplo e outros, consulte [Construtor de relatórios relatórios de exemplo](https://go.microsoft.com/fwlink/?LinkId=184851).  
  
##  <a name="what-you-will-learn"></a><a name="BackToTop"></a>O que você aprenderá  
  
### <a name="set-up-the-report"></a>Configurar o relatório  
 1. [Criar um relatório em branco com uma fonte de dados e um conjunto de dados](#CreateReport)  
  
 2. [Adicionar um campo à superfície de design do relatório (incorretamente e, em seguida, corretamente)](#AddField)  
  
 3. [Adicionar uma tabela ao Design Surface do relatório](#AddTable)  
  
### <a name="pick-and-choose"></a>Escolher e selecionar  
 [Adicionar um hiperlink ao relatório](#AddHyperlink)  
  
 [Girar texto no relatório](#RotateText)  
  
 [Exibindo texto com formatação HTML](#FormatHTML)  
  
 [Formatar moeda](#FormatCurrency)  
  
 [Salvar o relatório](#Save)  
  
 Tempo estimado para concluir este tutorial: 20 minutos.  
  
## <a name="requirements"></a>Requisitos  
 Para obter mais informações sobre os requisitos, consulte [Pré-requisitos para tutoriais &#40;Construtor de Relatórios&#41;](../reporting-services/report-builder-tutorials.md).  
  
##  <a name="create-a-blank-report-with-a-data-source-and-dataset"></a><a name="CreateReport"></a>Criar um relatório em branco com uma fonte de dados e um conjunto de dados  
  
#### <a name="to-create-a-blank-report"></a>Para criar um relatório em branco  
  
1.  Clique **em Iniciar**, aponte para **programas**, aponte [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)]para **Construtor de relatórios**e, em seguida, clique em **Construtor de relatórios**.  
  
    > [!NOTE]  
    >  A caixa de diálogo **Guia de Introdução** deve ser exibida. Se ela não for exibida, usando o botão do Construtor de Relatórios, clique em **Novo**.  
  
2.  No painel esquerdo da caixa de diálogo **Guia de Introdução** , verifique se **Novo Relatório** está selecionado.  
  
3.  No painel direito, clique em **Relatório em Branco**.  
  
#### <a name="to-create-a-data-source"></a>Para criar uma fonte de dados  
  
1.  No painel dados do relatório, clique em **novo**e em **fonte de dados**.  
  
2.  Na caixa **Nome** , digite: **TextDataSource**  
  
3.  Clique em **Usar uma conexão inserida no meu relatório**.  
  
4.  Verifique se o tipo de conexão é Microsoft SQL Server e, em seguida, na caixa **Cadeia de conexão**, digite: **Fonte de Dados = \<servername>**  
  
    > [!NOTE]  
    >  A expressão \<servername>, por exemplo, Report001, especifica um computador no qual uma instância do SQL Server mecanismo de banco de dados está instalada. Este tutorial não precisa de dados específicos; ele só precisa de uma conexão com um banco de dados [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] . Se você já tiver uma conexão de fonte de dados listada em **Conexões de Fonte de Dados**, será possível selecioná-la e ir para o próximo procedimento, “Para criar uma fonte de dados”. Para obter mais informações, consulte [Formas alternativas de obter uma conexão de dados &#40;Construtor de Relatórios&#41;](../reporting-services/alternative-ways-to-get-a-data-connection-report-builder.md).  
  
5.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
#### <a name="to-create-a-dataset"></a>Para criar um conjunto de dados  
  
1.  No painel de dados do relatório, clique em **Novo**e em **Conjunto de Dados**.  
  
2.  Verifique se a fonte de dados é **TextDataSource**.  
  
3.  Na caixa **Nome** , digite: **TextDataset.**  
  
4.  Verifique se o tipo de consulta **Texto** está selecionado e, em seguida, clique em **Designer de Consulta**.  
  
5.  Clique em **Editar como Texto**.  
  
6.  Cole a seguinte consulta no painel de consulta:  
  
    ```  
    SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(16996.60 AS money) AS Sales, 68 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13747.25 AS money) AS Sales, 55 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Carrying Case' as Product, CAST(9248.15 AS money) As Sales, 37 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1350.00 AS money) AS Sales, 18 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1800.00 AS money) AS Sales, 24 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1125.00 AS money) AS Sales, 15 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1147.50 AS money) AS Sales, 17 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,  'Lens Adapter' as Product, CAST(742.50 AS money) AS Sales, 11 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1417.50 AS money) AS Sales, 21 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(13497.30 AS money) AS Sales, 54 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(11997.60 AS money) AS Sales, 48 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory, 'Carrying Case' as Product, CAST(10247.95 AS money) As Sales, 41 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory, 'Tripod' as Product, CAST(1200.00 AS money) AS Sales, 16 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(2025.00 AS money) AS Sales, 27 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Tripod' as Product, CAST(1425.00 AS money) AS Sales, 19 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(887.50 AS money) AS Sales, 13 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Accessories' as Subcategory, 'Lens Adapter' as Product, CAST(607.50 AS money) AS Sales, 9 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Accessories' as Subcategory,'Lens Adapter' as Product, CAST(1215.00 AS money) AS Sales, 18 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(10191.00 AS money) AS Sales, 79 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8772.00 AS money) AS Sales, 68 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(10578.00 AS money) AS Sales, 82 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(7218.10 AS money) AS Sales, 38 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory,'Digital' as Subcategory, 'Slim Digital' as Product, CAST(8357.80 AS money) AS Sales, 44 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-05' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory,'Digital' as Subcategory,'Slim Digital' as Product, CAST(9307.55 AS money) AS Sales, 49 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(3870.00 AS money) AS Sales, 30 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory,'Compact Digital' as Product, CAST(5805.00 AS money) AS Sales, 45 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate,  'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Compact Digital' as Product, CAST(8643.00 AS money) AS Sales, 67 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Lauren Johnson' as FullName,'Central' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(9877.40 AS money) AS Sales, 52 as Quantity, 'Installing Report Builder' as LinkText, 'https://go.microsoft.com/fwlink/?LinkId=154882' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Warren Pal' as FullName,'North' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(12536.70 AS money) AS Sales, 66 as Quantity, 'Getting Started with Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=160556' AS URL  
    UNION SELECT CAST('2009-01-06' AS date) as SalesDate, 'Fernando Ross' as FullName,'South' as Territory, 'Digital' as Subcategory, 'Slim Digital' as Product, CAST(6648.25 AS money) AS Sales, 35 as Quantity, 'What is New in Report Builder' as Link, 'https://go.microsoft.com/fwlink/?LinkId=165064' AS URL  
    ```  
  
7.  Clique em Executar (**!**) para executar a consulta.  
  
     Os resultados da consulta são os dados disponíveis a serem exibidos no relatório.  
  
8.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
##  <a name="add-a-field-to-the-report-design-surface"></a><a name="AddField"></a>Adicionar um campo ao Design Surface do relatório  
 Se você quiser que um campo do conjunto de dados seja exibido em um relatório, seu primeiro impulso poderá ser de arrastá-lo diretamente para a superfície de design. Este exercício aponta por que isso não funciona e o que fazer em vez disso.  
  
#### <a name="to-add-a-field-to-the-report-and-get-the-wrong-result"></a>Para adicionar um campo ao relatório (e obter o resultado errado)  
  
1.  Arraste o campo **FullName** do painel Dados do Relatório até a superfície de design.  
  
     Construtor de Relatórios cria uma caixa de texto com uma expressão, representada como \<expr>.  
  
2.  Clique em **Executar**.  
  
     Observe que há apenas um registro, **Fernando Ross**, que é, em ordem alfabética, o primeiro registro na consulta. O campo não se repete para mostrar os outros registros nesse campo.  
  
3.  Clique em **Design** para retornar à exibição de design.  
  
4.  Selecione o> \<de expr de expressão na caixa de texto.  
  
5.  No painel Propriedades, na propriedade **Valor** , você vê o seguinte (se o painel Propriedades não estiver visível, na guia **Exibir** , marque **Propriedades**):  
  
    ```  
    =First(Fields!FullName.Value, "TextDataSet")  
    ```  
  
     A função `First` foi projetada para recuperar apenas o primeiro valor em um campo, e foi isso o que ela fez.  
  
     Arrastar o campo diretamente para a superfície de design criou uma caixa de texto. Por si, as caixas de texto não são regiões de dados, logo, elas não exibem dados de um conjunto de dados do relatório. As caixas de texto em regiões de dados, como tabelas, matrizes e listas, exibem dados.  
  
6.  Selecione a caixa de texto (se a expressão estiver selecionada, pressione ESC para marcar a caixa de texto) e pressione a tecla DEL.  
  
#### <a name="to-add-a-field-to-the-report-and-get-the-right-result"></a>Para adicionar um campo ao relatório (e obter o resultado certo)  
  
1.  Na guia **Inserir** da faixa de opções, na área **Regiões de Dados** , clique em **Lista**. Clique na superfície de design e, em seguida, arraste-a para criar uma caixa com aproximadamente 5,08 centímetros de largura e 2,54 centímetros de altura.  
  
2.  Arraste o campo **FullName** do painel Dados do Relatório até a caixa de listagem.  
  
     Desta vez, o Construtor de Relatórios cria uma caixa de texto com a expressão `[FullName]` .  
  
3.  Clique em **Executar**.  
  
     Observe que, desta vez, a caixa se repete para mostrar todos os registros na consulta.  
  
4.  Clique em **Design** para retornar à exibição de design.  
  
5.  Selecione a expressão na caixa de texto.  
  
6.  No painel Propriedades, na propriedade **Valor** , o seguinte é exibido:  
  
    ```  
    =Fields!FullName.Value  
    ```  
  
     Arrastando a caixa de texto até a região de dados da lista, você exibe os dados presentes no conjunto de dados.  
  
7.  Selecione a caixa de listagem e pressione a tecla DEL.  
  
##  <a name="add-a-table-to-the-report-design-surface"></a><a name="AddTable"></a>Adicionar uma tabela ao Design Surface do relatório  
 Crie essa tabela para que você tenha um lugar para colocar hiperlinks e texto girado.  
  
#### <a name="to-add-a-table-to-the-report"></a>Para adicionar uma tabela ao relatório  
  
1.  No menu **Inserir** , clique em **tabela**e, em seguida, clique em **Assistente de tabela**.  
  
2.  Na página **escolher um conjunto** de dados do assistente de nova tabela ou matriz, clique em **escolher um conjunto de dados existente neste relatório ou em um conjunto**de dados compartilhado e clique em **TextDataset (neste relatório)** e, em seguida, clique em **Avançar**.  
  
3.  Na página **organizar campos** , arraste os campos **território**, **linkText**e **produto** para grupos de **linhas**, arraste o campo **vendas** para **valores**e clique em **Avançar**.  
  
4.  Na página **escolher o layout** , desmarque a caixa de seleção **expandir/recolher grupos** para que você possa ver a tabela inteira e, em seguida, clique em **Avançar**.  
  
5.  Na página **escolher um estilo** , clique em **Tablet**e em **concluir**.  
  
6.  Arraste a tabela para que ela esteja abaixo do bloco de título.  
  
7.  Clique em **Executar**.  
  
     A tabela parece correta, mas tem duas linhas totais. O campo **linkText** não precisa de uma linha total.  
  
8.  Clique em **Design** para retornar à exibição de design.  
  
9. Clique com o botão direito do mouse na `[LinkText]`caixa de texto que contém e clique em **dividir células**.  
  
10. Selecione a célula vazia abaixo da `[LinkText]` célula e mantenha pressionada a tecla Shift e selecione as duas células à direita: a célula **total** na coluna **Product** e a `[Sum(Sales)]` célula na coluna **Sales** .  
  
11. Com essas três células selecionadas, clique com o botão direito do mouse em uma dessas células e clique em **Excluir linha**.  
  
12. Clique em **Executar**.  
  
##  <a name="add-a-hyperlink-to-the-report"></a><a name="AddHyperlink"></a>Adicionar um hiperlink ao relatório  
 Nesta seção, você adiciona um hiperlink ao texto na tabela da seção anterior.  
  
#### <a name="to-add-a-hyperlink-to-the-report"></a>Para adicionar um hiperlink ao relatório  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique com o botão direito do mouse na célula que contém `[LinkText]`e clique em **Propriedades da Caixa de Texto**.  
  
3.  Na caixa **Propriedades da caixa de texto** , clique em **ação**.  
  
4.  Clique em **ir para URL**.  
  
5.  Na caixa **selecionar URL** , clique em **[url]** e, em seguida, clique em **OK**.  
  
6.  Observe que o texto não parece diferente. Você precisa fazê-lo parecer um texto de link.  
  
7.  Selecione `[LinkText]`.  
  
8.  Na seção **fonte** da guia **início** , clique no botão **sublinhado** e, em seguida, clique na seta suspensa ao lado do botão **cor** e clique em **azul**.  
  
9. Clique em **Executar**.  
  
     O texto agora se parece com um link.  
  
10. Clique em um link. Se o computador estiver conectado à Internet, um navegador abrirá um tópico da Ajuda do Construtor de Relatórios.  
  
##  <a name="rotate-text-in-the-report"></a><a name="RotateText"></a>Girar texto no relatório  
 Nesta seção, você gira um texto na tabela das seções anteriores.  
  
#### <a name="to-rotate-text"></a>Para girar texto  
  
1.  Clique em **Design** para retornar à exibição de design.  
  
2.  Clique na célula que contém `[Territory].`  
  
3.  Na guia **Início** , na seção **Fonte** , clique no botão **Negrito** .  
  
4.  Se o painel Propriedades não estiver aberto, na guia **Exibir** , marque a caixa de seleção **Propriedades** .  
  
5.  Localize a propriedade WritingMode no painel Propriedades.  
  
    > [!NOTE]  
    >  Quando as propriedades no painel Propriedades estiverem organizadas em categorias, WritingMode estará na categoria **Localização** . Verifique se você selecionou a célula, e não o texto WritingMode é uma propriedade da caixa de texto, não do texto.  
  
6.  Na caixa de listagem, clique em **Rotate270**.  
  
7.  Na guia **início** da seção **parágrafo** , **clique nos botões central e** **Centro** para localizar o texto no centro da célula, verticalmente e horizontalmente.  
  
8.  Clique em Executar (**!**).  
  
 Agora o texto na célula `[Territory]` é executado verticalmente da parte inferior para a parte superior das células.  
  
##  <a name="displaying-text-with-html-formatting"></a><a name="FormatHTML"></a>Exibindo texto com formatação HTML  
  
#### <a name="to-display-text-formatted-as-html"></a>Para exibir texto formatado como HTML  
  
1.  Clique em **Design** a fim de alternar para a exibição de design.  
  
2.  Na guia **Inserir** , clique em **Caixa de Texto**e, na superfície de design, clique e arraste para criar uma caixa de texto abaixo da tabela, com cerca de 10 centímetros de largura e 8 centímetros de altura.  
  
3.  Copiar esse texto e cole-o na caixa de texto:  
  
    ```  
    <h4>Limitations of cascading style sheet attributes</h4>  
          <p>Only a basic set of <b>cascading style sheet (CSS)</b> attributes are defined:</p>  
          <ul><li>  
              text-align, text-indent  
            </li><li>  
              font-family, font-size  
            </li><li>  
              color  
            </li><li>  
              padding, padding-bottom, padding-top, padding-right, padding-left  
            </li><li>  
              font-weight  
            </li></ul>  
    ```  
  
4.  Selecione todo o texto na caixa de texto.  
  
     Essa é uma propriedade do texto, não da caixa de texto, portanto, em uma caixa de texto você pode ter uma mistura de texto sem formatação e texto que usa marcas HTML como estilos.  
  
5.  Clique com o botão direito do mouse em todo o texto selecionado e clique em **Propriedades do Texto**.  
  
6.  Na página **geral** , em **tipo de marcação**, clique em **HTML-interpretar marcas HTML como estilos**.  
  
7.  Clique em **OK**.  
  
8.  Clique em Executar (**!**) para visualizar o relatório.  
  
 O texto na caixa de texto é exibido como um título, um parágrafo e uma lista com marcadores.  
  
##  <a name="format-currency"></a><a name="FormatCurrency"></a>Formatar moeda  
  
#### <a name="to-format-numbers-as-currency"></a>Para formatar números como moeda  
  
1.  Clique em **Design** a fim de alternar para a exibição de design.  
  
2.  Clique na célula da tabela superior que contenha `[Sum(Sales)]`, mantenha a tecla SHIFT pressionada e clique na célula da tabela inferior que contenha `[Sum(Sales)]`.  
  
3.  Na guia **Início** , no grupo **Número** , clique no botão **Moeda** .  
  
4.  Adicional Na guia **início** , no grupo **número** , clique no botão **estilos de espaço reservado** e clique em **valores de exemplo** para ver como os números serão formatados.  
  
5.  (Opcional) Na guia **Início** , no grupo **Número** , clique no botão **Diminuir Decimais** duas vezes para exibir valores em dólares sem centavos.  
  
6.  Clique em Executar (**!**) para visualizar o relatório.  
  
 O relatório agora exibe dados formatados e é mais fácil de ler.  
  
##  <a name="save-the-report"></a><a name="Save"></a>Salvar o relatório  
 É possível salvar relatórios em um servidor de relatório, em uma biblioteca do SharePoint ou no computador.  
  
 Neste tutorial, salve o relatório em um servidor de relatório. Se você não tiver acesso ao servidor de relatório, salve o relatório no computador.  
  
#### <a name="to-save-the-report-on-a-report-server"></a>Para salvar o relatório em um servidor de relatório  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Sites e Servidores Recentes**.  
  
3.  Selecione ou digite o nome do servidor de relatório no qual você tem permissão para salvar relatórios.  
  
     A mensagem "Conectando-se a um servidor de relatório" é exibida. Quando a conexão for concluída, você verá o conteúdo da pasta do relatório que o administrador do servidor de relatório especificou como o local padrão para relatórios.  
  
4.  Em **Nome**, substitua o nome padrão por um nome de sua escolha.  
  
5.  Clique em **Salvar**.  
  
 O relatório será salvo no servidor de relatório. O nome do servidor de relatório ao qual você está conectado é exibido na barra de status da parte inferior da janela.  
  
#### <a name="to-save-the-report-on-your-computer"></a>Para salvar o relatório no computador  
  
1.  No botão **Construtor de Relatórios** , clique em **Salvar como**.  
  
2.  Clique em **Área de Trabalho**, **Meus Documentos**ou **Meu Computador**e, em seguida, navegue até a pasta na qual você deseja salvar o relatório.  
  
3.  Em **Nome**, substitua o nome padrão por um nome de sua escolha.  
  
4.  Clique em **Salvar**.  
  
## <a name="next-steps"></a>Próximas etapas  
 Há várias maneiras de Formatar texto em Construtor de Relatórios [tutorial: Criando um relatório de formato livre &#40;Construtor de Relatórios&#41;](../reporting-services/tutorial-creating-a-free-form-report-report-builder.md) contém mais exemplos.  
  
## <a name="see-also"></a>Consulte Também  
 [TUTORIAIS &#40;Construtor de Relatórios&#41;](report-builder-tutorials.md)   
 [Formatando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [Construtor de Relatórios no SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
