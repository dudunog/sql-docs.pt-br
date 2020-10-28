---
title: Edições e recursos com suporte
titleSuffix: SQL Server 2016
description: Este artigo descreve os recursos compatíveis com as várias edições do SQL Server 2016, que acomodam diferentes requisitos de desempenho, runtime e preço.
ms.custom:
- seo-lt-2019
- sqlfreshmay19
ms.date: 07/22/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: conceptual
helpviewer_keywords:
- Enterprise Edition [SQL Server]
- Developer Edition [SQL Server]
- 32-bit vs. 64-bit editions [SQL Server]
- default components
- Workgroup Edition [SQL Server]
- Internet servers [SQL Server]
- installing SQL Server, components
- Setup [SQL Server], components
- SQL Server, editions
- SQL Server, components
- client/server applications [SQL Server]
- editions [SQL Server]
- versions [SQL Server]
- Setup [SQL Server], editions
- SQL Server Installation Wizard
- components [SQL Server]
- Standard Edition [SQL Server]
- 64-bit edition [SQL Server]
- IIS [SQL Server]
- installing SQL Server, editions
- editions [SQL Server], about edition options
- Setup [SQL Server]
- CPSA
ms.assetid: e5186f02-dd91-47d0-8fa4-de3f41c76903
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8803d517b0f3917853261dc8bd6591123f4c3404
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "92255294"
---
# <a name="editions-and-supported-features-of-sql-server-2016"></a>Edições e recursos com suporte do SQL Server 2016
[!INCLUDE [SQL Server 2016](../includes/applies-to-version/sqlserver2016.md)]  

Este tópico fornece detalhes dos recursos compatíveis com as edições do SQL Server.

Para obter informações sobre outras versões, confira:

* [SQL Server 2019](editions-and-components-of-sql-server-version-15.md).  
* [SQL Server 2017](editions-and-components-of-sql-server-2017.md).  
* [SQL Server 2014](/previous-versions/sql/2014/getting-started/features-supported-by-the-editions-of-sql-server-2014?view=sql-server-2014).

Os requisitos de instalação variam de acordo com as necessidades do aplicativo. As diferentes edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] acomodam desempenho, runtime e requisitos de preço exclusivos para organizações e indivíduos. Os componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que você instala dependem também dos seus requisitos específicos. As seções a seguir ajudarão você a entender como fazer a melhor escolha entre as edições e os componentes disponíveis no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  

A edição Evaluation do SQL Server está disponível por um período de avaliação de 180 dias.  
  
Para notas de versão mais recentes e informações sobre novidades, consulte o seguinte:
- [Notas de versão do SQL Server 2017](../sql-server/sql-server-2017-release-notes.md)
- [Notas de versão do SQL Server 2016](../sql-server/sql-server-2016-release-notes.md)
- [Novidades no SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)
- [Novidades no SQL Server 2016](../sql-server/what-s-new-in-sql-server-2016.md)

### <a name="try-sql-server"></a>Experimente o SQL Server.    
    
