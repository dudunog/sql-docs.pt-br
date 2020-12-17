---
title: Ajuda do Assistente de Instalação | Microsoft Docs
description: Especifique se deseja criar uma instância padrão ou uma instância nomeada do SQL Server usando a Configuração de Instância no Assistente de instalação do SQL Server.
ms.custom: ''
ms.date: 08/16/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
f1_keywords:
- instance configuration, Setup
helpviewer_keywords:
- Instance Name page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Instance Name page
ms.assetid: 5bf822fc-6dec-4806-a153-e200af28e9a5
author: cawrites
ms.author: chadam
robots: noindex,nofollow
ms.openlocfilehash: 837e1c099dba7d19100bdaf2216a2c0cf879c62e
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97482314"
---
# <a name="installation-wizard-help"></a>Ajuda do Assistente de Instalação

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Este artigo descreve algumas das páginas de configuração no Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="instance-configuration-page"></a>Página Configuração da instância

Use a página **Configuração de Instância** do Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para especificar se uma instância padrão ou uma instância nomeada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser criada. Se uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ainda não estiver instalada, uma instância padrão será criada, a menos que você especifique uma instância nomeada.  
  
Cada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consiste em um conjunto distinto de serviços que têm configurações específicas para ordenações e outras opções. A estrutura de diretórios, a estrutura do Registro e os nomes do serviço refletem o nome da instância e uma ID de instância específica criada durante a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Uma instância é a instância padrão ou uma instância nomeada. O nome de instância padrão é MSSQLSERVER. O nome padrão não precisa de um cliente para especificar o nome da instância para estabelecer uma conexão. Uma instância nomeada é determinada pelo usuário durante a Instalação. Você pode instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como uma instância nomeada sem instalar a instância padrão em primeiro lugar. Apenas uma instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], independentemente da versão, pode ser a instância padrão em determinado momento.  
  
> [!NOTE]  
> Com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep, você pode especificar o nome da instância ao concluir uma instância preparada na página de **Configuração da Instância**. Você poderá configurar a instância preparada que está concluindo como uma instância padrão se não houver nenhuma instância padrão existente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador.  
  
### <a name="multiple-instances"></a>Várias instâncias
  
O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dá suporte a várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um único servidor ou processador, mas somente uma instância pode ser a padrão. Todas as demais devem ser instâncias nomeadas. Um computador pode executar várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] simultaneamente e cada instância é executada independentemente das demais.  
  
 Para saber mais, confira [Especificações de capacidade máxima para o SQL Server](../maximum-capacity-specifications-for-sql-server.md).  
  
### <a name="options"></a>Opções

**Somente instâncias de cluster de failover**: Especifique o nome de rede do cluster de failover [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse nome identifica a instância do cluster de failover na rede.  
  
**Decidir entre um padrão ou uma instância nomeada**: Considere as seguintes informações ao decidir se deve instalar uma instância padrão ou nomeada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
* Se você planeja instalar uma única instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um servidor de banco de dados, ela deve ser uma instância padrão.  
  
* Use uma instância nomeada para situações em que planeja ter várias instâncias no mesmo computador. Um servidor pode hospedar somente uma instância padrão.  
* Qualquer aplicativo que instale o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] deve instalá-lo como uma instância nomeada. Essa prática minimizará conflitos quando vários aplicativos forem instalados no mesmo computador.
  
**Instância padrão**: Selecione esta opção para instalar uma instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Um computador pode hospedar apenas uma instância padrão; todas as demais devem ser nomeadas. Entretanto, se você tiver uma instância padrão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalada, poderá adicionar uma instância padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no mesmo computador.  
  
**Instância nomeada**: Selecione esta opção para criar uma nova instância nomeada. Esteja ciente das seguintes informações ao nomear uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
* Nomes de instância não diferenciam maiúsculas de minúsculas.  
  
* Nomes de instância não podem iniciar nem terminar com um sublinhado (_).  
  
* Os nomes de instância não podem conter o termo "Padrão" ou outras palavras-chave reservadas. Se uma palavra-chave reservada for usada em um nome de instância, ocorrerá um erro de Instalação. Para saber mais, confira [Palavras-chave reservadas &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md).  
  
* Se você especificar MSSQLSERVER para o nome de instância, uma instância padrão será criada.  
  
* Uma instalação do [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] sempre é instalada como uma instância nomeada de “[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]”. Você não pode especificar um nome de instância diferente para essa função de recurso.  
  
* Os nomes de instância estão limitados a 16 caracteres.  
  
* O primeiro caractere do nome da instância deve ser uma letra. As letras aceitáveis são as definidas pelo Padrão Unicode 2.0. Essas letras incluem os caracteres latinos de a-z, A-Z e caracteres de letra de outros idiomas.  
  
* Os caracteres subsequentes podem ser letras definidas pelo Padrão Unicode 2.0, números decimais de Latim Básico ou outros scripts nacionais, o sinal de cifrão ($) ou um sublinhado (_).  
  
