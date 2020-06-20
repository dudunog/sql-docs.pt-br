---
title: Fazer upgrade do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, upgrading
- SSIS, upgrading
- SQL Server Integration Services, upgrading
- upgrading Integration Services
ms.assetid: 04f9863c-ba0b-47c5-af91-f2d41b078a23
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: ab63f0d12b4cd5d76fcb6e3419f5d1f1ed7232d6
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968346"
---
# <a name="upgrade-integration-services"></a>Atualização do Integration Services
  Se o [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] ou o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] estiver atualmente instalado no computador, você poderá atualizar para o [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)].  
  
 Quando você atualiza o [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] em um computador que tem uma dessas versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] instalada, [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] é instalado lado a lado com a versão anterior.  
  
 Com essa instalação lado a lado, várias versões do utilitário dtexec são instaladas. Para garantir que você execute a versão correta do utilitário, no prompt de comando, execute o utilitário digitando o caminho completo ( \<drive> : \Program Files\Microsoft SQL Server \\<versão \> \DTS\Binn). Para obter mais informações sobre dtexec, consulte [dtexec Utility](../packages/dtexec-utility.md).  
  
> [!NOTE]  
>  Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], por padrão, quando você instalava o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , todos os usuários no grupo Usuários tinham acesso ao serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Quando você instala o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], os usuários não têm acesso ao serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Por padrão, o serviço é protegido. Após a instalação do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , o administrador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deverá executar a ferramenta de Configuração DCOM (Dcomcnfg.exe) para conceder a usuários específicos acesso ao serviço do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter mais informações, consulte [Grant Permissions to Integration Services Service](../grant-permissions-to-integration-services-service.md).  
  
## <a name="before-upgrading-integration-services"></a>Antes de atualizar o Integration Services  
 Recomenda-se executar o Supervisor de Atualização antes de atualizar para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. O Supervisor de Atualização reporta problemas que você poderá encontrar se migrar pacotes existentes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para o novo formato de pacote utilizado pelo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Para obter mais informações, consulte [Use Upgrade Advisor to Prepare for Upgrades](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
> [!NOTE]
>  O suporte para migrar ou executar pacotes DTS (Data Transformation Services) foi descontinuado na versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . A seguinte funcionalidade do DTS foi descontinuada:  
> 
>  -   runtime DTS  
> -   API DTS  
> -   O Assistente de Migração de Pacotes para migração de pacotes DTS para a próxima versão do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
> -   Suporte para manutenção de pacote DTS no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
> -   Tarefa Executar Pacote DTS 2000  
> -   Exame de pacotes DTS do Supervisor de Atualização  
> 
>  Para obter informações sobre outros recursos descontinuados, consulte [Integration Services funcionalidade descontinuada no SQL Server 2014](../discontinued-integration-services-functionality-in-sql-server-2014.md).  
  
## <a name="upgrading-integration-services"></a>atualizando o Integration Services  
 Você pode fazer a atualização usando um dos seguintes métodos:  
  
-   Execute a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instalação e selecione a opção para **atualizar de SQL Server 2005, SQL Server 2008 ou SQL Server 2008 R2**ou **[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]** .  
  
-   Execute **setup.exe** no prompt de comando e especifique a `/ACTION=upgrade` opção. Para obter mais informações, consulte a seção "scripts de instalação para [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] " em [instalar SQL Server 2014 no prompt de comando](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
 Você não pode usar a atualização para executar as seguintes ações:  
  
-   Reconfigurar uma instalação existente do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   Mover de uma versão de 32 bits para uma versão de 64 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou de uma versão de 64 bits para uma versão de 32 bits.  
  
-   Mover de uma versão localizada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para outra versão localizada.  
  
 Quando atualizar, você poderá atualizar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e o [!INCLUDE[ssDE](../../includes/ssde-md.md)], ou apenas o [!INCLUDE[ssDE](../../includes/ssde-md.md)]ou somente o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Se você atualizar somente o [!INCLUDE[ssDE](../../includes/ssde-md.md)], o [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] ou o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] continuará funcionando, mas você não terá a funcionalidade do [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]. Se você atualizar apenas o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], o [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] funcionará por completo, mas poderá apenas armazenar pacotes no sistema de arquivos, a não ser que a instância do [!INCLUDE[ssDECurrent](../../includes/ssdecurrent-md.md)] esteja disponível em outro computador.  
  
