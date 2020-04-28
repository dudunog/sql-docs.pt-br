---
title: Propriedades da cadeia de conexão (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 29a00a41-5b0d-44b2-8a86-1b16fe507768
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7cd6ea975462a7967c7938de8900d5b1877ff524
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "79217070"
---
# <a name="connection-string-properties-analysis-services"></a>Propriedades de cadeia de conexão (Analysis Services)
  Este tópico documenta as propriedades da cadeia de conexão que você pode definir em uma das ferramentas de designer ou de administração, ou que você pode ver nas cadeias de conexão criadas por aplicativos cliente que se conectam aos dados do Analysis Services ou os consultam. Sendo assim, ele aborda apenas um subconjunto das propriedades disponíveis. A lista completa inclui várias propriedades de servidor e de banco de dados, permitindo que você personalize a conexão de um aplicativo específico, independentemente de como a instância ou o banco de dados está configurado no servidor.  
  
 Os desenvolvedores que criam cadeias de conexão personalizadas no código do aplicativo devem examinar a documentação da API do cliente ADOMD.NET para exibir uma lista mais detalhada: <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>  
  
 As propriedades descritas neste tópico são usadas pelas bibliotecas de cliente do Analysis Services, AMO, ADOMD.NET e provedor OLE DB do Analysis Services. A maioria das propriedades da cadeia de conexão pode ser usada com as três bibliotecas de cliente. As exceções são destacadas na descrição.  
  
 Este tópico inclui as seções a seguir:  
  
 [Parâmetros de conexão em uso comum](#bkmk_common)  
  
 [Autenticação e segurança](#bkmk_auth)  
  
 [Parâmetros de finalidade especial](#bkmk_special)  
  
 [Reservado para uso futuro](#bkmk_reserved)  
  
 [Exemplo de cadeias de conexão](#bkmk_examples)  
  
 [Formatos de cadeia de conexão usados no Analysis Services](#bkmk_supportedstrings)  
  
 [Criptografando cadeias de conexão](#bkmk_encrypt)  
  
> [!NOTE]  
>  Ao definir propriedades, se você define a mesma propriedade duas vezes por engano, a última propriedade da cadeia de conexão será usada.  
  
 Para saber mais sobre como especificar uma conexão do Analysis Services em aplicativos existentes da Microsoft, veja [Conectar-se de aplicativos cliente &#40;Analysis Services&#41;](connect-from-client-applications-analysis-services.md).  
  
##  <a name="connection-parameters-in-common-use"></a><a name="bkmk_common"></a> Parâmetros de conexão de uso comum  
 A tabela a seguir descreve as propriedades mais usadas na criação de uma cadeia de conexão.  
  
|Propriedade|Descrição|Exemplo|  
|--------------|-----------------|-------------|  
|`Data Source` ou `DataSource`|Especifica a instância do servidor. Esta propriedade é necessária para todas as conexões. Os valores válidos incluem o nome da rede ou o endereço IP do servidor, local ou localhost para conexões locais, uma URL se o servidor for configurado para acesso HTTP ou HTTPS, ou o nome de um arquivo de cubo local (.cub).|`Data source=AW-SRV01` para a instância padrão e a porta (TCP 2383).<br /><br /> `Data source=AW-SRV01$Finance:8081` para uma instância nomeada ($Finance) e uma porta fixa.<br /><br /> `Data source=AW-SRV01.corp.Adventure-Works.com` para um nome de domínio totalmente qualificado, assumindo a instância padrão e a porta.<br /><br /> `Data source=172.16.254.1` para um endereço IP do servidor, ignorando a pesquisa de servidor DNS, útil para solucionar problemas de conexão.|  
|`Initial Catalog` ou `Catalog`|Especifica o nome do banco de dados do Analysis Services que será o destino da conexão. O banco de dados deve ser implantado no Analysis Services, e você deve ter permissão para se conectar a ele. Esta propriedade é opcional para conexões do AMO, mas é obrigatória para o ADOMD.NET.|`Initial catalog=AdventureWorks2012`|  
|`Provider`|Os valores válidos incluem MSOLAP ou MSOLAP. \<versão>, em \<que a versão> é 3, 4 ou 5. No sistema de arquivos, o nome do provedor de dados é msolap110.dll para o SQL Server 2012, msolap100.dll para o SQL Server 2008 e 2008 R2, e msolap90.dll para o SQL Server 2005.<br /><br /> A versão atual é MSOLAP.5. Essa propriedade é opcional. Por padrão, as bibliotecas de cliente leem a versão atual do provedor OLE DB do Registro. Você só precisará definir essa propriedade se precisar de uma versão específica do provedor de dados, por exemplo, para se conectar a uma instância do SQL Server 2008.<br /><br /> Os provedores de dados correspondem às versões do SQL Server. Se sua organização usa a versão atual e as versões anteriores do Analysis Services, é mais provável que você precise especificar qual provedor será usado nas cadeias de conexão criadas manualmente. Talvez você também precise baixar e instalar versões específicas do provedor de dados em computadores que não têm a versão necessária. Você pode baixar o provedor OLE DB nas páginas do SQL Server Feature Pack no centro de download. Acesse [Microsoft SQL Server 2012 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=296473) para baixar o provedor OLE DB do Analysis Services para SQL Server 2012.<br /><br /> O MSOLAP.4 era fornecido no SQL Server 2008 e no SQL Server 2008 R2. A versão 2008 R2 oferece suporte às pastas de trabalho PowerPivot e, às vezes, precisa ser instalada manualmente nos servidores do SharePoint. Para fazer a distinção entre essas versões, você deve verificar o número da compilação nas propriedades de arquivo do provedor: vá para Arquivos de Programas\Microsoft Analysis Services\AS OLEDB\10. Clique com o botão direito do mouse em msolap110.dll e selecione **Propriedades**. Clique em **Detalhes**. Exiba as informações de versão do arquivo. A versão deve incluir 10,50. \<BuildNumber> para SQL Server 2008 R2. Para saber mais, veja [Instalar o Provedor OLE DB do Analysis Services em servidores do SharePoint](../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md) e [Provedores de dados usados para conexões do Analysis Services](data-providers-used-for-analysis-services-connections.md).<br /><br /> O MSOLAP. 3 foi lançado no SQL Server 2005.<br /><br /> O MSOLAP. 4 foi lançado no SQL Server 2008 e novamente SQL Server 2008 R2<br /><br /> O MSOLAP. 5 foi lançado no SQL Server 2012|`Provider=MSOLAP.3` é usado em conexões que exigem o SQL Server 2005 do provedor OLE DB para Analysis Services.|  
|`Cube`|Nome do cubo ou da perspectiva. Um banco de dados pode conter vários cubos e perspectivas. Quando vários destinos forem possíveis, inclua o nome do cubo ou da perspectiva na cadeia de conexão.|`Cube=SalesPerspective` mostra que você pode usar a propriedade da cadeia de conexão Cube para especificar o nome de um cubo ou de uma perspectiva.|  
  
##  <a name="authentication-and-security"></a><a name="bkmk_auth"></a>Autenticação e segurança  
 Esta seção inclui as propriedades da cadeia de conexão relacionadas à autenticação e à criptografia. O Analysis Services usa apenas a Autenticação do Windows, mas você pode definir as propriedades da cadeia de conexão a serem passadas em um nome de usuário e uma senha específicos.  
  
 As propriedades são listadas em ordem alfabética.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|`EffectiveUserName`|Use quando uma identidade de usuário final precisar ser representada no servidor. Especifique a conta em um formato domínio\usuário. Para usar essa propriedade, o chamador deve ter permissões administrativas no Analysis Services. Para obter mais informações sobre o uso dessa propriedade em uma pasta de trabalho do Excel no SharePoint, consulte [Usar o EffectiveUserName do Analysis Services no SharePoint Server 2013](https://go.microsoft.com/fwlink/?LinkId=311905). Para obter uma ilustração que demonstre como essa propriedade é usada com o Reporting Services, consulte [Usando EffectiveUserName para representar no SSAS](https://www.artisconsulting.com/blogs/greggalloway/2010/4/1/using-effectiveusername-to-impersonate-in-ssas).<br /><br /> `EffectiveUserName` é usado em uma instalação do PowerPivot para SharePoint a fim de capturar informações de uso. A identidade de usuário é fornecida ao servidor para que os eventos ou erros que incluem a identidade do usuário podem ser registrados nos arquivos de log. No caso do PowerPivot, ela não é usada para fins de autorização.|  
|**Encrypt Password**|Especifica se uma senha local será usada para criptografar cubos locais. Os valores válidos são True ou False. O padrão é False.|  
|`Encryption Password`|A senha usada para descriptografar um cubo local criptografado. O valor padrão é vazio. Esse valor deve ser explicitamente definido pelo usuário.|  
|`Impersonation Level`|Indica o nível de representação que o servidor pode usar ao representar o cliente. Os valores válidos incluem:<br /><br /> **Anônimo**: o cliente é anônimo para o servidor. O processo do servidor não pode obter informações sobre o cliente e o cliente não pode ser representado.<br /><br /> **Identificar**: o processo do servidor pode obter a identidade do cliente. O servidor pode representar a identidade do cliente para fins de autorização, mas não pode acessar objetos do sistema como cliente.<br /><br /> **Impersonate**: esse é o valor padrão. A identidade do cliente pode ser representada, mas somente quando a conexão é estabelecida, e não em cada chamada.<br /><br /> **Delegado**: o processo do servidor pode representar o contexto do Client Security ao atuar em nome do cliente. O processo do servidor também pode fazer chamadas de saída para outros servidores ao atuar em nome do cliente.|  
|`Integrated Security`|A identidade do Windows do chamador é usada para se conectar ao Analysis Services. Os valores válidos são em branco, SSPI e BASIC.<br /><br /> `Integrated Security`=`SSPI`é o valor padrão para conexões TCP, permitindo NTLM, Kerberos ou autenticação anônima. O valor padrão das conexões HTTP é em branco.<br /><br /> Ao usar `SSPI`, `ProtectionLevel` deve ser definido da seguinte maneira: `Connect`, `PktIntegrity` ou `PktPrivacy`.|  
|`Persist Encrypted`|Defina essa propriedade quando o aplicativo cliente exigir que o objeto da fonte de dados mantenha informações confidenciais de autenticação, como uma senha, em formato criptografado. Por padrão, as informações de autenticação não são mantidas.|  
|`Persist Security Info`|Os valores válidos são True e False. Quando definidas como True, as informações de segurança, como a identidade do usuário ou a senha especificada anteriormente na cadeia de conexão, poderão ser obtidas na conexão depois que ela for estabelecida. O valor padrão é False.|  
|`ProtectionLevel`|Determina o nível de segurança usado na conexão. Os valores válidos são:<br /><br /> `None`. Conexões não autenticadas ou anônimas. Não realiza nenhuma autenticação nos dados enviados ao servidor.<br /><br /> `Connect`. Conexões autenticadas. Realiza a autenticação somente quando o cliente estabelece uma relação com um servidor.<br /><br /> `PktIntegrity`. Conexões criptografadas. Verifica se todos os dados serão recebidos do cliente e se eles não foram alterados em trânsito.<br /><br /> `PktPrivacy`. Criptografia assinada, suporte apenas para XMLA. Verifica se todos os dados foram recebidos do cliente, se eles não foram alterados em trânsito, e protege a privacidade dos dados criptografando-os.<br /><br /> <br /><br /> Para obter mais informações, consulte [Establishing Secure Connections in ADOMD.NET](https://docs.microsoft.com/analysis-services/adomd/multidimensional-models-adomd-net-client/connections-in-adomd-net-establishing-secure-connections).|  
|`Roles`|Especifique uma lista delimitada por vírgulas de funções predefinidas a serem conectadas a um servidor ou banco de dados usando as permissões transmitidas por essa função. Se essa propriedade for omitida, todas as funções serão usadas, e as permissões efetivas serão a combinação de todas as funções. Definir a propriedade como um valor vazio (por exemplo, funções = ' ') a conexão do cliente não tem nenhuma associação de função.<br /><br /> Um administrador que usa essa propriedade se conecta usando as permissões transmitidas por essa função. Alguns comandos poderão apresentar falha se a função não tiver permissão suficiente.|  
|`SSPI`|Especifica explicitamente qual pacote de segurança será usado para autenticação do cliente quando a `Integrated Security` for definida como `SSPI`. O SSPI oferece suporte a vários pacotes, mas você pode usar esta propriedade para especificar um pacote específico. Os valores válidos são Negotiate, Kerberos, NTLM e Usuário Anônimo. Se esta propriedade não for definida, todos os pacotes estarão disponíveis para a conexão.|  
|`Use Encryption for Data`|Criptografa as transmissões de dados. Os valores válidos são True e False.|  
|`User ID`=...;`Password`=|`User ID`e `Password` são usados juntos. O Analysis Services representa a identidade de usuário especificada através dessas credenciais. Em uma conexão do Analysis Services, a inserção das credenciais na linha de comando é usada apenas quando o servidor é configurado para acesso HTTP, e você especificou a autenticação Básica em vez da segurança integrada no diretório virtual do IIS.<br /><br /> O nome de usuário e a senha devem ser as credenciais de uma identidade do Windows: uma conta local ou uma conta de usuário de domínio. Observe que `User ID` tem um espaço inserido. `UserName` (sem espaço) e `UID` são os outros alias possíveis para essa propriedade. O alias de `Password` é `PWD`.|  
  
##  <a name="special-purpose-parameters"></a><a name="bkmk_special"></a> Parâmetros para finalidades especiais  
 Esta seção descreve o restante dos parâmetros da cadeia de conexão. Eles são usados para assegurar os comportamentos de conexão específicos necessários a um aplicativo.  
  
 As propriedades são listadas em ordem alfabética.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|`Application Name`|Define o nome do aplicativo associado à conexão. Esse valor pode ser útil para monitorar eventos de rastreamento, especialmente quando você tem vários aplicativos que acessam os mesmos bancos de dados. Por exemplo, adicionar Application Name = ' test ' a uma cadeia de conexão faz com que ' test ' apareça em um rastreamento de SQL Server Profiler, conforme mostrado na seguinte captura de tela:<br /><br /> ![SSAS_AppNameExcample](../media/ssas-appnameexcample.gif "SSAS_AppNameExcample")<br /><br /> `sspropinitAppName` e `AppName` são os alias dessa propriedade. Para obter mais informações, consulte [Usar o parâmetro Application Name ao conectar-se ao SQL Server](https://www.connectionstrings.com/use-application-name-sql-server/).|  
|`AutoSyncPeriod`|Define a frequência (em milissegundos) de sincronização do cache do cliente e do servidor. O ADOMD.NET fornece armazenamento em cache do cliente para os objetos mais usados que tenham uma sobrecarga mínima de memória. Isso ajuda a reduzir o número de viagens de ida e volta ao servidor. O padrão é 10000 milissegundos (ou 10 segundos). Quando definida como nula ou 0, a sincronização automática é desativada.|  
|`Character Encoding`|Define como os caracteres são codificados na solicitação. Os valores válidos são Default ou UTF-8 (esses são equivalentes) e UTF-16|  
|`CompareCaseSensitiveStringFlags`|Ajusta comparações de cadeia de caracteres com diferenciação de maiúsculas e minúsculas em uma localidade especificada. Para obter mais informações sobre como definir essa propriedade, consulte [Propriedade CompareCaseSensitiveStringFlags](https://msdn.microsoft.com/library/aa237459\(v=sql.80\).aspx).|  
|`Compression Level`|Se `TransportCompression` for XPRESS, você poderá definir o nível de compactação para controlar a quantidade de compactação. Os valores válidos estão entre 0 e 9, em que 0 representa o nível mínimo de compactação e 9, o nível máximo de compactação. Quanto maior o nível de compactação, menos satisfatório será o desempenho. O valor padrão é 0.|  
|`Connect Timeout`|Determina a quantidade máxima de tempo (em segundos) que o cliente tenta uma conexão antes de atingir o tempo limite. Se uma conexão não tiver sucesso nesse período, o cliente encerrará a tentativa de conexão e gerará um erro.|  
|`MDX Compatibility`|O objetivo dessa propriedade é assegurar um conjunto consistente de comportamentos MDX para aplicativos que emitem consultas MDX. O Excel, que usa consultas MDX para preencher e calcular uma Tabela Dinâmica conectada ao Analysis Services, define essa propriedade para 1 para assegurar que os membros de espaço reservado em hierarquias desbalanceadas fiquem visíveis em uma Tabela Dinâmica. Os valores válidos são 0, 1 e 2.<br /><br /> Os valores 0 e 1 expõem os membros de espaço reservado; o valor 2 não expõe. Se essa propriedade estiver vazia, o valor 0 será assumido.|  
|`MDX Missing Member Mode=Error`|Indica se sentindo os membros ausentes são ignorados em instruções MDX. Os valores válidos são Default, Error e Ignore. Default usa um valor definido pelo servidor. Erro gera um erro quando um membro não existe. Ignore especifica que os valores ausentes devem ser ignorados.|  
|`Optimize Response`|Um bitmask que indica quais das otimizações de resposta de consulta a seguir são habilitadas.<br /><br /> 0x01: padrão. Usar o NormalTupleSet <br />0x02: Use quando as segmentações estiverem vazias|  
|`Packet Size`|Um tamanho de pacote de rede (em bytes) entre 512 e 32.767. O tamanho do pacote de rede padrão é 4096.|  
|`Protocol Format`|Define o formato do XML enviado ao servidor. Os valores válidos são Default, XML ou Binary. O protocolo é XMLA. Você pode especificar que o XML seja enviado em formato compactado (esse é o padrão), como XML bruto, ou em formato binário. O formato binário codifica os elementos e atributos XML, tornando-os menores. A compactação é um formato proprietário que reduz ainda mais o tamanho das solicitações e das respostas. Os formatos de compactação e binários são usados para acelerar as solicitações e respostas de transferências de dados.<br /><br /> Você deve usar uma biblioteca de cliente na conexão se estiver usando o formato binário ou compactado. O provedor OLE DB pode formatar as solicitações e as respostas em formato binário ou compactado. AMO e ADOMD.NET formatam as solicitações como Texto, mas aceitam respostas em formato binário ou compactado.<br /><br /> Essa propriedade de cadeia de conexão é equivalente às configurações de servidor `EnableBinaryXML` e `EnableCompression`.|  
|`Real Time Olap`|Defina esta propriedade de modo que ela ignore o armazenamento em cache, fazendo com que todas as partições escutem ativamente as notificações de consulta. Por padrão, essa propriedade não é definida.|  
|`Safety Options`|Define o nível de segurança das ações e funções definidas pelo usuário. Os valores válidos são 0, 1 e 2. Em uma conexão do Excel, essa propriedade é Safety Options=2. Detalhes sobre essa opção podem ser encontrados em <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.ConnectionString%2A>.|  
|`SQLQueryMode`|Especifica se as consultas SQL incluem cálculos. Os valores válidos são Data, Calculated e IncludeEmpty. Data significa que não serão permitidos cálculos. Calculated permite cálculos. IncludeEmpty permite cálculos e que sejam retornadas linhas vazias no resultado da consulta.|  
|`Timeout`|Especifica quanto tempo (em milissegundos) a biblioteca de cliente esperará a conclusão de um comando antes de gerar um erro.|  
|`Transport Compression`|Define como as comunicações de cliente e de servidor são compactadas, quando a compactação é especificada através da propriedade `Protocol Format`. Os valores válidos são Default, None, Compressed e `gzip`. Default significa que não há compactação para TCP ou `gzip` que não há compactação para HTTP. None indica que não será usada nenhuma compactação. Compressed usa a compactação XPRESS (SQL Server 2008 e posterior). `gzip`é válido somente para conexões HTTP, em que a solicitação HTTP inclui Accept-Encoding = gzip.|  
|`UseExistingFile`|Usado ao conectar-se a um cubo local. Essa propriedade especifica se o cubo local será substituído. Os valores válidos são True ou False. Se definido como True, o arquivo de cubo deve existir. O arquivo existente será o destino da conexão. Se for definido como False, o arquivo de cubo será substituído.|  
|`VisualMode`|Defina essa propriedade para controlar como os membros serão agregados quando a segurança da dimensão for aplicada.<br /><br /> No caso dos dados de cubo que todos podem ver, a agregação de todos os membros faz sentido porque todos os valores que contribuem para o total ficam visíveis. No entanto, se você filtrar ou restringir as dimensões com base na identidade do usuário, a exibição de um total com base em todos os membros (combinando valores restritos e permitidos em um único total) pode ser confusa ou mostrar mais informações do que devem ser reveladas.<br /><br /> Para especificar como os membros serão agregados quando a segurança da dimensão for aplicada, você poderá definir essa propriedade como True para usar somente os valores permitidos na agregação ou como False para excluir os valores restritos do total.<br /><br /> Quando definido na cadeia de conexão, esse valor se aplicará ao nível do cubo ou da perspectiva. Em um modelo, você pode controlar os totais visuais em um nível mais granular.<br /><br /> Os valores válidos são 0, 1 e 2.<br /><br /> 0 é o padrão. Atualmente, o comportamento padrão é equivalente a 2, no qual as agregações incluem valores que ficam ocultos para o usuário.<br /><br /> O valor 1 exclui os valores ocultos do total. Esse é o padrão para Excel.<br /><br /> O valor 2 inclui valores ocultos no total. Esse é o valor padrão no servidor.<br /><br /> <br /><br /> `Visual Total` ou `Default MDX Visual Mode` é o alia dessa propriedade.|  
  
##  <a name="reserved-for-future-use"></a><a name="bkmk_reserved"></a>Reservado para uso futuro  
 As propriedades a seguir são permitidas em uma cadeia de conexão, mas não funcionam nas versões atuais do Analysis Services.  
  
-   Usuário Autenticado  
  
-   Autenticação de Cache  
  
-   Modo de Cache (o uso desta propriedade foi investigado nas versões anteriores. Embora você talvez encontre postagens de blog que recomendam seu uso, evite definir essa propriedade, a menos que seja instruído pelo Suporte da Microsoft).  
  
-   Política de Cache  
  
-   Taxa do Cache  
  
-   Taxa do Cache2  
  
-   Limite Dinâmico de Depuração  
  
-   Modo de depuração  
  
-   Mode  
  
-   Compatibilidade SQL  
  
-   Usar Cache de Fórmulas  
  
##  <a name="example-connection-strings"></a><a name="bkmk_examples"></a>Exemplo de cadeias de conexão  
 Esta seção mostra a cadeia de conexão que você provavelmente usará ao configurar uma conexão de Analysis Services em aplicativos comumente usados.  
  
 **Cadeia de conexão genérica**  
  
 Você pode usar uma cadeia de conexão como esta se estiver configurando uma conexão no Reporting Services.  
  
 `Data source=<servername>; initial catalog=<databasename>`  
  
 **Cadeia de conexão no Excel**  
  
 A cadeia de conexão padrão ADOMD.NET no Excel especifica o provedor de dados, o servidor, o nome do banco de dados e a segurança integrada do Windows. O nível de compatibilidade MDX é sempre definido como 1. Embora você possa alterar o valor para a sessão atual, o Excel redefinirá a compatibilidade de MDX para 1 quando o arquivo for aberto em seguida.  
  
 `Provider=MSOLAP.5;Integrated Security=SSPI;Persist Security Info=True;Initial Catalog=Adventure Works DW 2008R2;Data Source=AW-SRV01;MDX Compatibility=1;Safety Options=2;MDX Missing Member Mode=Error`  
  
 Para obter mais informações, consulte [conexões de dados, fontes de dados e cadeias de conexão em Reporting Services](../../reporting-services/data-connections-data-sources-and-connection-strings-in-reporting-services.md) e [autenticação de dados para serviços do Excel no SharePoint Server 2013](https://go.microsoft.com/fwlink/?LinkId=296350).  
  
##  <a name="connection-string-formats-used-in-analysis-services"></a><a name="bkmk_supportedstrings"></a> Formatos de cadeia de conexão usados no Analysis Services  
 Esta seção lista todos os formatos de cadeia de conexão com suporte do Analysis Services. Com a exceção de conexões a bancos de dados PowerPivot, você pode especificar essas cadeias de conexão em aplicativos que se conectam ao Analysis Services.  
  
 **Conexões nativas (ou diretas) com o servidor**  
  
 `Data Source=server[:port][\instance]`onde "Port" e "\instance" são opcionais. Por exemplo, a especificação de "Data Source = server1" abre uma conexão com a instância padrão (e a porta padrão 2383) em um servidor chamado "Server1".  
  
 "Data Source = server1: port1" abrirá uma conexão com uma instância Analysis Services em execução na porta "port1" em "Server1".  
  
 "Data Source = server1\instance1" abrirá uma conexão com SQL Browser (em sua porta padrão 2382), resolverá a porta para a instância nomeada "instance1" e, em seguida, abrirá a conexão com essa porta de Analysis Services.  
  
 "Data Source = server1: port1\instance1" abrirá uma conexão com SQL Browser em "port1", resolverá a porta para a instância nomeada "instance1" e, em seguida, abrirá a conexão com essa porta de Analysis Services.  
  
 **Conexões de cubos locais (arquivos .cub)**  
  
 `Data Source=<path>`, por exemplo, "Data Source = c:\temp\a.Cub"  
  
 **Conexões de http(s) para msmdpump.dll**  
  
 `Data Source=<URL>`, onde a URL é o endereço HTTP ou HTTPS para a pasta IIS virtual que contém o msmdpump.dll. Para obter mais informações, consulte [Configurar o acesso HTTP ao Analysis Services no IIS &#40;(Serviços de Informações da Internet)&#41; 8.0](configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
 **Conexões de http para pastas de trabalho PowerPivot (arquivos .xlsx, .xlsb ou .xlsm)**  
  
 `Data Source=<URL>`, onde a URL é o caminho do SharePoint para uma pasta de trabalho PowerPivot que foi publicada em uma biblioteca do SharePoint. Por exemplo, "Data Source =<http://localhost/Shared> Documents/Sales. xlsx".  
  
 **Conexões http(s) com arquivos de Conexão do Modelo Semântico de BI**  
  
 `Data Source=<URL>` em que a URL é o caminho do SharePoint até o arquivo .bism. Por exemplo, "Data Source =<http://localhost/Shared> Documents/Sales. BISM".  
  
 **Conexões do PowerPivot inseridas**  
  
 `Data Source=$Embedded$` onde $embedded$ é um moniker que se refere a um modelo de dados PowerPivot inserido na pasta de trabalho. Esta cadeia de conexão é criada e gerenciada internamente. Não modifique-a. As cadeias de conexão inseridas são resolvidas pelo suplemento PowerPivot para Excel em estações de trabalho cliente ou por instâncias do PowerPivot para SharePoint em um farm do SharePoint.  
  
 **Contexto de servidor local em procedimentos armazenados do Analysis Services**  
  
 `Data Source=*`, em que * é resolvido como a instância local.  
  
##  <a name="encrypting-connection-strings"></a><a name="bkmk_encrypt"></a> Criptografando cadeias de conexão  
 O[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] criptografa e armazena as cadeias de conexão usadas para a conexão a cada uma de suas fontes de dados. Se a conexão a uma fonte de dados exigir nome de usuário e senha, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pode armazenar o nome e a senha com a cadeia de conexão ou solicitar o nome e a senha sempre que for necessário se conectar a uma fonte de dados. Quando o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solicita informações do usuário, isso indica que essas informações não precisam ser armazenadas e criptografadas. No entanto, se essas informações forem armazenadas na cadeia de conexão, será necessário criptografá-las e protegê-las.  
  
 Para criptografar e proteger as informações da cadeia de conexão, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa a API de Proteção aos Dados. O[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa uma chave de criptografia separada para criptografar informações da cadeia de conexão para cada banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . O[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cria essa chave durante a criação de um banco de dados e criptografa as informações da cadeia de conexão com base na conta de inicialização do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Quando o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] inicia, a chave criptografada para cada banco de dados é lida, descriptografada e armazenada. Em seguida, o[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa a chave descriptografada adequada para descriptografar as informações da cadeia de conexão da fonte de dados quando o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] precisa se conectar a uma fonte de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar o acesso HTTP para Analysis Services em Serviços de Informações da Internet &#40;IIS&#41; 8,0](configure-http-access-to-analysis-services-on-iis-8-0.md)   
 [Configurar Analysis Services para delegação restrita de Kerberos](configure-analysis-services-for-kerberos-constrained-delegation.md)   
 [Provedores de dados usados para conexões de Analysis Services](data-providers-used-for-analysis-services-connections.md)   
 [Conectar ao Analysis Services](connect-to-analysis-services.md)  
  
  