* Não são permitidos espaços inseridos ou outros caracteres especiais em nomes de instância. Os caracteres de barra invertida (\\), vírgula (,), dois-pontos (:), ponto-e-vírgula (;), aspas simples ('), E comercial (&), hífen (-) e arroba (@) também não são permitidos.  
  
  Somente caracteres válidos na página de código atual do Windows podem ser usados em nomes de instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se um caractere Unicode sem suporte for usado, ocorrerá um erro de Instalação.  
  
**Instâncias e recursos detectados**: Exiba uma lista de instâncias e componentes instalados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no computador em que a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada.  
  
**ID da Instância**: Por padrão, o nome da instância é usado como a ID da Instância. Essa ID é usada para identificar os diretórios de instalação e as chaves do Registro da sua instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. O mesmo comportamento ocorre com instâncias padrão e instâncias nomeadas. No caso de uma instância padrão, o nome da instância e a ID da Instância é MSSQLSERVER. Para usar uma ID de instância não padrão, especifique-a no campo **ID da Instância**.  
  
> [!IMPORTANT]  
>  Com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep, a ID da Instância exibida na página **Instance Configuration** é a ID da Instância especificada durante a etapa de preparação da imagem do processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep. Você não poderá especificar uma ID da Instância diferente durante a etapa de conclusão de imagem.

> [!NOTE]  
>  As IDs de instância que começam com sublinhado (_) ou contêm o sinal numérico (#) ou o cifrão ($) não têm suporte.  
  
Para saber mais sobre nomenclatura de ID de instância, locais de arquivos e diretórios, confira [Locais de arquivo para instâncias nomeadas e padrão do SQL Server](file-locations-for-default-and-named-instances-of-sql-server.md).  
  
Todos os componentes de uma determinada instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são gerenciados como uma unidade. Todos os service packs e as atualizações do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se aplicam a todos os componentes de uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Todos os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que compartilham o mesmo nome de instância devem atender aos seguintes critérios:  
  
* Mesma versão
* Mesma edição
* Mesmas configurações de idioma
* Mesmo estado clusterizado
* Mesmo sistema operacional  
  
> [!NOTE]  
> [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não dá suporte a cluster.  

## <a name="analysis-services-configuration---account-provisioning-page"></a>Configuração do Analysis Services – Página Provisionamento de conta
  
Use esta página para definir o modo de servidor e para conceder permissões administrativas a usuários ou serviços que requerem acesso irrestrito ao [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. A Instalação não adiciona automaticamente o grupo local do Windows BUILTIN\Administradores à função de administrador de servidor [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] da instância que está sendo instalada. Para adicionar o grupo Administradores local à função de administrador do servidor, é necessário especificar explicitamente esse grupo.  
  
Se você estiver instalando o [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], conceda permissões administrativas aos administradores de farms do SharePoint ou aos administradores de serviços responsáveis por uma implantação do servidor [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um farm do [!INCLUDE[SPS2010](../../includes/sps2010-md.md)].  
  
### <a name="options"></a>Opções

**Modo do Servidor**: O modo de servidor especifica o tipo de bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que podem ser implantados no servidor. Os modos de servidor são determinados durante a Instalação e não podem ser modificados posteriormente. Cada modo é mutuamente exclusivo, o que significa que você precisará de duas instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], cada uma configurada para um modo diferente, para dar suporte às soluções de modelo OLAP (processamento analítico online) clássico e de tabela.  
  
**Especificar administradores**: Você deve especificar, pelo menos, um administrador de servidor para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os usuários ou grupos que você especificar se tornarão membros da função de administrador de servidor da instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que está sendo instalada. Esses membros devem ter contas de usuário de domínio do Windows no mesmo domínio que o computador no qual você está instalando o software.  
  
> [!NOTE]  
> O UAC (Controle de Conta de Usuário) é um recurso de segurança do Windows que requer um administrador para aprovar especificamente aplicativos ou ações administrativas para que tenham permissão de execução. Como o UAC é ativado por padrão, será solicitado que você permita operações específicas que exijam privilégios elevados. É possível configurar o UAC para alterar o comportamento padrão ou personalizar o UAC para programas específicos. Para saber mais sobre o UAC e sua configuração, confira o [Guia passo a passo do Controle de Conta de Usuário](https://go.microsoft.com/fwlink/?linkid=196350) e [Controle de Conta de Usuário (Wikipedia)](https://go.microsoft.com/fwlink/?linkid=196351).  
  
### <a name="see-also"></a>Confira também
  
* [Configurar contas de serviço &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/instances/configure-service-accounts-analysis-services)
* [Configurar contas e permissões de serviço Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  

## <a name="analysis-services-configuration---data-directories-page"></a>Página Configuração do Analysis Services - diretórios de dados

Os diretórios padrão na tabela a seguir podem ser configurados pelo usuário durante a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A permissão para acessar esses arquivos é concedida a administradores locais e a membros do grupo de segurança SQLServerMSASUser$\<instance> que é criado e provisionado durante a instalação.  
  
### <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
  
|Descrição|Diretório padrão|Recomendações|  
|-----------------|-----------------------|---------------------|  
|**Diretório raiz de dados**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS *nn*.\<InstanceID>\OLAP\Data\ |Assegure-se de que a pasta \Arquivos de programas\Microsoft SQL Server\ esteja protegida com permissões limitadas. O desempenho do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] depende, em muitas configurações, do desempenho do armazenamento no qual o diretório de dados está localizado. Coloque esse diretório no armazenamento de melhor desempenho conectado ao sistema. Para instalações de cluster de failover, verifique se os diretórios de dados estão colocados no disco compartilhado.|  
|**Diretório do arquivo de log**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS *nn*.\<InstanceID>\OLAP\Log\ |Este diretório é para arquivos de log do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e inclui o log do FlightRecorder. Se você aumentar a duração do registrador de voo, atente para que o diretório de logs tenha espaço suficiente.|  
|**Diretório temporário**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS *nn*.\<InstanceID>\OLAP\Temp\ |Coloque o diretório Temp em um subsistema de armazenamento de alto desempenho.|  
|**Diretório de backup**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS *nn*.\<InstanceID>\OLAP\Backup\ |Este diretório é para arquivos de backup padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Em instalações do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, esse diretório também é o local em que os Serviços de Sistema do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] armazenam em cache arquivos de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].<br /><br /> Verifique se as permissões apropriadas estão definidas para impedir perda de dados e se o grupo de usuários do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tem permissões suficientes para gravar no diretório de backup. O uso de uma unidade mapeada para diretórios de backup não tem suporte.|  
  
### <a name="considerations"></a>Considerações  
  
* Quando instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] são implantadas em um farm do SharePoint, elas armazenam arquivos de aplicativos, arquivos de dados e propriedades em bancos de dados de conteúdo e bancos de dados de aplicativo de serviços.  
  
* Ao adicionar recursos a uma instalação existente, não é possível alterar o local de um recurso instalado anteriormente, nem especificar o local para o novo recurso.  

* Talvez você precise configurar softwares de verificação, como aplicativos antivírus e antispyware, para excluir pastas e tipos de arquivos do SQL Server. Examine este artigo de suporte para obter mais informações: [Software antivírus em computadores que executam o SQL Server](https://support.microsoft.com/kb/309422).
  
* Se você especificar diretórios de instalação não padrão, verifique se as pastas de instalação são exclusivas para essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não compartilhe os diretórios nesta caixa de diálogo com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Também instale os componentes [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em diretórios separados.  
  
* Os arquivos de programas e os arquivos de dados não podem ser instalados nas seguintes situações:  
  
  * Em uma unidade de disco removível  
  * Em um sistema de arquivos que usa compactação  
  * Em um diretório onde os arquivos do sistema estão localizados  
  
### <a name="see-also"></a>Confira também

Para saber mais sobre nomenclatura de ID de instância, locais de arquivos e diretórios, confira [Locais de arquivo para instâncias nomeadas e padrão do SQL Server](file-locations-for-default-and-named-instances-of-sql-server.md).  
  
### <a name="analysis-services-configuration---data-directories-page"></a>Página Configuração do Analysis Services - diretórios de dados

Os diretórios padrão na tabela a seguir podem ser configurados pelo usuário durante a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A permissão para acessar esses arquivos é concedida a administradores locais e a membros do grupo de segurança SQLServerMSASUser$\<instance> que é criado e provisionado durante a instalação.  
  
#### <a name="ui-element-list"></a>Lista de elementos da interface do usuário
  
|Descrição|Diretório padrão|Recomendações|  
|-----------------|-----------------------|---------------------|  
|**Diretório raiz de dados** |\<Drive:>\Program Files\Microsoft SQL Server\MSAS *nn*.\<InstanceID>\OLAP\Data |Assegure-se de que a pasta \Arquivos de programas\Microsoft SQL Server\ esteja protegida com permissões limitadas. O desempenho do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] depende, em muitas configurações, do desempenho do armazenamento no qual o diretório de dados está localizado. Coloque esse diretório no armazenamento de melhor desempenho conectado ao sistema. Para instalações de cluster de failover, verifique se os diretórios de dados estão colocados no disco compartilhado.|  
|**Diretório do arquivo de log**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS *nn*.\<InstanceID>\OLAP\Log |Este diretório é para arquivos de log do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e inclui o log do FlightRecorder. Se você aumentar a duração do registrador de voo, atente para que o diretório de logs tenha espaço suficiente.|  
|**Diretório temporário**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS *nn*.\<InstanceID>\OLAP\Temp |Coloque o diretório Temp em um subsistema de armazenamento de alto desempenho.|  
|**Diretório de backup**|\<Drive:>\Program Files\Microsoft SQL Server\MSAS *nn*.\<InstanceID>\OLAP\Backup |Este diretório é para arquivos de backup padrão do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Em instalações do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, também é o local em que os Serviços de Sistema do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] armazenam em cache arquivos de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].<br /><br /> Verifique se as permissões apropriadas estão definidas para impedir perda de dados e se o grupo de usuários do serviço do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tem permissões suficientes para gravar no diretório de backup. O uso de uma unidade mapeada para diretórios de backup não tem suporte.|  
  
#### <a name="considerations"></a>Considerações
  
* Quando instâncias do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] são implantadas em um farm do SharePoint, elas armazenam arquivos de aplicativos, arquivos de dados e propriedades em bancos de dados de conteúdo e bancos de dados de aplicativo de serviços.  
  
