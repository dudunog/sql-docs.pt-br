---
title: Assistente de Mapa e Assistente de Camada do Mapa (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.mapandlayerwizard.f1
- "10542"
- MICROSOFT.REPORTDESIGNER.MAPLAYER.NAME
ms.assetid: 48cbe18b-1290-4107-8a1c-ec6acd71f73b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: aa28d15a07a8621d2aafb71aaa69bd67ae9fcf4d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78172781"
---
# <a name="map-wizard-and-map-layer-wizard-report-builder-and-ssrs"></a>Assistente de Mapa e Assistente de Camada do Mapa (Construtor de Relatórios e SSRS)
  O Assistente de Mapa e o Assistente de Camada do Mapa automatizam a tarefa de criar um mapa, adicionar uma camada a um mapa ou alterar as opções de camada do mapa em uma camada existente.

> [!NOTE]
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]

 Antes de adicionar um mapa a um relatório ou uma camada a um mapa, você deve ter estas informações:

-   **Fonte de dados espaciais.** O local ou a conexão com uma fonte que fornece dados espaciais, por exemplo, o nome de uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e um banco de dados que contém dados espaciais ou o nome de um arquivo de forma ESRI (Environmental Systems Research Institute, Inc.).

-   **Spatial data.** Um campo que contém conjuntos de coordenadas que especificam locais da fonte de dados espaciais.

-   **Dados analíticos.** Dados analíticos a serem usados para variar a exibição do mapa, por exemplo, vendas anuais da loja.

-   **Campos de correspondência.** Campos correspondentes que definem a relação entre os dados espaciais e os dados analíticos, por exemplo, o nome de uma região e uma cidade para identificar exclusivamente cada cidade.

 As seções a seguir fornecem informações sobre opções que você especifica quando usa os Assistentes de Mapa e de Camada do Mapa.

##  <a name="map-wizard-and-map-layer-wizard-pages"></a><a name="BackToTop"></a>Páginas assistente de mapa e assistente de camada do mapa
 Para abrir o Assistente de Mapa, execute uma destas ações:

-   Quando você abrir o Construtor de Relatórios pela primeira vez, clique no ícone do assistente de **Mapa** no centro da superfície de design.

-   Na guia **Inserir** , clique em **Mapa**e em **Assistente de Mapa**.

 Para abrir o assistente de Camada do Mapa, execute esta ação:

-   Clique no mapa para exibir o painel Mapa e, na barra de ferramentas, clique no botão **Assistente de nova camada** .

 Clique no título da página do assistente para obter o respectivo conteúdo de ajuda. As páginas exibidas variarão de acordo com as suas escolhas de tipo de mapa, a fonte de dados espaciais e a fonte de dados analíticos.