> [![Download no Centro de Avaliação](https://docs.microsoft.com/analysis-services/analysis-services/media/download.png)](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) **[Download do SQL Server 2016 no Centro de Avaliação](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**    
> 
> ![A máquina virtual pequena do Azure](/analysis-services/analysis-services/media/azure-virtual-machine-small.png) **[Criar uma máquina virtual com o SQL Server 2016 já instalado](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftsqlserver.sql2017-ws2019?tab=Overview)**   
  
## <a name="ssnoversion-editions"></a>[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Edições  
 A tabela a seguir descreve essas edições do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. 
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] edição|Definição|  
|---------------------------------------|----------------|  
|Enterprise|A oferta Premium, edição [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Enterprise, fornece recursos de datacenter abrangentes de alta tecnologia com desempenho incrivelmente rápido, virtualização ilimitada e business intelligence de ponta a ponta – oferecendo altos níveis de serviço para cargas de trabalho críticas e acesso a insights de dados para usuários finais.|  
|Standard|A edição [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Standard fornece gerenciamento de dados básicos e bancos de dados de business intelligence para departamentos e pequenas empresas executarem seus aplicativos e dá suporte a ferramentas de desenvolvimento comuns para rede local e em nuvem – permitindo o gerenciamento eficiente de bancos de dados com mínimos recursos de TI.|  
|Web|O [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Web Edition é uma opção de baixo custo total de propriedade para hospedagem de sites e VAPs da Web que fornece recursos de escalabilidade, economia e capacidade de gerenciamento para propriedades da Web de pequeno a grande porte.|  
|Desenvolvedor|A edição[!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] Developer permite que os desenvolvedores criem qualquer tipo de aplicativo com base no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Ele inclui todas as funcionalidades da edição Enterprise, mas é licenciado para ser usado como um sistema de teste e desenvolvimento, e não como um servidor de produção. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer é uma opção ideal para pessoas que criam [!INCLUDE[ssNoVersion](../includes/ssNoVersion-md.md)] e testam aplicativos.|  
|Edições Express|A edição Express é o banco de dados gratuito de nível de entrada, ideal para conhecer e criar aplicativos de área de trabalho e aplicativos controlados por dados de pequenos servidores. É a melhor escolha para fornecedores de software independente, desenvolvedores e interessados que criam aplicativos cliente. Se precisar de recursos mais avançados de banco de dados, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express pode ser perfeitamente atualizado para versões mais sofisticadas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Express LocalDB é uma versão leve do Express que tem todos os seus recursos de programação, embora seja executado no modo de usuário, além de contar com uma instalação rápida e sem nenhuma configuração e uma lista curta de pré-requisitos.|  
  
## <a name="using-ssnoversion-with-an-internet-server"></a>Usando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com um servidor de Internet  
 Em um servidor de Internet, como um servidor que executa o IIS (Serviços de Informações da Internet), você instalará normalmente as ferramentas cliente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Essas ferramentas incluem os componentes cliente de conectividade usados por um aplicativo que se conecta a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!NOTE]
> Apesar de ser possível instalar uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um computador que executa o IIS, isso é feito normalmente apenas para pequenos sites da Web que possuem um único computador servidor. A maioria dos sites da Web possui sistemas IIS de camada intermediária em um servidor ou em clusters de servidores e bancos de dados em um servidor diferente ou em uma federação de servidores.  
  
## <a name="using-ssnoversion-with-clientserver-applications"></a>Usando o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] com aplicativos cliente/servidor  
 Você pode instalar apenas os componentes cliente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um computador que esteja executando aplicativos cliente/servidor que se conectam diretamente a uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. A instalação dos componentes cliente é também uma boa opção se você administra uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em um servidor de banco de dados ou se planeja desenvolver aplicativos no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 A opção de ferramentas cliente instala os seguintes recursos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] : componentes compatíveis com versões anteriores, [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], componentes de conectividade, ferramentas de gerenciamento, Software Development Kit e componentes dos Manuais Online do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para obter mais informações, consulte [Instalar o SQL Server](../database-engine/install-windows/install-sql-server.md).  
  
## <a name="deciding-among-ssnoversion-components"></a>Decidindo entre os componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
 Use a página Seleção de Recursos do Assistente de Instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para selecionar os componentes a serem incluídos em uma instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Por padrão, nenhum dos recursos na árvore está selecionado.  
  
 Use as informações nas tabelas a seguir para determinar o conjunto de recursos mais adequado às suas necessidades.  
  
|Componentes de servidor|Descrição|  
|-----------------------|-----------------|  
|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|[!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] inclui [!INCLUDE[ssDE](../includes/ssde-md.md)], o serviço principal para armazenamento, processamento e proteção de dados, replicação, pesquisa de texto completo, ferramentas para gerenciar dados XML e relacionais, na integração da análise de banco de dados e na integração do PolyBase para acesso ao Hadoop e a outras fontes de dados heterogêneas, bem como o servidor [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS).|  
|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] inclui as ferramentas para criação e gerenciamento de aplicativos OLAP (processamento analítico online) e de mineração de dados.|  
|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|O[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] inclui componentes de servidor e cliente por criar, gerenciar e implantar relatórios tabulares, de matriz, gráficos e de forma livre. O[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] também é uma plataforma extensível que você pode usar para desenvolver aplicativos de relatório.|  
|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] é um conjunto de ferramentas gráficas e objetos programáveis para mover, copiar e transformar dados. Ele também inclui o componente [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) para o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].|  
|[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]|O[!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] (MDS) é a solução do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para gerenciamento de dados mestre. O MDS pode ser configurado para gerenciar qualquer domínio (produtos, clientes, contas) e inclui hierarquias, segurança granular, transações, controle de versão de dados e regras de negócio, bem como um [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)] que pode ser usado para gerenciar dados.|  
|[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)]|[!INCLUDE[rsql_productname](../includes/rsql-productname-md.md)] dá suporte a soluções R distribuídas e escalonáveis em várias plataformas e usando várias fontes de dados empresariais, incluindo Linux, Hadoop e Teradata.|  
  