* Ao adicionar recursos a uma instalação existente, não é possível alterar o local de um recurso instalado anteriormente, nem especificar o local para o novo recurso.  

* Talvez você precise configurar softwares de verificação, como aplicativos antivírus e antispyware, para excluir pastas e tipos de arquivos do SQL Server. Para saber mais, veja [Software antivírus em computadores que executam o SQL Server](https://support.microsoft.com/kb/309422).
  
* Se você especificar diretórios de instalação não padrão, verifique se as pastas de instalação são exclusivas para essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não compartilhe os diretórios nesta caixa de diálogo com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Também instale os componentes [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em diretórios separados.  
  
* Os arquivos de programas e os arquivos de dados não podem ser instalados nas seguintes situações:  
  
  * Em uma unidade de disco removível  
  * Em um sistema de arquivos que usa compactação  
  * Em um diretório onde os arquivos do sistema estão localizados  
  
#### <a name="see-also"></a>Confira também

* Para saber mais sobre nomenclatura de ID de instância, locais de arquivos e diretórios, confira [Locais de arquivo para instâncias nomeadas e padrão do SQL Server](file-locations-for-default-and-named-instances-of-sql-server.md)  
* [Permissões de compartilhamento e de NTFS em um servidor de arquivos](https://docs.microsoft.com/iis/web-hosting/configuring-servers-in-the-windows-web-platform/configuring-share-and-ntfs-permissions)

## <a name="database-engine-configuration---server-configuration-page"></a><a name="serverconfig"></a> Configuração do Mecanismo de Banco de Dados – Página Configuração do Servidor

Use esta página para definir o modo de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e adicionar grupos ou usuários do Windows como administradores do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
### <a name="considerations-for-running-sscurrent"></a>Considerações sobre execução do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]

Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o grupo BUILTIN\Administradores era provisionado como um logon no [!INCLUDE[ssDE](../../includes/ssde-md.md)] e os membros do grupo local Administradores podiam fazer logon usando as credenciais de Administrador. No entanto, o uso de permissões elevadas não é uma prática recomendada.

No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o grupo BUILTIN\Administradores não é provisionado como logon. Crie um logon do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cada usuário administrativo e adicionar esse logon à função de servidor fixa **sysadmin** durante a instalação de uma nova instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Faça o mesmo para contas do Windows que executam trabalhos do agent [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], incluindo trabalhos de agente de replicação.  
  
### <a name="options"></a>Opções

**Modo de segurança**: Selecione **Autenticação do Windows** ou **Autenticação de Modo Misto** para sua instalação.  
  
**Provisionamento de entidade de segurança do Windows**: Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o grupo local Windows BUILTIN\Administradores era colocado na função de servidor **sysadmin** do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], concedendo efetivamente aos administradores do Windows o acesso à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o grupo BUILTIN\Administradores não é provisionado na função de servidor **sysadmin**. Em vez disso, você deve provisionar explicitamente administradores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para as novas instalações durante a Instalação.  
  
> [!IMPORTANT]  
> Você deve provisionar explicitamente administradores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para as novas instalações durante a Instalação. A Instalação não permitirá que você continue até que conclua esta etapa.
  
**Especificar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administradores**: É necessário especificar, pelo menos, uma entidade do Windows para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para adicionar a conta sob a qual a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está sendo executada, clique no botão **Adicionar Usuário Atual**. Para adicionar ou remover contas da lista de administradores do sistema, selecione **Adicionar** ou **Remover** e edite a lista de usuários, grupos ou computadores que terão privilégios de administrador para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Depois de concluir a edição da lista, selecione **OK** e verifique a lista de administradores na caixa de diálogo de configuração. Se a lista estiver completa, selecione **Avançar**.  
  
Se você selecionar a **Autenticação de Modo Misto**, deverá fornecer credenciais de logon para a conta interna [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administrador do sistema (**sa**).  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
**Modo de Autenticação do Windows**: Quando um usuário se conecta por uma conta de usuário do Windows, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valida o nome e a senha da conta usando o token da entidade do Windows no sistema operacional. A autenticação do Windows é o modo de autenticação padrão e é muito mais segura do que a autenticação de modo misto. A autenticação do Windows usa o protocolo de segurança Kerberos, fornece imposição de política de senha e termos de validação de complexidade para senhas fortes, dá suporte ao bloqueio de contas e dá suporte à expiração de senhas.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  

> [!IMPORTANT]  
> [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] Nunca defina uma senha de **sa** em branco ou fraca.  
  
**Modo Misto (autenticação do Windows ou do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])** : Permite que os usuários se conectem usando autenticação do Windows ou autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os usuários que se conectarem por uma conta de usuário do Windows podem usar conexões confiáveis que são validadas pelo Windows.  
  
Se você deve escolher autenticação de modo misto e precisa usar logons do SQL a fim de acomodar aplicativos herdados, deverá definir senhas fortes para todas as contas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
> A autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é fornecida somente para fins de compatibilidade com versões anteriores. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
**Digite a senha**: Insira e confirme o logon de administrador de sistema (**sa**). As senhas são a primeira linha de defesa contra intrusos; portanto, a configuração de senhas fortes é essencial para a segurança do seu sistema. Nunca defina uma senha de **sa** em branco ou fraca.  
  
> [!NOTE]  
> Senhas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem conter de 1 até 128 caracteres, incluindo qualquer combinação de letras, símbolos e números. Se você escolher a autenticação de modo misto, deverá inserir uma senha forte de **sa** antes de continuar na próxima página do Assistente de Instalação.  
  
#### <a name="strong-password-guidelines"></a>Diretrizes de senha forte
  
As senhas fortes não são prontamente adivinhadas por uma pessoa e não são facilmente violadas usando-se um programa de computador. As senhas fortes não podem usar condições ou termos proibidos, incluindo:  
  
* Um espaço em branco ou condição NULL
* "Password"
* "Admin"
* "Administrador"
* "sa"
* "sysadmin"

Uma senha forte não pode ter os termos a seguir associados ao computador de instalação:  
  
* O nome do usuário atualmente conectado à máquina
* O nome do computador  
  
Uma senha forte deve ter mais de 8 caracteres e satisfazer pelo menos três dos quatro critérios a seguir:  
  
* Deve conter letras maiúsculas.
* Deve conter letras minúsculas.  
* Deve conter números.
* Deve conter caracteres não alfanuméricos; por exemplo, #,% ou ^.  
  
As senhas inseridas nessa página devem satisfazer os requisitos de política de senha forte. Se você tiver qualquer automação que use autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], assegure-se de que a senha satisfaça os requisitos de política de senha forte.  
  
### <a name="see-also"></a>Confira também

Para saber mais sobre como escolher a autenticação do Windows vs. autenticação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Escolher um modo de autenticação](../../relational-databases/security/choose-an-authentication-mode.md).  