1.  [Escolha uma fonte de dados espaciais](#SpatialDataSource). Os dados espaciais podem vir da galeria de mapas, de um Arquivo de Forma ESRI ou de dados espaciais em um banco de dados relacional do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .

    -   [O que são dados espaciais?](#SpatialData)

    -   [O que é a Galeria de Mapas?](#MapGallery)

    -   [O que é um Arquivo de Forma ESRI?](#Shapefile)

    -   [Onde posso obter arquivos de forma ESRI?](#GetShapefiles)

    -   [O que é uma consulta espacial do SQL Server?](#SqlServerSpatial)

2.  [Escolha dados espaciais e opções de exibição de mapa](#MapView). Defina a exibição e a resolução do mapa, especifique se deseja inserir dados espaciais no relatório e defina se um plano de fundo de peças de mapa do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Bing deve ser incluído.

    -   [O que é a exibição ou o visor do mapa?](#Viewport)

    -   [O que é resolução ou otimização do mapa?](#Resolution)

    -   [O que faz a inserção de dados espaciais?](#Embed)

    -   [O que é um plano de fundo de peças de mapa do Bing?](#Tiles)

3.  [Escolha visualização de mapa](#Visualization). Escolha o tipo de mapa a ser criado.

    -   [Qual é a diferença entre um Mapa Básico, um Mapa de Bolha e um Mapa Analítico?](#MapType)

    -   **Escolher visualização de mapa: Polígonos**

    -   **Escolher visualização de mapa: Linhas**

    -   **Escolher visualização de mapa: Pontos**

4.  **Escolha uma conexão com uma fonte de dados**. Escolha uma conexão de fonte de dados ou crie uma com uma fonte de dados externa que contenha dados analíticos a serem exibidos no mapa.

5.  **Crie uma consulta**. Crie uma consulta que especifique os dados analíticos.

6.  [Escolha o conjunto de campos analíticos](#AnalyticalData). Especifique uma fonte de dados para os dados analíticos.

    -   [Qual é a diferença entre dados espaciais e dados analíticos?](#Diff)

7.  [Especifique os campos de correspondência para dados espaciais e analíticos](#SpecifyMatchFields). Crie uma relação entre os dados espaciais e os dados analíticos, para que a aparência dos elementos do mapa possa variar com base nos dados.

    -   [O que é um campo de correspondência?](#MatchFields)

8.  [Escolha o tema da cor e a visualização dos dados](#ThemeandVisualization). Para especificar como visualizar os dados em relação ao plano de fundo do mapa, especifique o tema do mapa, os campos a serem visualizados e o que variar: cor, tamanho, e/ou tipo de marcador.

    -   [O que faz o tema?](#Theme)

    -   [Para que servem as legendas e as escalas na Visualização de Mapa?](#Legends)

    -   [O que são regras?](#Rules)

 Depois que adicionar um mapa ou camada do mapa e visualizar o relatório, você poderá alterar as opções do mapa e da camada do mapa que definir nos assistentes. Para obter mais informações, consulte [Personalizar os dados e a exibição de um mapa ou de uma camada do mapa &#40;Construtor de Relatórios e SSRS&#41;](customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md).

 Para obter mais informações sobre mapas, consulte [Mapas &#40;Construtor de Relatórios e SSRS&#41;](maps-report-builder-and-ssrs.md). Para obter instruções passo a passo sobre como adicionar um mapa a um relatório, consulte [Tutorial: relatório de mapa &#40;Construtor de Relatórios&#41;](../tutorial-map-report-report-builder.md).

 ![Ícone de seta usado com o link voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [de volta ao início](#BackToTop)

##  <a name="choose-a-source-of-spatial-data"></a><a name="SpatialDataSource"></a>Escolher uma fonte de dados espaciais
 Nesta página, especifique a fonte de dados espaciais e quais dados espaciais deverão ser incluídos. Os dados espaciais podem vir da galeria de mapas, de um Arquivo de Forma ESRI ou de uma consulta de conjunto de dados que especifique dados espaciais do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de um banco de dados do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou de uma versão posterior.

 Você pode usar a mesma fonte ou uma fonte de dados espaciais diferente para cada camada, mas deverá especificar essa fonte cada vez que adicionar uma camada. Quando os dados espaciais forem da galeria de mapas ou de um Arquivo de Forma ESRI, a fonte de dados espaciais não será um item de relatório separado. Ela não aparece no painel de dados do relatório.

###  <a name="what-is-spatial-data"></a><a name="SpatialData"></a>O que são dados espaciais?
 Dados espaciais contêm coordenadas que definem elementos geográficos ou geométricos. Em um mapa, os dados espaciais definem *elementos do mapa*: polígonos que definem áreas ou formas, linhas que definem rotas ou caminhos e pontos que definem marcadores ou pinos. Os dados espaciais são armazenados em formato binário na fonte de dados e especificados como conjuntos de coordenadas. Por exemplo, um ponto é uma coordenada X e Y (X Y), uma linha corresponde a dois conjuntos de coordenadas ((X1 Y1), (X2 Y2)), um polígono corresponde a quatro ou mais conjuntos de coordenadas em que o primeiro e o último conjunto de coordenadas são iguais ((X1 Y1), (X2 Y2), (X3 Y3), (X1 Y1)).

 Para obter mais informações, consulte a documentação do tipo de dados espaciais que você está usando.

###  <a name="what-is-the-map-gallery"></a><a name="MapGallery"></a>O que é a Galeria de mapas?
 A galeria de mapas contém mapas de relatórios localizados na pasta da galeria de mapas do ambiente de criação de relatórios. Os mapas da galeria o ajudam a começar rapidamente a adicionar mapas a seu relatório. Os mapas predefinidos na galeria são fornecidos por um provedor de mapa.

> [!NOTE]
>  Esse [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] recurso de mapeamento usa dados de forma de Tiger/line que forneciam cortesia do censo[http://www.census.gov/](http://www.census.gov/)Bureau () dos EUA. Os arquivos de forma TIGER/Line são um extrato das informações geográficas e cartográficas selecionadas do banco de dados Census MAF/TIGER. Esses arquivos de forma podem ser obtidos sem encargos com a Agência de Recenseamento norte-americana. Para saber mais sobre os Shapefiles TIGER/Line, visite a [documentação técnica dos Shapefiles TIGER/Line e dos arquivos TIGER/Line](https://www.census.gov/programs-surveys/geography/technical-documentation/complete-technical-documentation/tiger-geo-line.html). As informações de limites nos arquivos de forma Tiger/Line destinam-se apenas a fins de coleta de dados estatísticos e tabulação; a representação e a designação dessas informações para propósitos estatísticos não constituem uma determinação de autoridade de jurisdição ou direitos de propriedade ou qualificação e elas não são descrições de terra legais. Census TIGER e TIGER/Line são marcas registradas da Agência de Recenseamento norte-americana.

 Para estender a galeria de mapas, você pode adicionar ou remover relatórios do diretório dessa galeria e adicionar pastas para organizar os mapas. Para obter mais informações, consulte [Mapas &#40;Construtor de Relatórios e SSRS&#41;](maps-report-builder-and-ssrs.md).

###  <a name="what-is-an-esri-shapefile"></a><a name="Shapefile"></a>O que é um formato de forma ESRI?
 Um Arquivo de Forma ESRI é um conjunto de arquivos com dados no formato de dados espaciais de Arquivo de Forma ESRI (Environmental Systems Research Institute, Inc.). O conjunto de arquivos normalmente inclui o * \<nome *do arquivo>. shp que contém os dados espaciais e um arquivo de suporte, * \<filename>*. dbf.

 Quando você especifica um arquivo de forma como fonte de dados espaciais e ele está em seu computador local, os dados espaciais são inseridos automaticamente no relatório. Para usar dados espaciais de um arquivo ESRI dinamicamente, faça o seguinte:

 No Construtor de Relatórios, carregue os arquivos .shp e .dbf na mesma pasta em um servidor de relatório e depois vincule ao arquivo .shp como a fonte de dados espaciais.

 No Designer de Relatórios no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], adicione os arquivos .shp e .dbf ao projeto de relatório e especifique o nome do arquivo .shp como a fonte de dados espaciais.

###  <a name="where-can-i-get-esri-shapefiles"></a><a name="GetShapefiles"></a>Onde posso obter forma ESRI?
 Há arquivos de forma ESRI disponíveis na Web. Para obter mais informações, consulte [Localizando arquivos de forma ESRI para um mapa](https://go.microsoft.com/fwlink/?linkid=178814).

###  <a name="what-is-a-sql-server-spatial-query"></a><a name="SqlServerSpatial"></a>O que é uma consulta espacial SQL Server?
 Uma consulta espacial do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é uma consulta de conjunto de dados que especifica dados do tipo de dados SQLGeometry ou SQLGeography de um banco de dados relacionais do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .

> [!NOTE]
>  Ao definir uma fonte de dados no assistente, você verá diferentes designers de consulta na página Crie uma Consulta, dependendo do tipo de fonte de dados ao qual estiver se conectando. Para obter mais informações, consulte [Designers de Consultas &#40;Construtor de Relatórios&#41;](../query-designers-report-builder.md).

 Quando você executa a consulta no designer de consulta, o conjunto de resultados exibe uma coluna com dados espaciais que aparecem como texto. Por exemplo, uma linha poderia conter dados espaciais que constituem um único ponto e a linha seguinte poderia conter dados espaciais que definissem um conjunto de pontos. Cada linha se torna um elemento do mapa. Você pode variar a exibição de cada elemento do mapa como uma unidade indivisível.

 Para obter mais informações, consulte "Types of Spatial Data" nos [Manuais Online do SQL Server](https://go.microsoft.com/fwlink/?linkid=120955).

 ![Ícone de seta usado com o link voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [de volta ao início](#BackToTop)

##  <a name="choose-spatial-data-and-map-view-options"></a><a name="MapView"></a>Escolher dados espaciais e opções de exibição de mapa
 Nesta página, você pode definir as seguintes opções:

-   Defina o centro de exibição e o nível de zoom para os dados espaciais que você selecionou na página anterior do assistente. A exibição que você define se aplica ao mapa inteiro.

-   Defina a resolução do mapa.

-   Especifique se deseja inserir os dados espaciais no relatório.

-   Para dados inseridos, especifique se você deseja incluir todos os dados ou apenas os dados na exibição atual.

-   Especifique se você deseja incluir um plano de fundo de peças de mapa do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .

###  <a name="what-is-the-map-view-or-viewport"></a><a name="Viewport"></a>O que é o visor ou exibição de mapa?
 O visor do mapa define a área do mapa a ser exibida para todas as camadas no relatório.

 Por padrão, as escalas de cores e distância aparecem dentro do visor, e a legenda do mapa aparece fora do visor. Você poderá alterar essas opções do visor depois que concluir o assistente.

###  <a name="what-is-map-resolution-and-optimization"></a><a name="Resolution"></a>O que é resolução e otimização de mapa?
 Quando alterar a resolução dos dados espaciais que representam linhas ou polígonos, você estará especificando o quão detalhado deve ser o desenho do mapa. Por exemplo, para vistas aéreas de uma região, você precisa de granularidade até cem metros da área da superfície na terra ou a resolução de aproximadamente 1,6 km é suficiente?

 Quando dados espaciais são inseridos no relatório, uma resolução mais alta aumenta o número de elementos necessários para desenhar detalhes nessa resolução. Quando os dados espaciais não são inseridos no relatório, uma resolução mais alta aumenta o tempo necessário para que o processador de relatório calcule as linhas do mapa nessa resolução toda vez que o relatório é exibido.

 Quando você diminuir a resolução, o processador de relatório aplicará um algoritmo para reduzir o número de pontos necessário para desenhar os elementos do mapa. Quanto menor a resolução, menor a quantidade de dados necessária para exibir os elementos do mapa, o que pode levar a um melhor desempenho de exibição.

 À medida que você ajusta o controle deslizante, os dados de visualização no painel do assistente são atualizados para dar a você uma indicação do efeito. Depois que adicionar o mapa ao relatório, você poderá ajustar este valor alterando as opções de visor do mapa.

###  <a name="what-does-embedding-spatial-data-do"></a><a name="Embed"></a>O que faz a incorporação de dados espaciais?
 Quando você insere elementos de mapa de peças de mapa do Bing em um relatório, os dados espaciais são armazenados na definição do relatório.

 Um relatório com um mapa pode usar dados espaciais ou peças de mapa do Bing recuperadas dinamicamente quando o relatório é processado ou em tempo de design e depois inserido na definição do relatório. Elementos de mapa inseridos podem aumentar significativamente o tamanho da definição do relatório, mas reduzem o tempo necessário para exibir o mapa no relatório. Os elementos de mapa dinâmicos reduzem o tamanho da definição do relatório, mas aumentam o tempo necessário para processar e exibir o mapa.

 O bom design de relatório requer que você avalie as desvantagens de dados de mapa estáticos ou dinâmicos e encontre o equilíbrio que funciona para suas circunstâncias. Em geral, mais dados significa que a definição do relatório e o relatório compilado exigirão mais armazenamento no servidor de relatório e tempos de processamento maiores. Sempre é uma prática recomendada cortar dados espaciais, bem como limitar outros dados do relatório, para incluir apenas o que for necessário para o relatório.

###  <a name="what-is-a-bing-map-tile-background"></a><a name="Tiles"></a>O que é uma fundo de bloco do mapa do Bing?
 Para adicionar um plano de fundo de imagem geográfica a seu mapa, selecione a opção de peças de mapa do Bing. O processador de relatório baixa itens dos Serviços Web Bing Maps para a área de mapa e resolução que você especifica nesta página do assistente. Você pode especificar um dos seguintes tipos lado a lado:

-   **Rodoviário.** Exibe um estilo de mapa rodoviário com plano de fundo branco.

-   **Aéreo.** Exibe apenas uma vista aérea. Nenhum texto é exibido neste modo.

-   **Ti.** Exibe a combinação de **Rodoviário** e **Aéreo** .

 Para obter mais informações sobre peças, consulte [Sistema de Peças do Bing Maps](https://go.microsoft.com/fwlink/?LinkId=147315).  Para obter mais informações sobre o uso de peças de mapa do Bing no seu relatório, consulte [termos de uso adicionais](https://go.microsoft.com/fwlink/?LinkId=151371) e a [Política de Privacidade](https://go.microsoft.com/fwlink/?LinkId=151372).

 Para visualizar um plano de fundo de peça no modo Design, você deve ter acesso à Internet. Para visualizar o plano de fundo de peça na visualização de um relatório em um servidor de relatório, esse servidor deve ser configurado para dar suporte a peças de mapa do Bing. Para obter mais informações, consulte [solucionar problemas de relatórios: mapear relatórios &#40;Construtor de relatórios e SSRS&#41;](troubleshoot-reports-map-reports-report-builder-and-ssrs.md) e "planejamento para mapas" na [documentação do Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) no manuais online do SQL Server.

 Para obter mais informações sobre outras maneiras de personalizar uma camada lado a lado, consulte [Adicionar, alterar ou excluir um mapa ou uma camada do mapa &#40;Construtor de Relatórios e SSRS&#41;](add-change-or-delete-a-map-or-map-layer-report-builder-and-ssrs.md).

 ![Ícone de seta usado com o link voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [de volta ao início](#BackToTop)

##  <a name="choose-map-visualization"></a><a name="Visualization"></a>Escolher visualização de mapa
 Nesta página, escolha a camada ou o tipo de mapa a ser adicionado ao seu relatório. Na primeira vez em que executar o assistente, você adicionará o mapa e a primeira camada do mapa ao relatório. Um mapa pode conter várias camadas. Cada camada do mapa exibe um tipo específico de dados espaciais: polígonos, linhas ou pontos.

 O tipo de mapa escolhido dependerá do propósito do mapa e dos dados disponíveis.

###  <a name="what-is-the-difference-among-a-basic-map-a-bubble-map-and-an-analytical-map"></a><a name="MapType"></a>Qual é a diferença entre um mapa básico, um mapa de bolha e um mapa analítico?
 Um **Mapa Básico** exibe apenas locais. Você pode variar as cores das áreas no mapa por sombra, mas a cor não representa valores de dados analíticos.

 Um **Mapa de Bolha** transmite o valor relativo de uma única agregação de dados analíticos como tamanho de bolha, por exemplo, as vendas da loja. Você pode criar mapas de bolha para polígonos ou pontos. Para polígonos, defina as propriedades de ponto central do polígono; para pontos, defina as propriedades de marcador.

 Um **Mapa Analítico** transmite o valor relativo de uma ou mais agregações de dados analíticos para cada elemento do mapa. Por exemplo, as vendas da loja como tamanho de marcador, a margem de lucro das categorias de produto como cor de marcador e o produto mais vendido como tipo de marcador.

 Para obter mais informações, consulte [Planejar um relatório de mapa &#40;Construtor de Relatórios e SSRS&#41;](plan-a-map-report-report-builder-and-ssrs.md).

 ![Ícone de seta usado com o link voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [de volta ao início](#BackToTop)

##  <a name="choose-the-analytical-dataset"></a><a name="AnalyticalData"></a>Escolher o conjunto de
 Nesta página, especifique onde obter os dados analíticos a serem exibidos nesta camada do mapa.

 Para exibir os dados de relatório ou qualquer dado analítico em relação ao plano de fundo do mapa, especifique o local em que os dados estão e como estão relacionados aos dados espaciais. Os dados podem vir de um conjunto de dados de relatório existente ou de um novo conjunto de dados para o qual você cria uma consulta. Os dados analíticos existentes podem ser incluídos no Arquivo de Forma ESRI que contém os dados espaciais.

###  <a name="what-is-the-difference-between-spatial-data-and-analytical-data"></a><a name="Diff"></a>Qual é a diferença entre dados espaciais e dados analíticos?
 Dados espaciais consistem em conjuntos de coordenadas que especificam pontos, linhas e polígonos. Os elementos do mapa se baseiam em dados espaciais.

 Os dados analíticos são dados numéricos ou categóricos que você deseja usar para variar a aparência do mapa. Os dados analíticos podem vir de um conjunto de dados de relatório ou podem ser incluídos em dados espaciais de um mapa da galeria de mapas ou de um arquivo de forma ESRI.

 ![Ícone de seta usado com o link voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [de volta ao início](#BackToTop)

##  <a name="specify-the-match-fields"></a><a name="SpecifyMatchFields"></a>Especificar os campos de correspondência
 Nesta página, crie uma relação entre os dados espaciais e os dados analíticos.

###  <a name="what-are-match-fields"></a><a name="MatchFields"></a>O que são campos de correspondência?
 Os campos de correspondência permitem que o processador de relatório crie uma relação entre os dados analíticos e os dados espaciais. Esses campos especificam valores exclusivos dentro dos dados analíticos. Por exemplo, o nome da loja talvez não ser exclusivo dentro dos dados, portanto, você poderia especificar uma cidade e o nome da loja.

 ![Ícone de seta usado com o link voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [de volta ao início](#BackToTop)

##  <a name="choose-color-theme-and-data-visualization"></a><a name="ThemeandVisualization"></a>Escolher o tema de cores e a visualização de dados
 Nesta página. especifique como visualizar os dados em relação ao plano de fundo do mapa, o tema do mapa, os campos a serem visualizados e o que variar: cor, tamanho, e/ou tipo de marcador.

###  <a name="what-does-the-theme-do"></a><a name="Theme"></a>O que o tema faz?
 O tema que você escolhe define valores padrão para cor, borda e fonte. Você poderá alterar essas opções depois que concluir o assistente.

###  <a name="what-are-the-legends-and-scales-in-map-preview-for"></a><a name="Legends"></a>Quais são as legendas e as escalas na visualização de mapa para?
 As legendas ajudam um usuário a interpretar os dados exibidos em um mapa. Um mapa fornece um intervalo de cores, uma escala de distância e uma legenda.

-   **Intervalo de cores.** O intervalo de cores exibe uma barra de cores com uma escala que fornece um guia para os intervalos de dados determinados pelo processador de relatório com base nas regras que você especifica para a camada.

-   **Escala de distância.** A escala de distância fornece uma guia para as unidades de distância no mapa. As unidades de distância são determinadas automaticamente com base na projeção do mapa e no nível de zoom.

-   **Legenda.** A legenda fornece uma guia para ajudar a interpretar o significado de cores, tamanhos, e tipos de marcador em um mapa. Por padrão, todas as regras para todas as camadas exibem intervalos de dados na primeira legenda. Você pode personalizar esta legenda e adicionar legendas após a adição do mapa ao relatório.

###  <a name="what-are-rules"></a><a name="Rules"></a>O que são regras?
 Regras são cálculos que o processador de relatório usa para dividir dados analíticos em intervalos. Você pode especificar regras diferentes para cada camada. O tipo de regras que você pode especificar depende do tipo de dados espaciais na camada:

-   **Polígonos.** Você pode especificar regras de cor.

-   **Pontos centrais de polígonos.** Você pode especificar regras de cor, tamanho e tipo de marcador.

-   **Alinha.** Você pode especificar regras de cor e largura.

-   **Faixas.** Você pode especificar regras de cor, tamanho e tipo de marcador.

 O processador de relatório aplica as regras que você define e determina automaticamente a lista de itens a serem exibidos em uma legenda. Por padrão, os resultados de todas regras para todas as camadas exibidas na primeira legenda. Você poderá ajustar isso depois que concluir o assistente. Para obter mais informações, consulte [Variar a exibição de polígono, linha e ponto por regras e dados analíticos &#40;Construtor de Relatórios e SSRS&#41;](vary-polygon-line-and-point-display-by-rules-and-analytical-data.md).

 ![Ícone de seta usado com o link voltar ao início](../../2014-toc/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao Início") [de volta ao início](#BackToTop)

## <a name="see-also"></a>Consulte Também
 [Solucionar problemas de relatórios: mapear relatórios &#40;Construtor de relatórios e ssrs&#41;](troubleshoot-reports-map-reports-report-builder-and-ssrs.md) [planejar um relatório de mapa &#40;Construtor de Relatórios e SSRS&#41;](plan-a-map-report-report-builder-and-ssrs.md) [mapas &#40;Construtor de relatórios e SSRS&#41;](maps-report-builder-and-ssrs.md)