|Ferramentas de gerenciamento|Descrição|  
|----------------------|-----------------|  
|[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]|O[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] é um ambiente integrado para acessar, configurar, gerenciar, administrar e desenvolver os componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. O[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] permite que os desenvolvedores e administradores de todos os níveis utilizem o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].<br /><br /> Baixar e instalar <br />                [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] de  [Baixar o SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager|O[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Configuration Manager fornece gerenciamento básico de configuração para serviços, protocolos do servidor, protocolos do cliente e aliases do cliente do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]|  
|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]|[!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] fornece uma interface gráfica do usuário para monitorar uma instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] ou do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].|  
|[!INCLUDE[ssDE](../includes/ssde-md.md)] Orientador de Otimização|O Orientador de Otimização do[!INCLUDE[ssDE](../includes/ssde-md.md)] ajuda a criar conjuntos de índices, exibições indexadas e partições ideais.|  
|Cliente Data Quality|Fornece uma interface gráfica do usuário altamente simples e intuitiva para se conectar ao servidor DQS e executar operações de limpeza de dados. Ele também permite monitorar centralmente várias atividades executadas durante a operação de limpeza de dados.|  
|[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]|O[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] oferece um IDE para criar soluções para os componentes de Business Intelligence: [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]e [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].<br /><br /> (Antes chamado de Business Intelligence Development Studio).<br /><br /> O[!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] também inclui "Projetos de banco de dados" que oferecem um ambiente integrado para desenvolvedores de banco de dados realizarem seu trabalho de design de banco de dados para qualquer plataforma [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (no local e fora do local) no Visual Studio. Os desenvolvedores de banco de dados podem usar o Gerenciador de Servidores aprimorado no Visual Studio para criar ou editar facilmente objetos de banco de dados e dados, ou executar consultas.|  
|Componentes de conectividade|Instala componentes para comunicação entre clientes e servidores, e bibliotecas de rede para DB-Library, ODBC e OLE DB.|  
  
|Documentação|Descrição|  
|-------------------|-----------------|  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Manuais Online|Documentação principal do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].| 

**Edições Developer e Evaluation**  
Para saber quais os recursos com suporte nas edições Developer e Evaluation, consulte os recursos listados para o SQL Server Enterprise Edition nas tabelas abaixo.


A Developer edition continua a dar suporte a apenas um cliente para o [SQL Server Distributed Replay](../tools/distributed-replay/sql-server-distributed-replay.md). 
  
##  <a name="scale-limits"></a><a name="Cross-BoxScaleLimits"></a> Scale Limits  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|
|Capacidade máxima de computação usada por uma única instância – [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]<sup>1</sup>|Máximo do sistema operacional|Limitado a menos de 4 soquetes ou 24 núcleos|Limitado a menos de 4 soquetes ou 16 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|Limitado a menos de 1 soquete ou 4 núcleos| 
|Capacidade máxima de computação usada por uma única instância – [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] ou [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Máximo do sistema operacional|Limitado a menos de 4 soquetes ou 24 núcleos|Limitado a menos de 4 soquetes ou 16 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|Limitado a menos de 1 soquete ou 4 núcleos|  
|Memória máxima para o pool de buffers por instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Máximo do sistema operacional|128 GB|64 GB|1410 MB|1410 MB|
|Máximo de memória para cache do segmento Columnstore por instância do [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memória ilimitada| 32 GB<sup>2</sup>| 16 GB<sup>2</sup>| 352 MB<sup>2</sup>| 352 MB<sup>2</sup>|  
|Tamanho de dados máximo otimizado para memória de acordo com banco de dados em [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]|Memória ilimitada| 32 GB<sup>2</sup>| 16 GB<sup>2</sup>| 352 MB<sup>2</sup>| 352 MB<sup>2</sup>|  
|Memória máxima utilizada por instância de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]|Máximo do sistema operacional|Tabela: 16 GB<br /><br /> MOLAP: 64 GB|N/D|N/D|N/D|  
|Memória máxima utilizada por instância de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]|Máximo do sistema operacional|64 GB|64 GB|4 GB|N/D|
|Tamanho máximo do banco de dados relacional|524 PB|524 PB|524 PB|10 GB|10 GB|  
  