## <a name="upgrading-both-integration-services-and-the-database-engine-to-sscurrent"></a>Atualizando o Integration Services e o Mecanismo de Banco de Dados para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 Esta seção descreve os efeitos da execução de uma atualização que tem os seguintes critérios:  
  
-   Você atualiza o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   O [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] estão no mesmo computador.  
  
### <a name="what-the-upgrade-process-does"></a>O que o processo de atualização faz  
 O processo de atualização realiza as seguintes tarefas:  
  
-   Instala os arquivos, o serviço e as ferramentas do [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] ([!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]). Quando há várias instâncias do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] no mesmo computador, na primeira vez que você atualiza uma das instâncias para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], os arquivos, serviços e ferramentas do [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] são instalados.  
  
-   Atualiza a instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] para a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versão.  
  
-   Move os dados das [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] tabelas do sistema ou para as [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] tabelas do sistema, da seguinte maneira:  
  
    -   Move pacotes sem alteração da tabela do sistema msdb.dbo.sysdtspackages90 para a tabela do sistema msdb.dbo.sysssispackages.  
  
        > [!NOTE]  
        >  Embora os dados sejam movidos para uma tabela do sistema diferente, o processo de atualização não migra pacotes para o novo formato.  
  
    -   Move metadados de pasta da tabela do sistema msdb.sysdtsfolders90 para a tabela do sistema msdb.sysssisfolders.  
  
    -   Move dados de log da tabela do sistema msdb.sysdtslog90 para a tabela do sistema msdb.sysssislog.  
  
-   Remove as tabelas do sistema msdb.sysdts*90 e os procedimentos armazenados usados para acessá-las depois de mover os dados para as novas tabelas msdb.sysssis\* . No entanto, a atualização substitui a tabela sysdtslog90 por uma exibição também denominada sysdtslog90. Essa nova exibição sysdtslog90 expõe a nova tabela de sistema msdb.sysssislog. Isso assegura que os relatórios com base na tabela de log continuem a ser executados sem interrupção.  
  
-   Para controlar o acesso aos pacotes, cria três novas funções fixas de nível de banco de dados: db_ssisadmin, db_ssisltduser e db_ssisoperator. As funções db_dtsadmin, db_dtsltduser e db_dtsoperator do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] não foram removidas, mas se tornaram membros das novas funções correspondentes.  
  
-   Se o [!INCLUDE[ssIS](../../includes/ssis-md.md)] repositório de pacotes (ou seja, o local do sistema de arquivos gerenciado pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] serviço) for o local padrão em **\sql Server\90**, **\sql Server\100**ou **\sql Server\110** moverá esses pacotes para o novo local padrão em **\sql Server\120**.  
  
-   Atualiza o arquivo de configuração do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para apontar para a instância atualizada do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
### <a name="what-the-upgrade-process-does-not-do"></a>O que o processo de atualização não faz  
 O processo de atualização não faz as seguintes tarefas:  
  
-   **Não remove o** [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] serviço ou [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] .  
  
-   Não migra os pacotes existentes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para o novo formato de pacote usado pelo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Para obter informações sobre como migrar pacotes, veja [Atualizar pacotes do Integration Services](upgrade-integration-services-packages.md).  
  
-   Não move pacotes de locais do sistema de arquivos, sem ser o local padrão, que foram adicionados ao arquivo de configuração do serviço. Caso você tenha editado anteriormente o arquivo de configuração do serviço para adicionar mais pastas do sistema de arquivos, os pacotes armazenados nesses campos não serão movidos para um novo local.  
  
-   No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, as etapas de trabalho que chamam o utilitário **dtexec** (dtexec.exe) diretamente não atualizam o caminho do sistema de arquivos do utilitário **dtexec** . É necessário editar essas etapas de trabalho manualmente para atualizar o caminho do sistema de arquivos para especificar o local do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para o utilitário **dtexec** .  
  