Para saber mais sobre como escolher uma conta para executar o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], confira [Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).

## <a name="database-engine-configuration---data-directories-page"></a><a name ="datadir"></a> Configuração do Mecanismo de Banco de Dados – página Diretórios de Dados

Use esta página para especificar a localização de instalação para programas e arquivos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Com base no tipo de instalação, o armazenamento com suporte pode incluir disco local, armazenamento compartilhado ou um servidor de arquivos SMB.  
  
Para especificar um compartilhamento de arquivos SMB como um diretório, você deve digitar o caminho UNC com suporte manualmente. Não há suporte para a navegação até um compartilhamento de arquivos SMB. O exemplo mostra o caminho UNC de um compartilhamento de arquivos SMB com suporte:

`\\<ServerName>\<ShareName>\...`

### <a name="standalone-instance-of-ssnoversion"></a>Instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
  
Em uma instância autônoma de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a tabela a seguir lista os tipos de armazenamento compatíveis e os diretórios padrão que você pode configurar durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
### <a name="ui-element-list"></a>Lista de elementos da interface do usuário
  
|Descrição|Tipos de armazenamento com suporte|Diretório padrão|Recomendações|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**Diretório raiz de dados**|Disco local, servidor de arquivos SMB, armazenamento compartilhado* |\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\ |A instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configura ACLs (lista de controle de acesso) para diretórios do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e interrompe a herança como parte da configuração.|  
|**Diretório do banco de dados de usuário**|Disco local, servidor de arquivos SMB, armazenamento compartilhado*|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL *nn*.\<InstanceID>\MSSQL\Data |As práticas recomendadas para diretórios de dados de usuário dependem dos requisitos de carga de trabalho e desempenho.|  
|**Diretório de log do banco de dados de usuário**|Disco local, servidor de arquivos SMB, armazenamento compartilhado*|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL *nn*.\<InstanceID>\MSSQL\Data|Verifique se o diretório de log tem espaço suficiente.|  
|**Diretório de backup**|Disco local, servidor de arquivos SMB, armazenamento compartilhado*|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL *nn*.\<InstanceID>\MSSQL\Backup|Defina as permissões adequadas para evitar perda de dados e verifique se a conta de usuário para o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tem permissões suficientes para realizar gravações no diretório de backup. O uso de uma unidade mapeada para diretórios de backup não tem suporte.|  
  