<sup>1</sup> O Enterprise Edition com Servidor + licenciamento baseado em CAL (Licença de Acesso para Cliente) (não disponível para novos contratos) é limitado ao máximo de 20 núcleos por instância do SQL Server. Não há limites no modelo de Licenciamento de Servidor Baseado em Núcleo. Para saber mais, confira [Compute Capacity Limits by Edition of SQL Server](../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
<sup>2</sup> Aplica-se ao [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1 como parte da criação de uma CPSA (área de superfície de programação comum) em todas as edições. 

##  <a name="rdbms-high-availability"></a><a name="RDBMSHA"></a> RDBMS High Availability  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Suporte do Server Core <sup>1</sup>|Sim|Sim|Sim|Sim|Sim|  
|Envio de logs|Sim|Sim|Sim|Não|Não|  
|Espelhamento de banco de dados|Sim|Sim<br /><br /> Somente segurança completa|Somente testemunha|Somente testemunha|Somente testemunha| 
|Compactação de backup|Sim|Sim|Não|Não|Não| 
|Instantâneo do banco de dados|Sim|Sim <sup>3</sup>|Sim <sup>3</sup>|Sim <sup>3</sup>|Sim <sup>3</sup>|
|Instâncias do cluster de failover do AlwaysOn|Yes<br /><br /> 16|Sim<br /><br /> Suporte para 2 nós|Não|Não|Não|  
|Grupos de disponibilidade AlwaysOn|Yes<br /><br /> Até 8 réplicas secundárias, incluindo 2 réplicas secundárias síncronas|Não|Não|Não|Não|
|Grupos de disponibilidade básicos <sup>2</sup>|Não|Sim<br /><br /> Suporte para 2 nós|Não|Não|Não|
|Restauração de arquivo e página online|Sim|Não|Não|Não|Não|
|Indexação online|Sim|Não|Não|Não|Não|
|Alteração de esquema online|Sim|Não|Não|Não|Não|
|Recuperação rápida|Sim|Não|Não|Não|Não|
|Backups espelhados|Sim|Não|Não|Não|Não|
|Adição de memória a quente e CPU|Sim|Não|Não|Não|Não|
|Supervisor de recuperação de banco de dados|Sim|Sim|Sim|Sim|Sim|
|Backup criptografado|Sim|Sim|Não|Não|Não|
|Backup híbrido para o Azure (backup para URL)|Sim|Sim|Não|Não|Não|  
  
 <sup>1</sup> Para obter mais informações sobre a instalação do SQL Server no Server Core, consulte [Instalar o SQL Server no Server Core](../database-engine/install-windows/install-sql-server-on-server-core.md). 

<sup>2</sup> Para obter mais informações sobre Grupos de disponibilidade básicos, consulte [Grupos de disponibilidade básicos](../database-engine/availability-groups/windows/basic-availability-groups-always-on-availability-groups.md).  

<sup>3</sup> Aplica-se ao [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)] 2016 SP1 como parte da criação de uma CPSA (área de superfície de programação comum) em todas as edições. 
  
##  <a name="rdbms-scalability-and-performance"></a><a name="RDBMSSP"></a> RDBMS Scalability and Performance  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Columnstore <sup>1</sup>|Sim|Sim <sup>2</sup>|Sim <sup>2</sup>|Sim<sup>2</sup>|Sim<sup>2</sup>|  
|OLTP na memória <sup>1</sup>|Sim|Sim <sup>2</sup>|Sim <sup>2</sup>|Sim <sup>2</sup>, <sup>3</sup>|Sim <sup>2</sup>|
|Stretch Database|Sim|Sim|Sim|Sim|Sim|
|Memória principal persistente|Sim|Sim|Sim|Sim|Sim|
|Suporte de várias instâncias|50|50|50|50|50|
|Particionamento de tabela e índice|Sim|Sim <sup>2</sup>|Sim <sup>2</sup>|Sim <sup>2</sup>|Sim <sup>2</sup>|  
|Compactação de dados|Sim|Sim <sup>2</sup>|Sim <sup>2</sup>|Sim <sup>2</sup>|Sim <sup>2</sup>|
|Administrador de Recursos|Sim|Não|Não|Não|Não|  
|Paralelismo de tabela particionada|Sim|Não|Não|Não|Não|
|Contêineres de vários fluxos de arquivos|Sim|Sim <sup>2</sup>|Sim <sup>2</sup>|Sim <sup>2</sup>|Sim <sup>2</sup>|
|Memória de página grande com reconhecimento para NUMA e alocação de matriz de buffer|Sim|Não <sup>4</sup>|Não|Não|Não|
|Buffer Pool Extension|Sim|Sim|Não|Não|Não|
|Governança de recursos de E/S|Sim|Não|Não|Não|Não|
|Read-Ahead|Sim|Não|Não|Não|Não|
|Exame avançado|Sim|Não|Não|Não|Não|
|Durabilidade atrasada|Sim|Sim|Sim|Sim|Sim|

<sup>1</sup> Tamanho de dados de OLTP na memória e cache do segmento Columnstore são limitados a quantidade de memória especificada por edição na seção limites de escala. Os graus de máximos de paralelismo é limitado. Os graus de paralelismo do processo (DOP) de criação de um índice é limitado a 2 DOP para a Standard Edition e 1 DOP para a Web e a Express Editions. Refere-se a índices de columnstore criados em tabelas baseadas em disco e tabelas com otimização de memória.

<sup>2</sup> Aplica-se ao [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1 como parte da criação de uma CPSA (área de superfície de programação comum) em todas as edições. Aplicação de agregação, aplicação de predicado de cadeia de caracteres e otimizações de SIMD são aprimoramentos de escalabilidade do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Edição Enterprise. Para obter mais detalhes, confira [Índices columnstore – novidades](../relational-databases/indexes/columnstore-indexes-what-s-new.md). 

<sup>3</sup> Esse recurso não está incluído na opção de instalação LocalDB.

<sup>4</sup> O licenciamento baseado em Standard Edition e SQL Server + CAL pode restringir a quantidade de processadores que o SQL Server Standard pode usar, embora o SQL Server Standard seja habilitado para NUMA. 
##  <a name="rdbms-security"></a><a name="RDBMSS"></a> RDBMS Security  
  
|Recurso|Enterprise|Standard|Web|Express|Express with Advanced Services|  
|-------------|----------------|--------------|---------|-------------|------------------------------------| 
|Segurança em nível de linha|Sim|Sim|Sim <sup>1</sup>|Sim <sup>1</sup>|Sim <sup>1</sup>|  
|Always Encrypted|Sim|Sim <sup>1</sup>|Sim <sup>1</sup>|Sim <sup>1</sup>|Sim <sup>1</sup>| 
|Mascaramento de dados dinâmicos|Sim|Sim|Sim <sup>1</sup>|Sim <sup>1</sup>|Sim <sup>1</sup>|   
|Auditoria de servidor|Sim|Sim|Sim|Sim|Sim| 
|Auditoria de banco de dados|Sim|Sim <sup>1</sup>|Sim <sup>1</sup>|Sim <sup>1</sup>|Sim <sup>1</sup>| 
|Criptografia transparente do banco de dados|Sim|Não|Não|Não|Não|   
|Gerenciamento extensível de chaves|Sim|Não|Não|Não|Não| 
|Funções definidas pelo usuário|Sim|Sim|Sim|Sim|Sim| 
|Bancos de dados independentes|Sim|Sim|Sim|Sim|Sim| 
|Criptografia para backups|Sim|Sim|Não|Não|Não|  

<sup>1</sup> Aplica-se ao [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1 como parte da criação de uma CPSA (área de superfície de programação comum) em todas as edições.      

##  <a name="replication"></a><a name="Replication"></a> Replicação  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Assinantes heterogêneos|Sim|Sim|Não|Não|Não|  
|Replicação de mesclagem|Sim|Sim|Sim (somente assinante)|Sim (somente assinante)|Sim (somente assinante)|   
|publicação Oracle|Sim|Não|Não|Não|Não| 
|Replicação transacional ponto a ponto|Sim|Não|Não|Não|Não|   
|Replicação de instantâneo|Sim|Sim|Sim (somente assinante)|Sim (somente assinante)|Sim (somente assinante)|   
|Controle de alterações do SQL Server|Sim|Sim|Sim|Sim|Sim| 
|Replicação transacional|Sim|Sim|Sim (somente assinante)|Sim (somente assinante)|Sim (somente assinante)|   
|Replicação transacional no Azure|Sim|Sim|Não|Não|Não|   
|Assinatura atualizável de replicação transacional|Sim|Sim|Não|Não|Não|  
  
##  <a name="management-tools"></a><a name="SSMS"></a> Management Tools  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|SQL Management Objects (SMO)|Sim|Sim|Sim|Sim|Sim|  
|SQL Configuration Manager|Sim|Sim|Sim|Sim|Sim|   
|SQL CMD (ferramenta de prompt de comando)|Sim|Sim|Sim|Sim|Sim|      
|Distributed Replay – Ferramenta de Administração|Sim|Sim|Sim|Sim|Não|  
|Distributed Replay – Cliente|Sim|Sim|Sim|Não|Não|  
|Distributed Replay - Controller|Sim (Até 16 clientes)|Sim (1 cliente)|Sim (1 cliente)|Não|Não|   
|SQL Profiler|Sim|Sim|Não <sup>1</sup>|Não <sup>1</sup>|Não <sup>1</sup>|  
|SQL Server Agent|Sim|Sim|Sim|Não|Não| 
|Pacote de gerenciamento do Microsoft System Center Operations Manager|Sim|Sim|Sim|Não|Não|  
|Database Tuning Advisor (DTA)|Sim|Sim <sup>2</sup>|Sim <sup>2</sup>|Não|Não|      
  
 <sup>1</sup> SQL Server Web, SQL Server Express, SQL Server Express with Tools e SQL Server Express with Advanced Services podem ter o perfil criado usando as edições SQL Server Enterprise e Standard.  
  
 <sup>2</sup> Ajuste habilitado somente em recursos da edição Standard  
  
##  <a name="rdbms-manageability"></a><a name="RDBMSM"></a> RDBMS Manageability  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Instâncias de usuário|Não|Não|Não|Sim|Sim| 
|LocalDB|Não|Não|Não|Sim|Não| 
|Conexão dedicada de administrador|Sim|Sim|Sim|Sim, com o sinalizador de rastreamento|Sim, com o sinalizador de rastreamento|   
|Suporte de scripts PowerShell|Sim|Sim|Sim|Sim|Sim| 
|Suporte a SysPrep <sup>1</sup>|Sim|Sim|Sim|Sim|Sim| 
|Suporte para operações de componente do aplicativo da camada de dados – extrair, implantar, atualizar, excluir|Sim|Sim|Sim|Sim|Sim| 
|Automação de política (verificação de agenda e alterações)|Sim|Sim|Sim|Não|Não|   
|Coletor de dados de desempenho|Sim|Sim|Sim|Não|Não| 
|Pode se inscrever como uma instância gerenciada no gerenciamento de várias instâncias|Sim|Sim|Sim|Não|Não|   
|Relatórios de desempenho padrão|Sim|Sim|Sim|Não|Não| 
|Guias de plano e planejar congelamento para guias de plano|Sim|Sim|Sim|Não|Não|   
|Direcione a consulta de exibições indexadas (usando a dica de NOEXPAND)|Sim|Sim|Sim|Sim|Sim| 
|Manutenção automática de exibições indexadas|Sim|Sim|Sim|Não|Não| 
|Exibições particionadas distribuídas|Sim|Não|Não|Não|Não| 
|Operações indexadas paralelas|Sim|Não|Não|Não|Não|  
|Uso automático da exibição indexada através do otimizador de consulta|Sim|Não|Não|Não|Não| 
|Verificação de consistência paralela|Sim|Não|Não|Não|Não| 
|Ponto de controle do Utilitário do SQL Server|Sim|Não|Não|Não|Não|    
|Extensão do pool de buffers|Sim|Sim|Não|Não|Não| 
  
 <sup>1</sup> Para obter mais informações, veja [Considerações para instalação do SQL Server usando SysPrep](../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md).  
 
<sup>2</sup> Aplica-se ao [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1 como parte da criação de uma CPSA (área de superfície de programação comum) em todas as edições.      
  
##  <a name="development-tools"></a><a name="DevTools"></a> Development Tools  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express| 
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Integração do Microsoft Visual Studio|Sim|Sim|Sim|Sim|Sim| 
|Intellisense (Transact-SQL e MDX)|Sim|Sim|Sim|Sim|Sim| 
|SQL Server Data Tools (SSDT)|Sim|Sim|Sim|Sim|Não|    
|Ferramentas de design, depuração e edição do MDX|Sim|Sim|Não|Não|Não|   
  
##  <a name="programmability"></a><a name="Programmability"></a> Programmability  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express 
|-------------|----------------|--------------|---------|------------------------------------|------------------------|  
|Integração básica do R|Sim|Sim|Sim|Sim|Não|   
|Integração avançada do R|Sim|Não|Não|Não|Não| 
|R Server (Autônomo)|Sim|Não|Não|Não|Não|   
|Nó de computação do PolyBase|Sim|Sim <sup>1</sup>|Sim <sup>1</sup>, <sup>2</sup>|Sim <sup>1</sup>, <sup>2</sup>|Sim <sup>1</sup>, <sup>2</sup>| 
|Nó de cabeçalho do PolyBase|Sim|Não|Não|Não|Não| 
|JSON|Sim|Sim|Sim|Sim|Sim|   
|Repositório de Consultas|Sim|Sim|Sim|Sim|Sim|   
|Temporal|Sim|Sim|Sim|Sim|Sim|   
|Integração do CLR (Common Language Runtime)|Sim|Sim|Sim|Sim|Sim|   
|Suporte a XML nativo|Sim|Sim|Sim|Sim|Sim| 
|Indexação XML|Sim|Sim|Sim|Sim|Sim| 
|Funcionalidades MERGE e UPSERT|Sim|Sim|Sim|Sim|Sim|   
|suporte a FILESTREAM|Sim|Sim|Sim|Sim|Sim| 
|FileTable|Sim|Sim|Sim|Sim|Sim| 
|Tipos de dados de Data e Hora|Sim|Sim|Sim|Sim|Sim|  
|Suporte à internacionalização|Sim|Sim|Sim|Sim|Sim| 
|Pesquisa semântica e de texto completo|Sim|Sim|Sim|Sim|Não| 
|Especificação de idioma em consulta|Sim|Sim|Sim|Sim|Não|   
|Service Broker (mensagens)|Sim|Sim|Não (Somente cliente)|Não (Somente cliente)|Não (Somente cliente)|   
|pontos de extremidade Transact-SQL|Sim|Sim|Sim|Não|Não| 

<sup>1</sup> Expansão com vários nós de computação requer um nó de cabeçalho.

<sup>2</sup> Aplica-se ao [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1 como parte da criação de uma CPSA (área de superfície de programação comum) em todas as edições.     
  
## <a name="integration-services"></a><a name="IS"></a> Integration Services

Para obter informações sobre os recursos do SSIS (Integration Services) com suporte nas edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [Recursos do Integration Services com suporte nas edições do SQL Server](../integration-services/integration-services-features-supported-by-the-editions-of-sql-server.md).

##  <a name="master-data-services"></a><a name="MDS"></a> Master Data Services  
 Para obter mais informações sobre o [!INCLUDE[ssMDSshort_md](../includes/ssmdsshort-md.md)] e os recursos do Data Quality Services compatíveis com as edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [Recursos do Master Data Services e do Data Quality Services compatíveis com as edições do SQL Server](../master-data-services/master-data-services-and-data-quality-services-features-support.md). 

  
##  <a name="data-warehouse"></a><a name="DW"></a> Data Warehouse  
  
|Recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|-------------|----------------|--------------|---------|------------------------------------|------------------------| 
|Criar cubos sem um banco de dados|Sim|Sim|Não|Não|Não |   
|Gerar automaticamente esquema de preparo e data warehouse|Sim|Sim|Não|Não|Não| 
|captura de dados de alterações|Sim|Sim <sup>1</sup>|Não|Não|Não| 
|Otimizações de consulta de junção em estrela|Sim|Não|Não|Não|Não| 
|Configuração escalonável somente leitura do Analysis Services|Sim|Não|Não|Não|Não| 
|Processamento paralelo de consultas em tabelas e índices particionados|Sim|Não|Não|Não|Não|   
|Agregação em lote global|Sim|Não|Não|Não|Não| 

<sup>1</sup> Aplica-se ao [!INCLUDE[ssSQL15](../includes/sssql15-md.md)] SP1 como parte da criação de uma CPSA (área de superfície de programação comum) em todas as edições.     

##  <a name="analysis-services"></a><a name="SSAS"></a> Analysis Services  
  
Para obter informações sobre os recursos do Analysis Services compatíveis com as edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [Recursos do Analysis Services compatíveis com as edições do SQL Server](/analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016). 
  
##  <a name="bi-semantic-model-multi-dimensional"></a><a name="BIMD"></a> BI Semantic Model (Multi Dimensional)  
  
Para obter informações sobre os recursos do Analysis Services compatíveis com as edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [Recursos do Analysis Services compatíveis com as edições do SQL Server](/analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016).
   
##  <a name="bi-semantic-model-tabular"></a><a name="BIT"></a> BI Semantic Model (Tabular)  
  
Para obter informações sobre os recursos do Analysis Services compatíveis com as edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [Recursos do Analysis Services compatíveis com as edições do SQL Server](/analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016).
  
##  <a name="power-pivot-for-sharepoint"></a><a name="PPSP"></a> Power Pivot for SharePoint  
  
Para obter mais informações sobre os recursos do Power Pivot para SharePoint compatíveis com as edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [Recursos do Analysis Services compatíveis com as edições do SQL Server](/analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016).
  
##  <a name="data-mining"></a><a name="DM"></a> Data Mining  
  
Para obter mais informações sobre os recursos de Mineração de dados compatíveis com as edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [Recursos do Analysis Services compatíveis com as edições do SQL Server](/analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016).
  
##  <a name="reporting-services"></a><a name="SSRS"></a> Reporting Services  
  
Para obter mais informações sobre os recursos do Reporting Services compatíveis com as edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [Recursos do Reporting Services compatíveis com as edições do SQL Server](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).

##  <a name="business-intelligence-clients"></a><a name="BIC"></a> Clientes de Business Intelligence  

Para obter informações sobre os recursos do Business Intelligence Client compatíveis com as edições do [!INCLUDE[ssNoVersion_md](../includes/ssnoversion-md.md)], consulte [Recursos do Analysis Services compatíveis com as edições do SQL Server](/analysis-services/analysis-services-features-supported-by-the-editions-of-sql-server-2016) ou [Recursos do Reporting Services compatíveis com as edições do SQL Server](../reporting-services/reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).
  
##  <a name="spatial-and-location-services"></a><a name="SLS"></a> Spatial and Location Services  
  
|Nome do recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|  
|------------------|----------------|--------------|---------|------------------------------------|------------------------|
|Índices espaciais|Sim|Sim|Sim|Sim|Sim|   
|Tipos de dados planares e geodésicos|Sim|Sim|Sim|Sim|Sim| 
|Bibliotecas espaciais avançadas|Sim|Sim|Sim|Sim|Sim|   
|Importação/exportação de formatos de dados espaciais padrão da indústria|Sim|Sim|Sim|Sim|Sim|   
  
##  <a name="additional-database-services"></a><a name="ADS"></a> Additional Database Services  
  
|Nome do recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------| 
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Assistente de Migração|Sim|Sim|Sim|Sim|Sim|   
|Database Mail|Sim|Sim|Sim|Não|Não| 
  
##  <a name="other-components"></a><a name="Other"></a> Other Components  
  
|Nome do recurso|Enterprise|Standard|Web|Express with Advanced Services|Express|   
|------------------|----------------|--------------|---------|------------------------------------|------------------------|  
|StreamInsight|StreamInsight Premium Edition|StreamInsight Standard Edition|StreamInsight Standard Edition|Não|Não| 
|StreamInsight HA|StreamInsight Premium Edition|Não|Não|Não|Não|   
  
> [![Baixar o SSMS](https://docs.microsoft.com/analysis-services/analysis-services/media/download.png)](../ssms/download-sql-server-management-studio-ssms.md) **[Baixar a versão mais recente do SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)**      
  
## <a name="see-also"></a>Consulte Também  
 [Instalar o SQL Server](../database-engine/install-windows/install-sql-server.md)  
 
  
