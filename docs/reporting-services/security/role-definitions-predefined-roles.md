---
title: Definições de função – funções predefinidas | Microsoft Docs
ms.date: 06/10/2020
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- security [Reporting Services], defaults
- default security
- role-based security [Reporting Services], defaults
ms.assetid: 6b46db51-7c30-467d-a251-50f50647fe21
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7c792804d9e7daae9209bcbafb8bae95fffb3492
ms.sourcegitcommit: c8e45e0fdab8ea2ae1c7e709346354576b18ca1e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/11/2020
ms.locfileid: "84716733"
---
# <a name="role-definitions---predefined-roles"></a>Definições de função – funções predefinidas
[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é instalado com funções predefinidas que você pode usar para conceder acesso a operações de servidor de relatório. Cada função predefinida descreve uma coleção de tarefas relacionadas. Você pode atribuir grupos e contas do usuário a funções predefinidas para fornecer acesso imediato a operações de servidor de relatório.  
  
## <a name="how-to-use-predefined-roles"></a>Como usar funções predefinidas  
  
1. Examine as funções predefinidas para determinar se você pode usá-las no estado em que se encontram. Se for necessário ajustar as tarefas ou definir funções adicionais, faça isso antes de começar a atribuir usuários a funções específicas. Para criar ou editar funções personalizadas, use o SQL Server Management Studio. Para obter mais informações, consulte [Criar, excluir ou modificar uma função &#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md).
  
2. Identifique quais usuários e grupos requerem acesso ao servidor de relatório, e em que nível. A maioria dos usuários deve ser atribuída à função **Navegador** ou à função **Construtor de Relatórios** . Um número menor de usuários deve ser atribuído à função **Publicador** . Pouquíssimos usuários devem receber a função **Gerenciador de Conteúdo**.  

3. Quando você estiver pronto para atribuir contas de usuário e grupo a funções específicas, use o portal da Web. Para obter mais informações, confira [Conceder acesso ao usuário a um servidor de relatório](../../reporting-services/security/grant-user-access-to-a-report-server.md).  
  
##  <a name="predefined-role-definitions"></a><a name="bkmk_rolelist"></a> Definições de funções predefinidas  
 As funções predefinidas são determinadas pelas tarefas às quais oferecem suporte. Você pode modificar essas funções ou substituí-las por funções personalizadas.  
  
 *Escopo* define os limites dentro dos quais as funções são usadas. As funções de nível de item fornecem níveis variados de acesso aos itens do servidor de relatório e às operações que afetam esses itens. Essas funções são definidas no nó raiz (Base) e em todos os itens na hierarquia de pastas do servidor de relatório. As funções de nível de sistema autorizam o acesso ao nível do site. As funções de nível de item e de sistema são mutuamente exclusivas, mas são utilizadas em conjunto para fornecer permissões abrangentes ao conteúdo e às operações do servidor de relatório.  
  
 A tabela a seguir descreve o escopo predefinido das funções:  
  
|Função predefinida|Escopo|DESCRIÇÃO|  
|---------------------|-----------|-----------------|  
|[Função Gerenciador de Conteúdo](#bkmk_content)|Item|Pode gerenciar o conteúdo no Servidor de relatório. Isso inclui pastas, relatórios e recursos.|  
|[Função Publicador](#bkmk_publisher)|Item|Pode publicar relatórios e relatórios vinculados ao Servidor de relatório.|  
|[Função Navegador](#bkmk_browser)|Item|Pode exibir pastas, relatórios e assinar relatórios.|  
|[Função Construtor de Relatórios](#bkmk_reportbuilder)|Item|Pode exibir as definições de relatório.|  
|[Função Meus Relatórios](#bkmk_myreports)|Item|Pode publicar relatórios e relatórios vinculados; gerenciar pastas, relatórios e recursos em uma pasta Meus Relatórios dos usuários.|  
|[Função Administrador do Sistema](#bkmk_systemadministrator)|Sistema|Exibe e modifica as atribuições de função do sistema, as definições de função do sistema, as propriedades do sistema e as agendas compartilhadas, além de criar definições de função e gerenciar trabalhos no Management Studio.|  
|[Função Usuário do Sistema](#bkmk_systemuser)|Sistema|Exibe as propriedades do sistema, agendas compartilhadas e permitir o uso do Construtor de Relatórios ou outros clientes que executam definições de relatório.|  
  
##  <a name="content-manager-role"></a><a name="bkmk_content"></a> Função do gerenciador de conteúdo  
 A função **Gerenciador de Conteúdo** é uma função predefinida que inclui tarefas úteis para um usuário que gerencia relatórios e conteúdo Web, mas não é necessariamente autor de relatórios ou gerencia um servidor Web ou instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um gerenciador de conteúdo implanta relatórios, gerencia modelos de relatório e conexões de fontes de dados, além de tomar decisões sobre como os relatórios devem ser usados. Todas as tarefas do nível de item são selecionadas por padrão para a definição da função **Gerenciador de Conteúdo** .  
  
 A função **Gerenciador de Conteúdo** é frequentemente usada com a função **Administrador do Sistema** . Juntas, as duas definições de função fornecem um conjunto completo de tarefas a usuários que solicitam acesso total a todos os itens em um servidor de relatório. Apesar de a função **Gerenciador de Conteúdo** dar acesso completo a relatórios, modelos de relatórios, pastas, entre outros itens dentro da hierarquia de pastas, ela não fornece acesso a itens ou operações no nível do site. Tarefas como a criação e gerenciamento de agendas compartilhadas, configuração das propriedades do servidor e gerenciamento de definições de função são tarefas no nível do sistema incluídas na função **Administrador do Sistema** . Por esse motivo, recomendamos que você crie uma segunda atribuição de função no nível do site que forneça acesso a agendas compartilhadas.  
  
### <a name="content-manager-tasks"></a>Tarefas do gerenciador de conteúdo  
 A tabela a seguir relaciona as tarefas incluídas na função **Gerenciador de Conteúdo**:  
  
|Tarefa|DESCRIÇÃO|  
|----------|-----------------|  
|Relatórios de consumo|Lê definições de relatório.|  
|Criar relatórios vinculados|Criar relatórios vinculados com base em um relatório não vinculado.|  
|Gerenciar todas as assinaturas|Exibir, modificar e excluir qualquer assinatura para relatórios e relatórios vinculados, independentemente de quem for proprietário da assinatura. Essa tarefa dá suporte à criação de assinaturas controladas por dados. Ela também dá suporte à edição e execução da [atualização agendada para arquivos do Power BI (.pbix) no Servidor de Relatórios do Power BI](https://docs.microsoft.com/power-bi/report-server/configure-scheduled-refresh).|  
|Gerenciar as fontes de dados|Criar e excluir itens de fontes de dados compartilhadas, exibir e modificar propriedades de fontes de dados e conteúdos.|  
|Gerenciar pastas|Criar, exibir e excluir pastas, e exibir e modificar propriedades de pasta.|  
|Gerenciar modelos|Criar, exibir e excluir modelos e exibir e modificar propriedades de modelo.|  
|Administrar assinaturas individuais|Criar, exibir, modificar e excluir assinaturas de propriedade do usuário para relatórios e relatórios vinculados. Essa tarefa também dá suporte à edição e execução da [atualização agendada para arquivos do Power BI (.pbix) no Servidor de Relatórios do Power BI](https://docs.microsoft.com/power-bi/report-server/configure-scheduled-refresh).|  
|Gerenciar histórico de relatório|Criar, exibir e excluir histórico de relatório, exibir propriedades do histórico de relatório, e exibir e modificar configurações que determinam limites para o número de instantâneos e o funcionamento do cache.|  
|Gerenciar relatórios|Adicionar e excluir relatórios, modificar parâmetros de relatório, exibir e modificar propriedades de relatório, exibir e modificar fontes de dados que fornecem o conteúdo para o relatório, exibir e modificar definições de relatório e definir diretrizes de segurança no nível do relatório.|  
|Gerenciar recursos|Criar, modificar e excluir recursos, e exibir e modificar propriedades de recurso.|  
|Definir políticas de segurança para itens|Definir políticas de segurança para relatórios, relatórios vinculados, pastas, recursos e fontes de dados. Para obter mais informações, consulte [Itens protegíveis](../../reporting-services/security/securable-items.md).|  
|Exibir fontes de dados|Exibir itens de fontes de dados compartilhadas na hierarquia de pastas.|  
|Exibir relatórios|Executar relatórios e exibir propriedades de relatório.|  
|Exibir modelos|Exibir modelos na hierarquia de pastas, usar modelos como fontes de dados para um relatório e executar consultas no modelo para recuperar dados.|  
|Exibir recursos|Exibir recursos e propriedades de recurso.|  
|Exibir pastas|Exibir conteúdos de pasta e navegar pela hierarquia de pastas.|  
  
### <a name="customizing-the-content-manager-role"></a>Como personalizar a função gerenciador de conteúdo  
 Essa função foi planejada para usuários de confiança responsáveis por gerenciar e fazer a manutenção de conteúdo de servidor de relatório. Você pode remover tarefas dessa definição, mas isso pode introduzir ambiguidade no que pode ser gerenciado. Por exemplo, remover a tarefa "Exibir relatórios" da definição da função impede que **Gerenciador de Conteúdo** exiba conteúdos de relatório e, portanto, não possa verificar alterações nas configurações de credencial e parâmetro.  
  
 A função **Gerenciador de Conteúdo** é usada em segurança padrão.  
  
##  <a name="publisher-role"></a><a name="bkmk_publisher"></a> Função publicador  
 A função **Publicador** é uma definição de função interna que inclui tarefas que permitem que os usuários adicionem conteúdo a um servidor de relatório. Para facilitar, essa função é predefinida. Ela não é usada até que você crie atribuições de função que a incluam. Essa função foi desenvolvida para os usuários que criam relatórios ou modelos no Designer de Relatórios ou no Designer de Modelo e, em seguida, publicam esses itens em um servidor de relatório.  
  
> [!CAUTION]  
> A permissão para publicar itens em um servidor de relatório deve ser concedida somente para usuários confiáveis. A função Publisher concede permissões abrangentes que permitem aos usuários transferir qualquer tipo de arquivo para um servidor de relatório. Se um relatório ou arquivo HTML carregado contiver algum script suspeito, qualquer usuário que clicar no relatório ou documento HTML executará o script com suas credenciais.  
  
 As definições de relatório podem incluir scripts e outros elementos que são vulneráveis a ataques de injeção HTML quando o relatório é renderizado em HTML no tempo de execução. Se um relatório publicado contiver algum script suspeito, qualquer usuário que executar esse relatório provocará acidentalmente a execução do script quando o relatório for aberto. Se o usuário tiver permissões concedidas, o script será executado com essas permissões.  
  
 Para reduzir o risco de execução acidental de scripts suspeitos, limite o número de usuários que têm permissão para publicar conteúdo e verifique se os usuários só publicam documentos e relatórios provenientes de origens confiáveis. Se você não souber ao certo se é seguro publicar uma definição de relatório, abra o arquivo .rdl em um editor de texto e procure marcas de script. Os scripts suspeitos podem estar ocultos em expressões e URLs (por exemplo, uma URL em uma ação de navegação).  
  
### <a name="publisher-tasks"></a>Tarefas do publicador  
 A tabela a seguir relaciona as tarefas incluídas na função **Publicador**:  
  
|Tarefa|Descrição|  
|----------|-----------------|  
|Criar relatórios vinculados|Criar relatórios vinculados e publicá-los em uma pasta do servidor de relatório.|  
|Gerenciar as fontes de dados|Criar e excluir itens de fontes de dados compartilhadas, exibir e modificar propriedades de fontes de dados e conteúdos.|  
|Gerenciar pastas|Criar, exibir e excluir pastas; exibir e modificar propriedades de pasta.|  
|Gerenciar relatórios|Adicione e exclua relatórios, modifique parâmetros de relatório, exiba e modifique propriedades de relatório, exiba e modifique fontes de dados que fornecem conteúdo ao relatório, exiba e modifique definições de relatório.|  
|Gerenciar modelos|Criar, exibir e excluir modelos de relatório; exibir e modificar propriedades de modelo de relatório.|  
|Gerenciar recursos|Criar, modificar e excluir recursos; exibir e modificar propriedades de recurso.|  
  
### <a name="customizing-the-publisher-role"></a>Como personalizar a função publicador  
 Você pode modificar a função **Publicador** de acordo com suas necessidades. Por exemplo, é possível remover a tarefa “Criar relatórios vinculados” se você não desejar que os usuários criem e publiquem relatórios vinculados ou adicionar a tarefa “Exibir pastas” para que os usuários possam navegar pela hierarquia de pastas ao selecionar um local para um novo item.  
  
 No mínimo, os usuários que publicam relatórios a partir do Designer de Relatórios precisam da tarefa “Gerenciar relatórios” para adicionar um relatório ao servidor de relatório. Se o usuário precisar publicar relatórios que usam fontes de dados compartilhadas ou arquivos externos, inclua também “Gerenciar fontes de dados” e “Gerenciar recursos”. Caso o usuário também precise criar uma pasta como parte do processo de publicação, inclua “Gerenciar pastas”.  
  
##  <a name="browser-role"></a><a name="bkmk_browser"></a> Função navegador  
 A função **Navegador** é uma função predefinida que inclui tarefas úteis para o usuário que gerencia relatórios, mas não é necessariamente o autor de relatórios, nem os gerencia. Essa função fornece recursos básicos para o uso convencional de um servidor de relatório. Sem essas tarefas, pode ser difícil para usuários usarem um servidor de relatório.  
  
 A função **Navegador** deve ser usada com a função **Usuário do Sistema** . Juntas, as duas definições de função fornecem um conjunto completo de tarefas para usuários que interagem com itens em um servidor de relatório. Apesar de a função **Navegador** fornecer acesso de exibição a relatórios, modelos de relatórios, pastas, entre outros itens dentro da hierarquia de pastas, ela não fornece acesso a itens ou operações de site, como agendas compartilhadas, úteis para a criação de assinaturas, por exemplo. Por esse motivo, recomendamos que você crie uma segunda atribuição de função no nível do site que forneça acesso a agendas compartilhadas.  
  
### <a name="browser-tasks"></a>Tarefas do navegador  
 A tabela a seguir relaciona as tarefas incluídas na função **Navegador**:  
  
|Tarefa|Descrição|  
|----------|-----------------|  
|Exibir relatórios|Executar um relatório e exibir as propriedades do relatório.|  
|Exibir recursos|Exibir recursos e propriedades de recurso.|  
|Exibir pastas|Exibir conteúdos de pasta e navegar pela hierarquia de pastas.|  
|Exibir modelos|Exibir modelos na hierarquia de pastas, usar modelos como fontes de dados para um relatório e executar consultas no modelo para recuperar dados.|  
|Administrar assinaturas individuais|Criar, exibir, modificar e excluir assinaturas de propriedade do usuário para relatórios e relatórios vinculados, e criar agendas como suporte a essas assinaturas.|  
  
### <a name="customizing-the-browser-role"></a>Como personalizar a função navegador  
 É possível modificar a função **Navegador** de acordo com as suas necessidades. Por exemplo, é possível remover a tarefa "Gerenciar assinaturas individuais" se não desejar oferecer suporte a assinaturas, ou remover a tarefa "Exibir recursos" se não quiser que os usuários vejam documentação colateral ou outros itens que podem ser carregados no servidor de relatório.  
  
 Como mínimo, essa função deve ser compatível com ambas as tarefas "Exibir relatórios" e "Exibir pastas" para oferecer suporte à exibição e navegação em pastas. Você remova a tarefa "Exibir pastas", exceto se desejar eliminar a navegação de pasta. Igualmente, você remova a tarefa "Exibir relatórios", a menos que queira impedir que os usuários visualizem relatórios. Esses tipos de modificação sugerem a necessidade de uma definição de função personalizada aplicada de forma seletiva em um grupo específico de usuários.  
  
##  <a name="report-builder-role"></a><a name="bkmk_reportbuilder"></a> Função Construtor de Relatórios  
 A função **Construtor de Relatórios** é uma função predefinida que inclui tarefas para carregar relatórios no Construtor de Relatórios, bem como exibir e navegar na hierarquia de pasta. Para criar e modificar relatórios no Construtor de Relatórios, você também deve ter uma atribuição de função de sistema que inclua a tarefa “Executar definições de relatório”, necessária para processar relatórios localmente no Construtor de Relatórios.  
  
### <a name="report-builder-tasks"></a>Tarefas do Construtor de Relatórios  
 A tabela a seguir relaciona as tarefas incluídas na função **Construtor de Relatórios**:  
  
|Tarefa|Descrição|  
|----------|-----------------|  
|Relatórios de consumo|Lê definições de relatório.|  
|Exibir relatórios|Executar um relatório e exibir as propriedades do relatório.|  
|Exibir recursos|Exibir recursos e propriedades de recurso.|  
|Exibir pastas|Exibir conteúdos de pasta e navegar pela hierarquia de pastas.|  
|Exibir modelos|Exibir modelos na hierarquia de pastas, usar modelos como fontes de dados para um relatório e executar consultas no modelo para recuperar dados.|  
|Administrar assinaturas individuais|Criar, exibir, modificar e excluir assinaturas de propriedade do usuário para relatórios e relatórios vinculados, e criar agendas como suporte a essas assinaturas.|  
  
### <a name="customizing-the-report-builder-role"></a>Como personalizar a função Construtor de Relatórios  
 Você pode modificar a função **Construtor de Relatórios** para atender às suas necessidades. As recomendações geralmente são as mesmas da função **Navegador** : remova a função “Gerenciar assinaturas individuais” se não desejar oferecer suporte a assinaturas, remova a tarefa “Exibir recursos” se não desejar que os usuários vejam os recursos e mantenha as tarefas “Exibir relatórios” e “Exibir pastas” para oferecer suporte à exibição e navegação de pastas.  
  
 A tarefa mais importante desta definição de função é “Consumir relatórios”, que permite ao usuário carregar uma definição de relatório do servidor de relatório em uma instância local do Construtor de Relatórios. Se não desejar oferecer suporte a essa tarefa, exclua esta definição de função e use a função **Navegador** para oferecer suporte ao acesso geral a um servidor de relatório.  
  
##  <a name="my-reports-role"></a><a name="bkmk_myreports"></a> Função Meus Relatórios  
 A função **Meus Relatórios** é uma função predefinida que inclui um conjunto de tarefas que são úteis para os usuários do recurso Meus Relatórios. Esta definição de função inclui tarefas que concedem permissões administrativas a usuários na pasta Meus Relatórios que eles possuem.  
  
 Embora seja possível escolher outra função para usar com o recurso Meus Relatórios, é recomendado escolher a função usada exclusivamente para a segurança de Meus Relatórios. Para obter mais informações, consulte [Proteger Meus Relatórios](../../reporting-services/security/secure-my-reports.md).  
                          
### <a name="my-reports-tasks"></a>Tarefas de Meus Relatórios  
 A tabela a seguir relaciona as tarefas incluídas na função **Meus Relatórios**:  
  
|Tarefa|Descrição|  
|----------|-----------------|  
|Criar relatórios vinculados|Criar relatórios vinculados que são baseados em relatórios armazenados na pasta Meus Relatórios do usuário.|  
|Gerenciar pastas|Criar, exibir e excluir pastas, e exibir e modificar propriedades de pasta.|  
|Gerenciar as fontes de dados|Criar e excluir itens de fontes de dados compartilhadas, exibir e modificar propriedades de fontes de dados e conteúdos.|  
|Administrar assinaturas individuais|Criar, exibir, modificar e excluir assinaturas para relatórios e relatórios vinculados.|  
|Gerenciar relatórios|Adicionar e excluir relatórios, modificar parâmetros de relatório, exibir e modificar propriedades de relatório, exibir e modificar fontes de dados que fornecem o conteúdo para o relatório, exibir e modificar definições de relatório e definir diretrizes de segurança no nível do relatório.|  
|Gerenciar recursos|Criar, modificar e excluir recursos e o modo de exibição. e modificar propriedades de recurso.|  
|Exibir relatórios|Executar os relatórios armazenados na pasta Meus Relatórios do usuário e exibir propriedades de relatório.|  
|Exibir fontes de dados|Exibir itens de fontes de dados compartilhadas na hierarquia de pastas.|  
|Exibir recursos|Exibir recursos e propriedades de recurso.|  
|Exibir pastas|Exibir o conteúdo da pasta.|  
  
### <a name="customizing-the-my-reports-role"></a>Como personalizar a função Meus Relatórios  
 Você pode modificar esta função conforme suas necessidades. No entanto, é recomendado manter as tarefas “Gerenciar relatórios” e “Gerenciar pastas” para habilitar o gerenciamento básico do conteúdo. Além disso, essa função deve oferecer suporte a todas as tarefas baseadas em exibição para que os usuários possam ver o conteúdo da pasta e executar os relatórios que gerenciam.  
  
 Embora a tarefa “Definir políticas de segurança para itens” não faça parte da definição de função por padrão, você pode adicionar essa tarefa à função **Meus Relatórios** para que os usuários possam personalizar as configurações de segurança para subpastas e relatórios.  
  
##  <a name="system-administrator-role"></a><a name="bkmk_systemadministrator"></a> Função administrador do sistema  
 A função **Administrador do Sistema** é uma função predefinida que inclui tarefas úteis para um administrador de servidor de relatório que tem a responsabilidade geral por um servidor de relatório, mas não necessariamente por seu conteúdo.  
  
 Para criar uma atribuição de função que inclui essa função, use a página Configurações do Site do portal da Web ou use os comandos acionados com o clique com o botão direito do mouse no nó do servidor de relatórios no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 A função **Administrador do Sistema** não concede o mesmo intervalo total de permissões que um administrador local poderia ter em um computador. Em vez disso, a função **Administrador do Sistema** inclui operações que são executadas no nível de site, e não no nível de item. Para os usuários que requerem acesso às operações do site inteiro e aos itens armazenados no servidor de relatório, crie uma segunda atribuição de função na pasta Base que inclui a função **Gerenciador de Conteúdo** . Juntas, as duas definições de função fornecem um conjunto completo de tarefas a usuários que solicitam acesso total a todos os itens em um servidor de relatório.  
  
### <a name="system-administrator-tasks"></a>Tarefas de administrador do sistema  
 A tabela a seguir lista as tarefas que são incluídas na função **Administrador do Sistema**:  
  
|Tarefa|Descrição|  
|----------|-----------------|  
|Executar definições de relatório|Iniciar a execução da definição de relatório sem publicá-la em um servidor de relatório.|  
|Gerenciar trabalhos|Exibir e cancelar trabalhos que estão em execução. Para obter mais informações, consulte [Gerenciar um processo em execução](../../reporting-services/subscriptions/manage-a-running-process.md).|  
|Gerenciar propriedades de servidor de relatório|Exibir e modificar propriedades que se aplicam ao servidor de relatório e a itens gerenciados pelo servidor de relatório.<br /><br /> Esta tarefa oferece suporte para a renomeação do portal da Web, a habilitação de Meus Relatórios e a configuração de padrões de históricos de relatórios.|  
|Gerenciar funções|Criar, exibir, modificar e excluir definições de função.<br /><br /> Os membros da função **Administrador do Sistema** podem usar a página Configurações de Site para gerenciar funções.|  
|Gerenciar agendas compartilhadas|Criar, exibir, modificar e excluir agendas compartilhadas que são usadas para executar ou atualizar relatórios.|  
|Gerenciar segurança de servidor de relatório|Exibir e modificar atribuições de função do sistema inteiro|  
  
 A função **Administrador do Sistema** é usada na segurança padrão.  
  
##  <a name="system-user-role"></a><a name="bkmk_systemuser"></a> Função usuário do sistema  
A função **Usuário do Sistema** é uma função predefinida que inclui tarefas que permitem aos usuários visualizar informações básicas sobre o servidor de relatório. Também inclui suporte para carregar um relatório em Construtor de Relatórios. O Construtor de Relatórios é um aplicativo cliente que pode processar um relatório de maneira independente de um servidor de relatório. A tarefa "Executar Definições de Relatórios" é planejada para ser usada com o Construtor de Relatórios. Se você não estiver usando o Construtor de Relatórios, poderá remover essa tarefa da função **Usuário do Sistema** .  

A tabela a seguir lista as tarefas incluídas na definição da função **Usuário do Sistema**:  
  
### <a name="system-user-tasks"></a>Tarefas do usuário do sistema  
  
|Tarefa|Descrição|  
|----------|-----------------|  
|Executar definições de relatório|Execute um relatório sem publicá-lo em um servidor de relatório.|  
|Exibir propriedades do servidor de relatório|Exiba as propriedades aplicáveis ao servidor de relatório, como o nome do aplicativo, se a configuração Meus Relatórios está habilitada e os padrões de histórico do relatório.<br /><br /> Se você remover essa tarefa da função **Usuário do Sistema** , a página Configurações de Site não estará disponível. Além disso, o título do aplicativo não é exibido na parte superior de cada página. Por padrão, o título do portal da Web é "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]".|  
|Exibir agendas compartilhadas|Exiba os agendamentos compartilhados usados para executar relatórios ou atualizar um.<br /><br /> Se você remover essa tarefa da função **Usuário do Sistema** , os usuários não poderão selecionar os agendamentos compartilhados a serem usados com assinaturas e outras opções agendadas.|  
  
 A função **Usuário do Sistema** pode ser usada para complementar a segurança padrão. Você pode incluir a função em novas atribuições de função que ampliam o acesso do servidor de relatório aos usuários de relatórios. Para obter mais informações, consulte [Concedendo permissões em um servidor de relatório no modo nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md).  
  
## <a name="see-also"></a>Confira também  
[Criar, excluir ou modificar uma função &#40;Management Studio&#41;](../../reporting-services/security/role-definitions-create-delete-or-modify.md)  
[Conceder acesso ao usuário a um servidor de relatório](../../reporting-services/security/grant-user-access-to-a-report-server.md)  
[Modificar ou excluir uma atribuição de função &#40; do portal da Web do SSRS&#41;](../../reporting-services/security/role-assignments-modify-or-delete.md)  
[Conceder permissões em um servidor de relatório no Modo Nativo](../../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md)  
[Tarefas e permissões](../../reporting-services/security/tasks-and-permissions.md)
  