\* Embora haja suporte para discos compartilhados, não recomendamos seu uso para uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="failover-cluster-instance-of-ssnoversion"></a>Instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

Em uma instância de cluster de failover de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a tabela a seguir lista os tipos de armazenamento compatíveis e os diretórios padrão que você pode configurar durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Descrição|Tipos de armazenamento com suporte|Diretório padrão|Recomendações|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**Diretório raiz de dados**|Armazenamento compartilhado, servidor de arquivos SMB|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<br /><br /> **Dica**: Se você selecionar **disco compartilhado** na página **Seleção de Disco de Cluster**, o padrão será o primeiro disco compartilhado. O padrão do campo será um espaço em branco se nenhuma seleção for feita na página **Seleção de Disco de Cluster**.|A instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configura ACLs para diretórios do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e interrompe a herança como parte da configuração.|  
|**Diretório do banco de dados de usuário**|Armazenamento compartilhado, servidor de arquivos SMB|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL *nn*.\<InstanceID>\MSSQL\Data<br /><br /> **Dica**: Se você selecionar **disco compartilhado** na página **Seleção de Disco de Cluster**, o padrão será o primeiro disco compartilhado. O padrão do campo será um espaço em branco se nenhuma seleção for feita na página **Seleção de Disco de Cluster**.|As práticas recomendadas para diretórios de dados de usuário dependem dos requisitos de carga de trabalho e desempenho.|  
|**Diretório de log do banco de dados de usuário**|Armazenamento compartilhado, servidor de arquivos SMB|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL *nn*.\<InstanceID>\MSSQL\Data<br /><br /> **Dica**: Se você selecionar **disco compartilhado** na página **Seleção de Disco de Cluster**, o padrão será o primeiro disco compartilhado. O padrão do campo será um espaço em branco se nenhuma seleção for feita na página **Seleção de Disco de Cluster**.|Verifique se o diretório de log tem espaço suficiente.|  
|**Diretório de backup**|Disco local, armazenamento compartilhado, servidor de arquivos SMB|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL *nn*.\<InstanceID>\MSSQL\Backup<br /><br /> **Dica**: Se você selecionar **disco compartilhado** na página **Seleção de Disco de Cluster**, o padrão será o primeiro disco compartilhado. O padrão do campo será um espaço em branco se nenhuma seleção for feita na página **Seleção de Disco de Cluster**.|Defina as permissões adequadas para evitar perda de dados e verifique se a conta de usuário do serviço do SQL Server tem permissões suficientes para gravar no diretório de backup. O uso de uma unidade mapeada para diretórios de backup não tem suporte.|  
  
### <a name="security-considerations"></a>Considerações de segurança
  
A instalação configurará ACLs para diretórios do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e interromperá a herança como parte da configuração.  
  
As seguintes recomendações se aplicam aos servidores de arquivos SMB:  
  
* A conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá ser uma conta de domínio se for usado um servidor de arquivos SMB.  
  
* A conta usada para instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ter permissões NTFS Full Control na pasta de compartilhamento de arquivos SMB usada como o diretório de dados.  
  
* A conta usada para instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ter privilégios SeSecurityPrivilege no servidor de arquivos SMB. Para conceder esse privilégio, use o console de Política de Segurança Local no servidor de arquivos para adicionar a conta de configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à política **Gerenciar o log de auditoria e segurança**. Essa configuração está na seção **Atribuições de Direitos do Usuário**, em **Políticas Locais**, no console Política de Segurança Local.

### <a name="considerations"></a>Considerações
  
* Ao adicionar recursos a uma instalação existente, você não pode alterar o local de um recurso instalado anteriormente, nem especificar o local para um novo recurso.  
  