### <a name="what-you-can-do-after-upgrading"></a>O que você pode fazer depois da atualização  
 Após a conclusão do processo de atualização você poderá realizar as seguintes tarefas:  
  
-   Executar trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que executam pacotes.  
  
-   Use [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o para gerenciar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacotes armazenados em uma instância do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ou do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . É preciso modificar o arquivo de configuração do serviço para adicionar a instância do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] à lista de locais gerenciados pelo serviço.  
  
    > [!NOTE]  
    >  As versões anteriores do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] não podem se conectar ao serviço do [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] .  
  
-   Identificar a versão dos pacotes na tabela do sistema msdb.dbo.sysssispackages verificando o valor na coluna packageformat. A tabela tem uma coluna packageformat que identifica a versão de cada pacote. Um valor de 2 na coluna packageformat indica um pacote do [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]; um valor de 3 indica um pacote do [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]. Até você migrar os pacotes para o novo formato de pacote, o valor na coluna packageformat não se altera.  
  
-   Você não pode usar [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] as [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ferramentas ou para criar, executar ou gerenciar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacotes. As ferramentas do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] incluem as respectivas versões do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e o Utilitário de Execução de Pacotes (dtexecui.exe). O processo de atualização não remove as [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ferramentas ou. No entanto, você não poderá usar essas ferramentas para continuar trabalhando com os pacotes do [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] ou [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] em um servidor que foi atualizado.  
  
-   Por padrão, em uma instalação de atualização, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] está configurado para registrar eventos relacionados à execução dos pacotes para o log de eventos do Aplicativo. Essa configuração pode gerar muitas entradas de log de evento quando você usar o recurso Coletor de Dados do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Os eventos que são registrados incluem EventID 12288, "Pacote iniciado" e EventID 12289, "Pacote concluído com êxito". Para parar o registro desses dois eventos para o log de eventos do Aplicativo, abra o Registro para edição. No Registro, localize o nó HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS e altere o valor de DWORD da configuração LogPackageExecutionToEventLog de 1 para 0.  
  
## <a name="upgrading-only-the-database-engine-to-sscurrent"></a>Atualizando somente o Mecanismo de Banco de Dados para o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 Esta seção descreve os efeitos da execução de uma atualização que tem os seguintes critérios:  
  
-   Você atualiza somente uma instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Isto é, a instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] agora é uma instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], mas a instância do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e as ferramentas de cliente são do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
-   A instância do [!INCLUDE[ssDE](../../includes/ssde-md.md)] está em um computador e o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e as ferramentas de cliente estão em outro.  
  
### <a name="what-you-can-do-after-upgrading"></a>O que você pode fazer depois da atualização  
 As tabelas do sistema que armazenam pacotes na instância atualizada do [!INCLUDE[ssDE](../../includes/ssde-md.md)] não são as mesmas que as usadas no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Portanto, as [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] versões ou do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e do [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] não podem descobrir os pacotes nas tabelas do sistema na instância atualizada do [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Como esses pacotes não podem ser descobertos, há limitações sobre o que você pode fazer com esses pacotes:  
  
-   Você não pode usar as ferramentas do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], em outros computadores para carregar ou gerenciar pacotes da instância atualizada do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
    > [!NOTE]  
    >  Embora os pacotes na instância atualizada do [!INCLUDE[ssDE](../../includes/ssde-md.md)] ainda não tenham sido migrados para o novo formato de pacote, não é possível descobri-los com as ferramentas do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Portanto, os pacotes não podem ser usados pelas ferramentas do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
-   Você não pode usar o [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] ou [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] em outros computadores para executar pacotes armazenados no msdb na instância atualizada do [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
-   Não é possível usar trabalhos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent em computadores com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] para executar pacotes do [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] ou [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] armazenados na instância atualizada do [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="external-resources"></a>Recursos externos  
 Entrada de blog, [Fazendo com que aplicativos e extensões de SSIS personalizados existentes funcionem no Denali](https://go.microsoft.com/fwlink/?LinkId=238157), em blogs.msdn.com.  
  
  
