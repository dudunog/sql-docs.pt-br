---
title: Assistente para Gerar e Publicar Scripts
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.generatescriptswizard.setscriptingoptions.f1
- sql9.swb.generatescriptswizard.scriptwizarddescription.f1
- sql12.swb.generatescriptswizard.saveorpublishscripts.f1
- sql9.swb.generatescriptswizard.selectdatabase.f1
- sql9.swb.generatescriptswizard.scriptfileoption.f1
- sql12.swb.generatescriptswizard.advancedscriptingoptions.f1
- sql9.swb.generatescriptswizard.choosescriptoptions.f1
- sql12.swb.generatescriptswizard.summarypage.f1
- sql9.swb.generatescriptswizard.chooseviews.f1
- sql12.swb.generatescriptswizard.providerconfiguration.f1
- sql9.swb.generatescriptswizard.choosestoredprocedures.f1
- sql9.swb.generatescriptswizard.chooseobjecttypes.f1
- sql9.swb.generatescriptswizard.welcome.f1
- sql9.swb.generatescriptswizard.chooseudf.f1
- sql12.swb.generatescriptswizard.manageproviders.f1
- sql9.swb.generatescriptswizard.chooseuddt.f1
- sql12.swb.generatescriptswizard.advancedpublishingoptions.f1
- sql12.swb.generatescriptswizard.introduction.f1
- sql9.swb.generatescriptswizard.chooserules.f1
- sql12.swb.generatescriptswizard.chooseobjects.f1
- sql9.swb.generatescriptswizard.progress.f1
- sql9.swb.generatescriptswizard.choosedefaults.f1
- sql9.swb.generatescriptswizard.chooseobjects.f1
- sql9.swb.generatescriptswizard.choosetables.f1
helpviewer_keywords:
- databases [SQL Server], publishing
- publishing databases
- scripts [SQL Server], generating
- scripts [SQL Server], publishing
- databases [SQL Server], generating scripts
- Publish Database Wizard
ms.assetid: 5ee520ba-ec7e-4199-a441-189e9e264b37
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47bf324dd757661a6f49f18b28f810c87ca1419e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "75242105"
---
# <a name="generate-and-publish-scripts-wizard"></a>Assistente para Gerar e Publicar Scripts
  Você pode usar **Assistente para Gerar e Publicar Scripts** para criar scripts para transferir um banco de dados entre instâncias do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] ou do [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. É possível gerar scripts para um banco de dados em uma instância do Mecanismo de Banco de Dados em sua rede local ou no [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Os scripts gerados podem ser executados em outra instância do Mecanismo de Banco de Dados ou no [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. É possível usar o assistente para publicar o conteúdo de um banco de dados diretamente em um serviço Web criado usando os Serviços de Publicação de Banco de dados. É possível criar scripts para um banco de dados inteiro ou limitá-lo a objetos específicos.  
  
1.  **Antes de iniciar:**  [Publicando em um serviço hospedado](#PubHostSvc), [Permissões](#Permissions)  
  
2.  **Para gerar ou publicar um script, usando:**  [Assistente para Gerar e Publicar Scripts](#GenPubScriptWiz)  
  
## <a name="before-you-begin"></a>Antes de começar  
 Os bancos de dados de origem e destino podem estar no [!INCLUDE[ssSDS](../../includes/sssds-md.md)], ou em uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] que esteja executando o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou posterior.  
  
###  <a name="publishing-to-a-hosted-service"></a><a name="PubHostSvc"></a> Publicando em um serviço hospedado  
 Além de criar scripts, você pode usar o **Assistente para Gerar e Publicar Scripts** para criar scripts para publicar um banco de dados em um tipo específico de serviço Web hospedado do SQL Server. O Conjunto de Ferramentas de Hospedagem do SQL Server fornece Serviços de Publicação de Banco de dados como um projeto de origem compartilhado no CodePlex. O projeto dos Serviços de Publicação de Banco de dados pode ser usado por provedores de hospedagem na Web para criar um conjunto de serviços Web que facilitam a implantação de banco de dados no serviço Web para clientes. Para obter mais informações sobre como baixar o Conjunto de Ferramentas de Hospedagem do SQL Server, consulte [SQL Server Database Publishing Services](https://go.microsoft.com/fwlink/?LinkId=142025)(em inglês).  
  
 Para publicar um banco de dados em um serviço de hospedagem Web, selecione a opção **Publicar no Serviço Web** na página **Definir Opções de Script** do assistente.  
  
###  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 A permissão mínima para publicar um banco de dados é a associação à função de banco de dados fixa db_ddladmin no banco de dados de origem. A permissão mínima para publicar um script de banco de dados para uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no provedor de hospedagem é a participação na função de banco de dados fixa db_ddladmin no banco de dados de destino.  
  
 O usuário também tem que fornecer um nome e uma senha do usuário para acessar a conta do provedor de hospedagem para publicação com o assistente. O banco de dados de destino deve ser criado no provedor de hospedagem antes da publicação do banco de dados de origem. A publicação substitui objetos naquele banco de dados existente.  
  
##  <a name="using-the-generate-and-publish-scripts-wizard"></a><a name="GenPubScriptWiz"></a> Usando o Assistente para Gerar e Publicar Scripts  
 **Para gerar e publicar um script**  
  
1.  No **Pesquisador de Objetos**, expanda o nó da instância que contém o banco de dados a ser incluído no script.  
  
2.  Aponte para **Tarefas**e clique em **Gerar Scripts**.  
  
3.  Conclua as etapas das caixas de diálogo do assistente:  
  
    -   [Página de Introdução](#Introduction)  
  
    -   [Página Escolher Objetos](#ChooseObjects)  
  
    -   [Página Definir Opções de Script](#SetScriptOpt)  
  
    -   [Página Opções de Script Avançadas](#AdvScriptOpt)  
  
    -   [Página Gerenciar Provedores](#MgProviders)  
  
    -   [Página Opções de Publicação Avançadas](#AdvPubOpts)  
  
    -   [Página Configuração do Provedor](#ProvConfig)  
  
    -   [Página de Resumo](#Summary)  
  
    -   [Página Salvar ou Publicar Scripts](#SavePubScripts)  
  
###  <a name="introduction-page"></a><a name="Introduction"></a> Página de Introdução  
 Esta página descreve as etapas para gerar ou publicar um script.  
  
 **Não mostrar esta página novamente** – Ignore esta página na próxima vez que iniciar o **Assistente para Gerar e Publicar Scripts**.  
  
 **Avançar >**: continua para a página **Escolher Método**.  
  
 **Cancelar** – Encerra o assistente sem gerar nem publicar um script do banco de dados.  
  
###  <a name="choose-objects-page"></a><a name="ChooseObjects"></a> Página Escolher Objetos  
 Use esta página para escolher quais objetos você deseja incluir nos scripts gerados por este assistente. Na página do assistente a seguir, você terá a opção de salvar esses scripts no local de sua escolha ou usá-los para publicar objetos de banco de dados em um provedor remoto de hospedagem Web que tenha instalados os [SQL Server Database Publishing Services](https://go.microsoft.com/fwlink/?LinkId=142025).  
  
 **Opção Gerar Script de Todo o Banco de Dados** – Clique para gerar scripts para todos os objetos do banco de dados e incluir um script para o próprio banco de dados.  
  
 **Selecionar objetos de banco de dados específicos** – Clique para limitar o assistente para gerar scripts somente para os objetos específicos no banco de dados escolhido:  
  
-   **Objetos de banco de dados** – Selecione, pelo menos, um objeto para incluir no script.  
  
-   **Selecionar Tudo** – Marca todas as caixas de seleção disponíveis.  
  
-   **Desmarcar Tudo** – Limpa todas as caixas de seleção. Para continuar, selecione pelo menos um objeto de banco de dados.  
  
###  <a name="set-scripting-options-page"></a><a name="SetScriptOpt"></a> Página Definir Opções de Script  
 Use esta página para especificar se você deseja que o assistente salve scripts no local de sua escolha ou use os scripts para publicar objetos de banco de dados em um provedor remoto de hospedagem Web. Para publicar, você precisa ter acesso a um serviço Web instalado usando os Serviços de Publicação de Banco de Dados.  
  
 **Opções** – Se desejar que o assistente salve scripts em um local de sua preferência, selecione **Salvar scripts em um local específico**. Você pode executar os scripts posteriormente em relação a uma instância do Mecanismo de Banco de Dados ou em relação ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Se você desejar que o assistente publique seus objetos de banco de dados em um provedor remoto de hospedagem Web, selecione **Publicar no serviço Web**.  
  
 **Salvar scripts em um local específico** – salve um ou mais. Arquivos de script Transact-SQL para um local especificado.  
  
-   **Avançado** – Exiba a caixa de diálogo **Opções de Script Avançadas** em que você pode selecionar opções avançadas para gerar scripts.  
  
-   **Salvar em arquivo** – Salve o script em um ou mais arquivos .sql. Clique no botão Procurar (**…**) para especificar um nome e uma localização para o arquivo. Marque a caixa de seleção **Substituir o arquivo existente** para substituir o arquivo se já existir outro com o mesmo nome. Clique em **Arquivo único** ou **Arquivo único por objeto** para especificar como os scripts devem ser gerados. Clique **Texto Unicode** ou **Texto ANSI** para especificar o tipo de texto que deve ser usado no script.  
  
-   **Salvar na Área de Transferência** – Salve o script Transact-SQL na área de transferência.  
  
-   **Salvar na nova janela de consulta** – Gere o script para uma janela do Editor de Consultas do Mecanismo de Banco de Dados. Se nenhuma janela de editor for aberta, uma nova janela de editor será aberta como o destino do script.  
  
 **Publicar em Serviço Web** – Publique os objetos selecionados em um serviço de host remoto Web para o qual você configurou um provedor.  
  
-   **Gerenciar Provedores** – Exiba a caixa de diálogo **Gerenciar Provedores** . Use a caixa de diálogo **Gerenciar Provedores** para adicionar, editar e excluir provedores de hospedagem. Cada provedor especifica informações de conexão com um serviço Web de hospedagem e os bancos de dados de destino naquele serviço.  
  
-   **Avançado** – Exiba a caixa de diálogo **Opções de Publicação Avançadas** em que você pode selecionar opções avançadas para publicar scripts.  
  
-   **Provedor** – Selecione o provedor que especifica as informações de conexão para o serviço de host Web que hospeda o banco de dados em que você deseja publicar os objetos selecionados. Você deve ter pelo menos um provedor na caixa de diálogo **Gerenciar Provedores** para selecionar um provedor.  
  
-   **Banco de dados de destino** – Selecione o banco de dados de destino em que você deseja publicar os objetos selecionados. Você deve selecionar um provedor antes de selecionar um banco de dados de destino.  
  
###  <a name="advanced-scripting-options-page"></a><a name="AdvScriptOpt"></a> Página Opções de Script Avançadas  
 Use essa página para especificar como você deseja que esse assistente gere scripts. Muitas opções diferentes estão disponíveis. As opções ficarão acinzentadas se não tiverem suporte da versão do SQL Server ou do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] especificado no **Tipo de mecanismo de banco de dados**.  
  
 **Opções** – Especifique opções avançadas selecionando um valor da lista de configurações disponíveis à direita de cada opção.  
  
 **Geral** – as opções a seguir se aplicam ao script inteiro.  
  
-   **Preenchimento ANSI** – inclui `ANSI PADDING ON` no script. O padrão é **True**.  
  
-   **Acrescentar ao arquivo** – Se for **True**, este script será adicionado à parte inferior de um script existente, especificado na página **Definir Opções de Script** . Se for **False**, o novo script substituirá um script anterior. O padrão é **False**.  
  
-   **Continuar o script se houver erro** – Quando for **True**, o script será interrompido quando ocorrer um erro. Se for **False**, o script continuará. O padrão é **False**.  
  
-   **Converter UDDTs em tipos de base** – Se for **True**, os UDDT (tipos de dados definidos pelo usuário) serão convertidos nos tipos de dados base subjacentes que foram usados para criá-los. Use **True** quando o UDDT não existir no banco de dados em que o script será executado. Se for **False**, serão usados UDDTs. O padrão é **False**.  
  
-   **Gerar script para objetos dependentes** – Gera um script para qualquer objeto que precise estar presente quando o script do objeto selecionado for executado. O padrão é **True**.  
  
-   **Incluir cabeçalhos descritivos** – Se for **True**, comentários descritivos serão adicionados ao script, separando-o em seções para cada objeto. O padrão é **False**.  
  
-   **Incluir se NOT EXISTS** – Se for **True**, o script incluirá uma instrução para verificar se o objeto já existe no banco de dados e não tentará criar um novo objeto se já existir um. O padrão é **False**.  
  
-   **Incluir nomes de restrição do sistema** -quando **for falso**, o valor padrão das restrições que foram nomeadas automaticamente no banco de dados de origem será automaticamente renomeado no banco de dados de destino. Se for **True**, as restrições terão o mesmo nome nos bancos de dados de origem e de destino.  
  
-   **Incluir instruções sem suporte** – Se for **False**, o script não conterá instruções para objetos sem suporte na versão de servidor selecionada ou no tipo de mecanismo. Se for **True**, o script conterá os objetos sem suporte. Cada instrução para um objeto sem suporte terá um comentário de que a instrução deve ser editada antes de o script ser executado em relação à versão do SQL Server selecionada ou ao tipo de mecanismo. O padrão é **False**.  
  
-   **Qualificar nomes de objetos do esquema** – Inclui o nome do esquema no nome de objetos que são criados. O padrão é **True**.  
  
-   **Associação de script** – Gera um script para associação padrão e objetos de regra. O padrão é **False**. Para obter mais informações, veja [CREATE DEFAULT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-default-transact-sql) e [CREATE RULE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-rule-transact-sql).  
  
-   **Ordenação de scripts** – Inclui informações de ordenação no script. O padrão é **False**. Para obter mais informações, consulte [Suporte a ordenações e a Unicode](../collations/collation-and-unicode-support.md).  
  
-   **Padrões de script** – Inclui objetos padrão usados para definir valores padrão em colunas de tabela. O padrão é **True**. Para obter mais informações, veja [CREATE DEFAULT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-default-transact-sql).  
  
-   **Script drop e create** – Se for **Script CREATE**, serão incluídas instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] para criar objetos. Se for o **Script DROP**, serão incluídas instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] para descartar objetos. Se for **Script DROP e CREATE**, a instrução drop [!INCLUDE[tsql](../../../includes/tsql-md.md)] será incluída no script, seguida da instrução create, para cada objeto de script. O padrão é **Script CREATE**.  
  
-   **Propriedades estendidas do script** – Inclui propriedades estendidas no script se o objeto tem propriedades estendidas. O padrão é **True**.  
  
-   **Script para tipo de mecanismo** – Cria um script que pode ser executado no tipo selecionado do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] ou em uma instância do Mecanismo de Banco de Dados do SQL Server. Objetos sem suporte no tipo especificado não são incluídos no script. O padrão é o tipo do servidor de origem.  
  
-   **Script para a versão do servidor** – Cria um script que pode ser executado na versão selecionada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Recursos que são novos em uma versão não podem ser incluídos em scripts executado por versões anteriores. O padrão é a versão do servidor de origem.  
  
-   **Logons de script** – Quando o objeto a ser gerado com scrip é um usuário de banco de dados, esta opção cria os logons dos quais o usuário depende. O padrão é **False**.  
  
-   **Gerar script de permissões em nível de objeto** – Inclui scripts para definir a permissão nos objetos no banco de dados. O padrão é **False**.  
  
-   **Estatísticas de script** – quando definido como **Estatísticas de script**, essa opção `CREATE STATISTICS` inclui a instrução para recriar estatísticas no objeto. A opção **Gerar script de estatísticas e histogramas** também cria informações de histograma. O padrão é **Não gerar script de estatísticas**. Para obter mais informações, veja [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
-   **Script use Database** -adiciona a `USE DATABASE` instrução ao script. Para ter certeza de que os objetos de banco de dados serão criados no banco de dados correto, inclua a instrução `USE DATABASE`. Quando espera-se que o script seja usado em um banco de dados **False** diferente, selecione false `USE DATABASE` para omitir a instrução. O padrão é **True**. Para obter mais informações, veja [USE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql).  
  
-   **Tipos de dados para o script** – Seleciona o que deve ser inserido no script: **Somente dados**, **Somente esquema** ou ambos. O padrão é **Esquema somente**.  
  
 **Opções de tabela/exibição** – As opções a seguir são válidas somente para scripts de tabelas ou exibições.  
  
-   **Controle de alterações de script** – Controle de alterações de scripts se for habilitado no banco de dados de origem ou nas tabelas no banco de dados de origem. O padrão é **False**. Para obter mais informações, veja [Sobre o controle de alterações &#40;SQL Server&#41;](../track-changes/about-change-tracking-sql-server.md).  
  
-   **Restrições de verificação** de script `CHECK` – adiciona restrições ao script. O padrão é **True**. Restrições `CHECK` exigem que os dados inseridos em uma tabela atendam algumas condições especificadas. Para obter mais informações, consulte [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md).  
  
-   **Opções de compactação de dados de script** – Gera scripts de opções de compactação de dados quando elas são configuradas no banco de dados de origem ou em tabelas no banco de dados de origem. Para saber mais, veja [Data Compression](../data-compression/data-compression.md). O padrão é **False**.  
  
-   **Chaves estrangeiras do script** – Adiciona chaves estrangeiras ao script. O padrão é **True**. Chaves estrangeiras indicam e impõem relações entre tabelas.  
  
-   **Índices de texto completo do script** – Gera script para a criação de índices de texto completo. O padrão é **False**.  
  
-   **Índices de script** – Gera script para a criação de índices nas tabelas. O padrão é **True**. Os índices ajudam você a localizar dados rapidamente.  
  
-   **Chaves primárias de script** – Gera script para a criação de chaves primárias em tabelas. O padrão é **True**. Chaves primárias identificam com exclusividade cada linha de uma tabela.  
  
-   **Gatilhos de script** – Gera script para a criação de gatilhos DML em tabelas. O padrão é **False**. Um gatilho DML é uma ação programada para executar quando um evento de linguagem de manipulação de dados (DML) ocorre no servidor de banco de dados. Para obter mais informações, consulte [DML Triggers](../triggers/dml-triggers.md).  
  
-   **Chaves exclusivas do script** – Gera script para a criação de chaves exclusivas em tabelas. Chaves exclusivas evitam a inserção de dados duplicados. O padrão é **True**. Para obter mais informações, consulte [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md).  
  
###  <a name="manage-providers-page"></a><a name="MgProviders"></a>Página gerenciar provedores  
 Use essa caixa de diálogo para exibir, adicionar, editar, excluir ou testar conexões de provedores de hospedagem. Um provedor de hospedagem especifica as informações de conexão para um serviço Web criado usando o projeto Database Publishing Services no SQL Server Hosting Toolkit, no CodePlex.  
  
 **Provedores configurados** – Lista o nome e o endereço do serviço **Web** de cada provedor de hospedagem que foi salvo.  
  
 **Novo** – Abre a caixa de diálogo **Configuração do provedor para novo provedor** para adicionar um novo provedor de hospedagem.  
  
 **Editar** – Abre a caixa de diálogo **Configuração do provedor** correspondente para editar um provedor de hospedagem existente.  
  
 **Excluir** – Exclui o provedor de hospedagem selecionado.  
  
 **Testar** – Testa a conexão com um serviço de hospedagem usando as informações do provedor selecionado.  
  
 **OK** – Salva todas as alterações feitas na caixa de diálogo **Provedor de Hospedagem** .  
  
 **Cancelar** – Desfaz todas as alterações feitas na caixa de diálogo **Provedor de Hospedagem** .  
  
###  <a name="advanced-publishing-options-page"></a><a name="AdvPubOpts"></a>Página opções de publicação avançadas  
 Use essa página para especificar como você deseja que esse assistente publique um banco de dados. Muitas opções diferentes estão disponíveis. As opções ficarão acinzentadas se não tiverem suporte da versão do SQL Server ou do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] especificado no **Tipo de mecanismo de banco de dados**.  
  
 **Opções** – Especifique opções avançadas selecionando um valor da lista de configurações disponíveis à direita de cada opção.  
  
 **Geral** – as opções a seguir se aplicam à publicação inteira.  
  
1.  **Converter UDDTs em tipos de base** – Se for **True**, os UDDT (tipos de dados definidos pelo usuário) serão convertidos nos tipos de dados base subjacentes que foram usados para criá-los. Use **True** quando o UDDT não existir no banco de dados em que o script será executado. Se for **False**, serão usados UDDTs. O padrão é **False**.  
  
2.  **Publicar ordenação** – Inclui informações de ordenação para colunas de tabela. O padrão é **False**. Para obter mais informações, consulte [Suporte a ordenações e a Unicode](../collations/collation-and-unicode-support.md).  
  
3.  **Publicar padrões** – Inclui objetos padrão usados para definir valores padrão em colunas de tabela. O padrão é **True**. Para obter mais informações, veja [CREATE DEFAULT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-default-transact-sql).  
  
4.  **Publicar objetos dependentes** – Publica qualquer objeto que precise estar presente quando o script do objeto selecionado for executado. O padrão é **True**.  
  
5.  **Publicar propriedades estendidas** – Inclui propriedades estendidas no script enviado ao provedor para publicação, caso o objeto tenha propriedades estendidas. O padrão é **True**.  
  
6.  **Publicar para versão do servidor** – Cria um script que é enviado ao provedor remoto para publicação de uma maneira que possa ser executado na versão selecionada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Recursos que são novos em uma versão não podem ser incluídos em scripts executado por versões anteriores. O padrão é a versão do servidor de origem.  
  
7.  **Publicar script de permissões em nível de objeto** – Inclui as permissão nos objetos selecionados no banco de dados. O padrão é **False**.  
  
8.  **Publicar estatísticas** – quando definido como **publicar estatísticas**, inclui a `CREATE STATISTICS` instrução para recriar estatísticas no objeto. A opção **Publicar estatísticas e histogramas** também cria informações de histograma. O padrão é **Não publicar estatísticas**. Para obter mais informações, veja [CREATE STATISTICS &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-statistics-transact-sql).  
  
9. **Publicar opções vardecimal** – habilita o `vardecimal` formato de tabela na tabela de banco de dados de destino quando ela está habilitada na tabela de banco de dados de origem. O padrão é **True**.  
  
10. **Qualificar nomes de objetos do esquema** – Inclui o nome do esquema no nome de objetos que são criados. O padrão é **True**.  
  
11. **Associação de script** – Inclui associação por padrão e objetos de regra no script enviados ao provedor para publicação. O padrão é **True**. Para obter mais informações, veja [CREATE DEFAULT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-default-transact-sql) e [CREATE RULE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-rule-transact-sql).  
  
12. **Tipos de dados para publicação** – Seleciona o que deve ser gerado com script: **Somente dados**, **Somente esquema**ou ambos. O padrão é **Esquema e Dados**.  
  
 **Publicando Opções** – especifica transações devem ser usadas ao publicar no provedor de host Web.  
  
1.  **Publicar usando transações** – Usa transações ao publicar em um provedor remoto de hospedagem na Web. Se o banco de dados de destino não puder concluir a publicação, as transações serão revertidas. O padrão é **True**.  
  
 **Opções de Tabela/Exibição** – As opções a seguir se aplicam somente a tabelas ou exibições.  
  
1.  **Publicar restrições check** – inclui a criação de `CHECK` restrições no processo de publicação. O padrão é **True**. Restrições `CHECK` exigem que os dados inseridos em uma tabela atendam algumas condições especificadas. Para obter mais informações, consulte [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md).  
  
2.  **Publicar chaves estrangeiras** – Inclui a criação de chaves estrangeiras no processo de publicação. O padrão é **True**. Chaves estrangeiras indicam e impõem relações entre tabelas. Para obter mais informações, consulte [Primary and Foreign Key Constraints](../tables/primary-and-foreign-key-constraints.md).  
  
3.  **Publicar índices de texto completo** – Gera script para a criação de índices de texto completo. O padrão é **False**.  
  
4.  **Publicar índices** – Inclui índices em tabelas no processo de publicação. O padrão é **True**. Os índices ajudam você a localizar dados rapidamente.  
  
5.  **Publicar chaves primárias** – Inclui a criação de chaves primárias no processo de publicação. O padrão é **True**. Chaves primárias identificam com exclusividade cada linha de uma tabela. Para obter mais informações, consulte [Primary and Foreign Key Constraints](../tables/primary-and-foreign-key-constraints.md).  
  
6.  **Publicar gatilhos** – Inclui a criação de gatilhos DML no processo de publicação. O padrão é **True**. Um gatilho DML é uma ação programada para executar quando um evento de linguagem de manipulação de dados (DML) ocorre no servidor de banco de dados. Para obter mais informações, consulte [DML Triggers](../triggers/dml-triggers.md).  
  
7.  **Publicar chaves exclusivas** – Inclui a criação de chaves exclusivas em tabelas no processo de publicação. Chaves exclusivas evitam a inserção de dados duplicados. O padrão é **True**. Para obter mais informações, consulte [Unique Constraints and Check Constraints](../tables/unique-constraints-and-check-constraints.md).  
  
8.  **Publicar controle de alterações** – Incluirá controle de alterações no processo de publicação se for habilitado no banco de dados de origem ou nas tabelas no banco de dados de origem. O padrão é **False**. Para obter mais informações, veja [Sobre o controle de alterações &#40;SQL Server&#41;](../track-changes/about-change-tracking-sql-server.md).  
  
9. **Publicar opções de compactação de dados** – Incluirá opções de compactação de dados no processo de publicação se eles forem configurados no banco de dados de origem ou em tabelas no banco de dados de origem. O padrão é **True**. Para saber mais, veja [Data Compression](../data-compression/data-compression.md).  
  
###  <a name="provider-configuration-page"></a><a name="ProvConfig"></a>Página de configuração do provedor  
 Use esta caixa de diálogo para exibir ou modificar as configurações de hospedagem do provedor. É possível usar esta caixa de diálogo para o seguinte:  
  
-   Exibir, adicionar ou editar informações de conexão para um provedor de hospedagem.  
  
-   Exibir, adicionar, editar ou excluir um banco de dados para uma conexão de provedor.  
  
-   Configurar automaticamente bancos de dados para um provedor de hospedagem.  
  
 Um provedor de hospedagem especifica as informações de conexão para um serviço Web criado usando o projeto Database Publishing Services no SQL Server Hosting Toolkit, no CodePlex.  
  
 **Nome** – Nome do provedor de hospedagem.  
  
 **Endereço de serviço Web** – Endereço HTTPS do serviço de hospedagem.  
  
 **Autenticação de serviço Web** – O nome de usuário e senha exigiu fazer logon no serviço de hospedagem.  
  
 **Salvar senha** – Criptografe e salve a senha no computador local.  
  
 **Bancos de dados disponíveis** – Os bancos de dados configurados para provedores de hospedagem são listados em ordem crescente no formato: *server_name*.*database_name*.  
  
 **Novo** – Abra a caixa de diálogo de configuração **Banco de Dados** e adicione um novo banco de dados.  
  
 **Editar** – Abra a caixa de diálogo de configuração **Banco de Dados** para o banco de dados selecionado.  
  
 **Excluir** – Exclua o banco de dados selecionado.  
  
 **Definir como padrão** – Selecione o banco de dados selecionado como padrão.  
  
 **OK** – Salve todas as alterações feitas nessa caixa de diálogo e retorne ao assistente.  
  
 **Cancelar** – Desfaça todas as alterações feitas nessa caixa de diálogo e retorne para o assistente.  
  
###  <a name="summary-page"></a><a name="Summary"></a> Página de Resumo  
 Essa página resume as opções selecionadas nesse assistente. Para alterar uma opção, clique em **Anterior**. Para começar a gerar scripts que serão salvos ou publicados, clique em **Avançar**.  
  
 **Examinar as seleções** – Exibe as seleções feitas em cada página do assistente. Expanda um nó para ver as opções selecionadas para a página correspondente.  
  
###  <a name="save-or-publish-scripts-page"></a><a name="SavePubScripts"></a> Página Salvar ou Publicar Scripts  
 Use esta página para monitorar o andamento do assistente enquanto ele ocorre.  
  
 **Detalhes** – Exiba a coluna **Ação** para consultar o andamento do assistente. Depois de gerar os scripts, o assistente salva os scripts em um arquivo ou os usa para publicar em um serviço Web, dependendo de suas seleções. Quando cada uma dessas etapas estiver completa, clique no valor na coluna **Resultado** para ver o resultado da etapa correspondente.  
  
 **Salvar Relatório** – Clique para salvar os resultados do progresso do assistente em um arquivo.  
  
 **Cancelar** – Clique para fechar o assistente antes de o processamento ser concluído, ou se ocorrer um erro.  
  
 **Concluir** – Clique para fechar o assistente após a conclusão do processamento, ou se ocorrer um erro.  
  
## <a name="see-also"></a>Consulte Também  
 [Instalando o SMO](../server-management-objects-smo/installing-smo.md)   
 [Copiar bancos de dados para outros servidores](../databases/copy-databases-to-other-servers.md)  
  
  