* Se você especificar diretórios de instalação não padrão, verifique se as pastas de instalação são exclusivas para essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Não compartilhe os diretórios nesta caixa de diálogo com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Também instale os componentes [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em diretórios separados.  
  
* Os arquivos de programas e os arquivos de dados não podem ser instalados nas seguintes situações:  
  
  * Em uma unidade de disco removível
  * Em um sistema de arquivos que usa compactação
  * Em um diretório onde os arquivos do sistema estão localizados
  * Em uma unidade de rede mapeada em uma instância de cluster de failover  
  
## <a name="a-nametempdb-database-engine-configuration---tempdb-page"></a><a name="tempdb"><a/> Configuração do Mecanismo de Banco de Dados – página TempDB

Use esta página para especificar a localização, tamanho, configurações de crescimento e número de arquivos dos dados de **tempdb** e do arquivo de log para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Com base no tipo de instalação, o armazenamento com suporte pode incluir disco local, armazenamento compartilhado ou um servidor de arquivos SMB.  
  
Para especificar um compartilhamento de arquivos SMB como um diretório, você deve digitar o caminho UNC com suporte manualmente. Não há suporte para a navegação até um compartilhamento de arquivos SMB. O exemplo mostra o caminho UNC de um compartilhamento de arquivos SMB com suporte:

`\\<ServerName>\<ShareName>\....`
  
### <a name="data-and-log-directories-for-a-standalone-instance-of-ssnoversion"></a>Diretórios de dados e de log para uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

Nas instâncias autônomas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a tabela a seguir lista os tipos de armazenamento com suporte e os diretórios padrão que você pode definir durante a instalação.  
  
|Descrição|Tipo de armazenamento com suporte|Diretório padrão|Recomendações|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**Diretórios de dados**|Disco local, servidor de arquivos SMB, armazenamento compartilhado* |\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL *nn*.\<InstanceID>\MSSQL\Data|A instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configura ACLs para diretórios do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e interrompe a herança como parte da configuração.<br /><br /> As práticas recomendadas para diretórios **tempdb** dependem dos requisitos de carga de trabalho e desempenho. Para distribuir os arquivos de dados entre vários volumes, especifique várias pastas/unidades.|  
|**Diretório de log**|Disco local, servidor de arquivos SMB, armazenamento compartilhado*|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL *nn*.\<InstanceID>\MSSQL\Data|Verifique se o diretório de log tem espaço suficiente.|  
  
\* Embora haja suporte para discos compartilhados, não recomendamos seu uso para uma instância autônoma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="data-and-log-directories-for-a-failover-cluster-instance-of-ssnoversion"></a>Diretórios de dados e de log para uma instância de cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

Em uma instância de cluster de failover de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a tabela a seguir lista os tipos de armazenamento compatíveis e os diretórios padrão que você pode configurar durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Descrição|Tipo de armazenamento com suporte|Diretório padrão|Recomendações|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**Diretório de dados tempdb**|Disco local, armazenamento compartilhado, servidor de arquivos SMB|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL *nn*.\<InstanceID>\Data<br /><br /> **Dica**: Se você selecionar **disco compartilhado** na página **Seleção de Disco de Cluster**, o padrão será o primeiro disco compartilhado. O padrão do campo será um espaço em branco se nenhuma seleção for feita na página **Seleção de Disco de Cluster**.|A instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configura ACLs para diretórios do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e interrompe a herança como parte da configuração.<br /><br /> Verifique se o diretório, ou diretórios, especificado (se vários arquivos forem especificados) é válido para todos os nós do cluster. Durante o failover, se os diretórios de **tempdb** não estiverem disponíveis no nó de destino de failover, o recurso do SQL Server não é exibido online.|  
|**Diretório de logs de tempdb**|Disco local, armazenamento compartilhado, servidor de arquivos SMB|\<Drive:>\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL *nn*.\<InstanceID>\MSSQL\Data<br /><br /> **Dica**: Se você selecionar **disco compartilhado** na página **Seleção de Disco de Cluster**, o padrão será o primeiro disco compartilhado. O padrão do campo será um espaço em branco se nenhuma seleção for feita na página **Seleção de Disco de Cluster**.|As práticas recomendadas para diretórios de dados de usuário dependem dos requisitos de carga de trabalho e desempenho.<br /><br /> Verifique se o diretório especificado é válido para todos os nós de cluster. Durante o failover, se os diretórios de **tempdb** não estiverem disponíveis no nó de destino de failover, o recurso do SQL Server não é exibido online.<br /><br /> Verifique se o diretório de log tem espaço suficiente.|  
  
### <a name="ui-element-list"></a>Lista de elementos da interface do usuário

Defina as configurações para **tempdb** de acordo com suas necessidades e carga de trabalho. As configurações a seguir se aplicam aos arquivos de dados **tempdb** :  
  
* **Número de arquivos** é o número total de arquivos de dados para **tempdb**. O valor padrão é inferior a oito, ou o número de núcleos lógicos detectados pela Instalação. Como regra geral, se o número de processadores lógicos for menor ou igual a 8, use o mesmo número de arquivos de dados que o de processadores lógicos. Se o número de processadores lógicos for maior que 8, use 8 arquivos de dados. Se a contenção acontecer, aumente o número de arquivos de dados em múltiplos de quatro (até o número dos processadores lógicos) até que a contenção seja reduzida a níveis aceitáveis ou faça alterações no código ou na carga de trabalho.
  
* **Tamanho inicial (MB)** é o tamanho inicial em megabytes de cada arquivo de dados **tempdb**. O valor padrão é 8 MB (ou 4 MB para [!INCLUDE[ssexpress](../../includes/ssexpress_md.md)]). [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] apresenta um tamanho do arquivo inicial máximo de 262.144 MB (256 GB). [!INCLUDE[sssql15](../../includes/sssql15-md.md)] tem um tamanho do arquivo inicial máximo de 1024 MB. Todos os arquivo de dados **tempdb** têm o mesmo tamanho inicial. Como o **tempdb** é recriado sempre que o SQL Server é iniciado ou passa por failover, especifique um tamanho próximo ao tamanho exigido por sua carga de trabalho para uma operação normal. Para otimizar ainda mais a criação de **tempdb** durante o início, habilite a [Inicialização instantânea de arquivo do banco de dados](../../relational-databases/databases/database-instant-file-initialization.md).  
  
* **Tamanho inicial total (MB)** é o tamanho cumulativo de todos os arquivos de dados **tempdb**.  
  
* **Expansão automática (MB)** é a quantidade de espaço em megabytes que cada arquivo de dados **tempdb** aumentará automaticamente quando ficar sem espaço. No [!INCLUDE[sssql15](../../includes/sssql15-md.md)] e posterior, todos os arquivos de dados aumentarão ao mesmo tempo conforme a quantidade especificada nessa configuração.  
  
* **Expansão automática total (MB)** é o tamanho cumulativo de cada evento de expansão automática.  
* **Diretórios de dados** mostra todos os diretórios que contêm arquivos de dados **tempdb**. Quando há vários diretórios, os arquivos de dados são colocados em diretórios por meio de um rodízio. Por exemplo, se você criar três diretórios e especificar oito arquivos de dados, os arquivos de dados 1, 4 e 7 serão criados no primeiro diretório. Os arquivos de dados 2, 5 e 8 serão criados no segundo diretório. Os arquivos de dados 3 e 6 estarão no terceiro diretório.  
  
* Para adicionar diretórios, selecione **Adicionar...** .  
  
* Para remover um diretório, selecione o diretório e selecione **Remover**.  
  
**Arquivo de logs Tempdb** é o nome do arquivo de log. Esse arquivo é criado automaticamente. As configurações a seguir se aplicam apenas aos arquivos de dados **tempdb** :  
  
* **Tamanho inicial (MB)** é o tamanho inicial do arquivo de log **tempdb** . O valor padrão é 8 MB (ou 4 MB para [!INCLUDE[ssexpress](../../includes/ssexpress_md.md)]). [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] apresenta um tamanho do arquivo inicial máximo de 262.144 MB (256 GB). [!INCLUDE[sssql15](../../includes/sssql15-md.md)] tem um tamanho do arquivo inicial máximo de 1024 MB. Como o **tempdb** é recriado sempre que o SQL Server é iniciado ou passa por failover, especifique um tamanho próximo ao tamanho exigido por sua carga de trabalho para uma operação normal. Para otimizar ainda mais a criação de **tempdb** durante o início, habilite a [Inicialização instantânea de arquivo do banco de dados](../../relational-databases/databases/database-instant-file-initialization.md).  
  
  > [!NOTE]
  > **Tempdb** usa o registro em log mínimo. O arquivo de log do **tempdb** não pode passar por backup. Ele é recriado sempre que o SQL Server é iniciado ou quando uma instância de cluster passa por failover.

* **Expansão automática (MB)** é o incremento de expansão do log **tempdb** em megabytes.  O valor padrão de 64 MB cria o número ideal de arquivos de log virtuais durante a inicialização.  

  > [!NOTE]
  > Os arquivos de log **Tempdb** não usam a inicialização instantânea de arquivo.
  
* **Diretório de log** é o diretório no qual os arquivos de log **tempdb** são criados. Há apenas um diretório de log **tempdb**.  
  
### <a name="security-considerations"></a>Considerações de segurança
  
A instalação configura ACLs para diretórios do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e interrompe a herança como parte da configuração.  

As seguintes recomendações se aplicam ao servidor de arquivos SMB:  
  
* A conta de serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá ser uma conta de domínio se for usado um servidor de arquivos SMB.  
  
* A conta usada para instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] precisa ter permissões NTFS **Controle Total** na pasta de compartilhamento de arquivos SMB usada como o diretório de dados.  
  
* A conta usada para instalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ter privilégios SeSecurityPrivilege no servidor de arquivos SMB. Para conceder esse privilégio, use o console de Política de Segurança Local no servidor de arquivos para adicionar a conta de configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] à política **Gerenciar o log de auditoria e segurança**. Essa configuração está na seção **Atribuições de Direitos do Usuário**, em **Políticas Locais**, no console Política de Segurança Local.  
  
> [!NOTE]
> Se você especificar diretórios de instalação não padrão, verifique se as pastas de instalação são exclusivas para essa instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nenhum dos diretórios nesta caixa de diálogo deve ser compartilhado com diretórios de outras instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os componentes [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também devem ser instalados em diretórios separados.
  
### <a name="see-also"></a>Confira também

* [Configurar contas e permissões de serviço Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)
* [Permissões de compartilhamento e de NTFS em um servidor de arquivos](https://docs.microsoft.com/iis/web-hosting/configuring-servers-in-the-windows-web-platform/configuring-share-and-ntfs-permissions)  

<!--
The MaxDOP setting applies only to SQL Server 2019 and later.
-->

::: moniker range=">=sql-server-ver15"

## <a name="a-namemaxdop-database-engine-configuration---maxdop-page"></a><a name="maxdop"><a/> Página Configuração do Mecanismo de Banco de Dados – MaxDOP

O **MaxDOP (grau máximo de paralelismo)** determina o número máximo de processadores que uma única instrução pode utilizar. O [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] introduz a capacidade de configurar essa opção durante a instalação. O [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] também detecta automaticamente a configuração de MaxDOP recomendada para o servidor com base no número de núcleos.  

Se essa página for ignorada durante a instalação, o valor de MaxDOP padrão será o valor recomendado exibido nessa página, em vez do valor padrão [!INCLUDE[ssde_md](../../includes/ssde_md.md)] das versões anteriores (0). Você também pode definir manualmente essa configuração na página e modificar a configuração após a instalação. 

### <a name="ui-element-list"></a>Lista de elementos da interface do usuário

* O **MaxDOP (grau máximo de paralelismo)** é o valor do número máximo de processadores a ser usado durante uma execução paralela de uma única instrução. O valor padrão será alinhado às diretrizes de grau máximo da opção de paralelismo especificadas em [Configurar a opção de configuração de servidor grau máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md#Guidelines).

## <a name="a-namememory-database-engine-configuration---memory-page"></a><a name="memory"><a/> Página Configuração do Mecanismo de Banco de Dados – Memória

A **memória mínima do servidor** determina o menor limite de memória que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usará para o pool de buffers e outros caches. Tanto o valor padrão quanto o valor recomendado são 0. Para obter mais informações sobre os efeitos de **memória mínima do servidor**, confira o [Guia de arquitetura de gerenciamento de memória](../../relational-databases/memory-management-architecture-guide.md#effects-of-min-and-max-server-memory).

A **memória máxima do servidor** determina o limite máximo de memória que o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] usará para o pool de buffers e outros caches. O valor padrão é 2.147.483.647 MB (megabytes), e os valores recomendados calculados serão alinhados com as diretrizes especificadas em [Opções de configuração de memória do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md#manually) para uma instância autônoma de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], com base na memória do sistema existente. Para obter mais informações sobre os efeitos de **memória máxima do servidor**, confira o [Guia de arquitetura de gerenciamento de memória](../../relational-databases/memory-management-architecture-guide.md#effects-of-min-and-max-server-memory).

Se essa página for ignorada durante a instalação, o valor padrão de **memória máxima do servidor** usado será o valor padrão de [!INCLUDE[ssde_md](../../includes/ssde_md.md)] (2.147.483.647 megabytes). Você pode definir essas configurações manualmente nessa página depois de escolher o botão de opção **Recomendado** e pode modificá-las após a instalação. Para saber mais, veja [Opções de configuração de memória do servidor](../../database-engine/configure-windows/server-memory-server-configuration-options.md).

### <a name="ui-element-list"></a>Lista de elementos da interface do usuário
  
**Padrão**: esse botão de opção é selecionado por padrão e define as configurações **memória mínima do servidor** e **memória máxima do servidor** para os valores padrão de [!INCLUDE[ssde_md](../../includes/ssde_md.md)]. 

**Recomendado**: esse botão de opção precisa ser selecionado para aceitar os valores recomendados calculados ou a fim de alterar os valores calculados para valores configurados pelo usuário.  
  
**Memória Mínima do Servidor (MB)** : se estiver fazendo a alteração do valor recomendado calculado para um valor configurado pelo usuário, insira o valor de **memória mínima do servidor**.  
  
**Memória Máxima do Servidor**: se estiver fazendo a alteração do valor recomendado calculado para um valor configurado pelo usuário, insira o valor de **memória máxima do servidor**.  

**Clique aqui para aceitar as configurações de memória recomendadas para o Mecanismo de Banco de Dados do SQL Server**: marque esta caixa de seleção para aceitar as configurações de memória recomendadas calculadas neste servidor. Se o botão de opção **Recomendado** tiver sido selecionado, a instalação não poderá continuar sem que essa caixa de seleção esteja selecionada.

::: moniker-end

## <a name="database-engine-configuration---filestream-page"></a>Configuração do Mecanismo de Banco de Dados – página FILESTREAM

Use esta página para habilitar FILESTREAM para esta instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. O FILESTREAM integra o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] com um sistema de arquivos NTFS armazenando dados BLOB (objeto binário grande) **varbinary(max)** como arquivos no sistema de arquivos. [!INCLUDE[tsql](../../includes/tsql-md.md)] podem inserir, atualizar, consultar, pesquisar e fazer backup de dados FILESTREAM. As interfaces do sistema de arquivos do Microsoft Win32 fornecem acesso de streaming aos dados. 
  
### <a name="ui-element-list"></a>Lista de elementos da interface do usuário
  
**Habilitar FILESTREAM para acesso Transact-SQL**: Selecione para habilitar FILESTREAM para acesso [!INCLUDE[tsql](../../includes/tsql-md.md)] . Essa caixa de seleção precisa ser marcada antes que as outras opções estejam disponíveis.  
  
**Habilitar FILESTREAM para acesso de fluxo de E/S de arquivo**: Selecione para habilitar o acesso de fluxo Win32 para FILESTREAM.  
  
**Nome de compartilhamento do Windows**: Insira o nome do compartilhamento do Windows no qual os dados FILESTREAM serão armazenados.  
  
**Permitir que clientes remotos tenham acesso de streaming a dados FILESTREAM**: Marque essa caixa de seleção para permitir que clientes remotos acessem dados FILESTREAM neste servidor.  
  
### <a name="see-also"></a>Confira também

* [Habilitar e configurar o FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)
* [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  

## <a name="database-engine-configuration---user-instance-page"></a>Página Configuração do Mecanismo de Banco de Dados – instância de usuário

Use a página **Instância de Usuário** para:

* Gerar uma instância separada do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para usuários sem permissões de administrador.
* Adicionar usuários à função de administrador.  
  
### <a name="options"></a>Opções
  
**Habilitar instâncias de usuário**: O padrão é ligado. Para desativar a capacidade de habilitar instâncias de usuário, desmarque a caixa de seleção.  
  
A instância do usuário, também conhecida como instância filha ou cliente, é uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gerada pela instância pai (a instância primária executada como um serviço, como o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) em nome de um usuário. A instância de usuário é executada como um processo de usuário no contexto de segurança daquele usuário. A instância de usuário é isolada da instância pai e de qualquer outra instância de usuário que estiver em execução no computador. O recurso de instância de usuário também é chamado de RANU "run as normal user" (Executar como Usuário Normal).  
  
> [!NOTE]  
> Os logons provisionados como membros da função de servidor fixa **sysadmin** durante a Instalação são provisionados como administradores no banco de dados de modelo. Eles são membros da função de servidor fixa **sysadmin** na instância de usuário, a menos que sejam removidos.  
  
**Adicionar usuário à função de Administrador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** :  O padrão é desligado. Para adicionar o usuário de Instalação atual à função de Administrador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], marque a caixa de seleção.  
  
Os usuários do [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] que são membros de BUILTIN\Administradores não são adicionados automaticamente à função de servidor fixa **sysadmin** quando se conectam a [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Somente os usuários do [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] explicitamente adicionados a uma função de administrador de nível de servidor podem administrar o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Os membros do grupo Built-In\Usuários pode se conectar à instância do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], mas terá permissões limitadas para executar tarefas do banco de dados. Por esse motivo, os usuários cujos privilégios do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] sejam herdados de BUILTIN\Administradores e Built-In\Usuários das versões anteriores do Windows precisam receber explicitamente privilégios administrativos em instâncias do [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] executadas no [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)].  
  
Para fazer alterações nas funções de usuário depois do programa de instalação, use o [SQL Server Management Studio](../../relational-databases/security/authentication-access/join-a-role.md) ou o [Transact-SQL](../../t-sql/statements/alter-role-transact-sql.md).
