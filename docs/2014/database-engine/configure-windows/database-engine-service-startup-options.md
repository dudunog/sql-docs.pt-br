---
title: Opções de inicialização do serviço do Mecanismo de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- single-user mode [SQL Server], startup option
- overriding default startup options
- minimal configuration mode [SQL Server], startup option
- default startup options
- temporarily override default startup options [SQL Server]
- startup options [SQL Server]
- starting SQL Server, options
ms.assetid: d373298b-f6cf-458a-849d-7083ecb54ef5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 29984a52d711ef02c3c3b640ef8d59323806c2bd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62812278"
---
# <a name="database-engine-service-startup-options"></a>Opções de inicialização do serviço Mecanismo de Banco de Dados
  As opções de inicialização designam certos locais de arquivos necessários durante inicialização e especificam algumas condições que abrangem o servidor. A maioria dos usuários não precisa especificar opções de inicialização a menos que você esteja solucionando problemas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] ou tenha um problema incomum e é instruído a usar uma opção de inicialização pelo Suporte de Cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!WARNING]  
>  O uso impróprio de opções de inicialização pode afetar o desempenho do servidor e impedir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de iniciar.  
  
## <a name="about-startup-options"></a>Sobre as opções de inicialização  
 Quando você instala o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a Instalação grava um conjunto de opções de inicialização padrão no Registro do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Você pode usar essas opções de inicialização para especificar um arquivo de banco de dados  mestre alternado, mestre arquivo de log de banco de dados ou arquivo de log de erros. Se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não conseguir localizar os arquivos necessários, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não será iniciado.  
  
 As opções de inicialização podem ser definidas com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. Para obter informações, veja [Configurar opções de inicialização do servidor &#40;SQL Server Configuration Manager&#41;](scm-services-configure-server-startup-options.md).  
  
## <a name="list-of-startup-options"></a>Lista de opções de inicialização  
  
|Opções de inicialização padrão|Descrição|  
|-----------------------------|-----------------|  
|**-d**  *master_file_path*|O caminho totalmente qualificado para o arquivo de banco de dados mestre (geralmente, C:\Arquivos de Programas\Microsoft SQL Server\MSSQL.*n*\MSSQL\Data\master.mdf). Se você não fornecer essa opção, os parâmetros de registro existentes serão usados.|  
|**-e**  *error_log_path*|O caminho totalmente qualificado para o arquivo de log de erros (normalmente, C:\Arquivos de Programa\Microsoft SQL Server\MSSQL.*n*\MSSQL\LOG\ERRORLOG). Se você não fornecer essa opção, os parâmetros de registro existentes serão usados.|  
|**-l**  *master_log_path*|O caminho totalmente qualificado para o arquivo de log do banco de dados mestre (geralmente, C:\Arquivos de Programas\Microsoft SQL Server\MSSQL.*n*\MSSQL\Data\mastlog.ldf). Se você não especificar essa opção, serão usados os parâmetros de registro existentes.|  
  
|Outras opções de inicialização|Descrição|  
|---------------------------|-----------------|  
|**-c**|Reduz o tempo de inicialização ao iniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no prompt de comando. Normalmente, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] inicia como um serviço chamando o Gerenciador de Controle de Serviços. Como o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] não é iniciado como um serviço quando o prompt de comando é iniciado, use **-c** para ignorar esta etapa.|  
|**-f**|Inicia uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com configuração mínima. Isso será útil se a definição de um valor de configuração (por exemplo, sobrecarga de confirmação de memória) impediu o servidor de ser iniciado. Iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de configuração mínima coloca o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único. Para obter mais informações, veja a descrição de **-m** a seguir.|  
|**-g**  *memory_to_reserve*|Especifica um número inteiro de megabytes (MB) de memória que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deixará disponível para alocações de memória dentro do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mas fora do pool de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A memória fora do pool de memória é a área usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para carregar itens, como arquivos .dll de procedimento estendido, os provedores OLE DB referenciados por consultas distribuídas e objetos de automação referenciados em instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] . O padrão é 256 MB.<br /><br /> O uso desta opção pode ajudar a ajustar alocação de memória, mas só quando a memória física excede o limite configurado definido pelo sistema operacional em memória virtual disponível para aplicativos. O uso desta opção pode ser apropriado em configurações de memória grandes nas quais os requisitos de uso de memória de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são atípicos e o espaço de endereço virtual do processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está totalmente em uso. O uso incorreto dessa opção pode conduzir a condições nas quais uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode não ser iniciada ou encontrar erros em tempo de execução.<br /><br /> Use o padrão para o parâmetro **-g** , a menos que você veja algum dos seguintes avisos no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :<br /><br /> -"Falha de alocar bytes virtuais \<: FAIL_VIRTUAL_RESERVE tamanho>"<br /><br /> -"Falha de alocar bytes virtuais \<: FAIL_VIRTUAL_COMMIT tamanho>"<br /><br /> Essas mensagens podem indicar que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está tentando liberar partes do pool de memória do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para encontrar espaço para itens, como arquivos .dll de procedimento armazenado estendido ou objetos de automação. Nesse caso, considere aumentar a quantidade de memória reservada pela opção **-g** .<br /><br /> Usar um valor menor que o padrão aumentará a quantidade de memória disponível para o pool de memória gerenciado pelo Gerenciador de Memória do SQL Server e pilhas de thread; isso pode, por sua vez, oferecer algum benefício de desempenho a cargas de trabalho de uso intenso de memória em sistemas que não usam muitos procedimentos armazenados estendidos, consultas distribuídas ou objetos de automação.|  
|**-m**|Inicia uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em modo de usuário único. Quando você inicia uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em modo de usuário único, só um único usuário pode conectar e o processo de CHECKPOINT não é iniciado. CHECKPOINT garante que transações concluídas sejam gravadas regularmente do cache de disco para o dispositivo de banco de dados. (Normalmente, essa opção será usada se você perceber problemas com bancos de dados do sistema que devem ser corrigidos.) Habilita a opção sp_configure allow updates. Por padrão, a permissão de atualizações está desabilitada. Iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único permite que qualquer membro do grupo de Administradores locais do computador se conecte à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como um membro da função de servidor fixa sysadmin. Para obter mais informações, consulte [conectar-se a SQL Server quando os administradores do sistema estiverem bloqueados](connect-to-sql-server-when-system-administrators-are-locked-out.md). Para obter mais informações sobre o modo de usuário único, consulte [iniciar SQL Server no modo de usuário único](start-sql-server-in-single-user-mode.md).|  
|**-m "nome do aplicativo cliente"**|Limita as conexões a um aplicativo cliente especificado quando você usa a opção **-m** com a opção **SQLCMD** ou [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Por exemplo, **-m"SQLCMD"** limita as conexões a uma única conexão e essa conexão deve se identificar como o programa cliente **SQLCMD**. Use essa opção quando estiver iniciando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único e se um aplicativo cliente desconhecido estiver usando a única conexão disponível. Para se conectar por meio do Editor de Consultas no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], use **-m"Microsoft SQL Server Management Studio - Query"**.<br /><br /> O nome do aplicativo cliente diferencia maiúsculas de minúsculas.<br /><br /> Observação de ** \* segurança \* \* ** Não use essa opção como um recurso de segurança. O aplicativo cliente fornece o nome do aplicativo cliente e pode fornecer um nome falso como parte da cadeia de conexão.|  
|**-n**|Não usa o log de aplicativo do Windows para registrar eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você iniciar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com **-n**, recomendamos que você também use a opção de inicialização **-e** . Caso contrário, eventos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não são registrados no log.|  
|**-s**|Permite iniciar uma instância nomeada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sem o parâmetro **-s** definido, a instância padrão tentará iniciar. Você deve passar para o diretório BINN apropriado da instância em um prompt de comando antes de iniciar o **sqlservr.exe**. Por exemplo, se Instance1 tiver de usar \mssql$Instance1 para seus binários, o usuário deverá estar no diretório \mssql$Instance1\binn para iniciar **sqlservr.exe -s instance1**.|  
|**-T**  *trace #*|Indica que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser iniciada com um sinalizador de rastreamento especificado (*trace#*) em vigor. São usados sinalizadores de rastreamento para iniciar o servidor com comportamento fora do padrão. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).<br /><br /> ** \* Importante \* \* ** Ao especificar um sinalizador de rastreamento com a opção **-t** , use um "T" maiúsculo para passar o número do sinalizador de rastreamento. Um "t" minúsculo é aceito através de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas isso define outros sinalizadores de rastreamento internos que só são exigidos através de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] engenheiros de suporte. (Parâmetros especificados na janela de inicialização do Painel de Controle não são legíveis.)|  
|**-x**|Desabilita os seguintes recursos de monitoramento:<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Contadores de monitor de desempenho<br /><br /> Manutenção da hora da CPU e as estatísticas de taxa de acertos de cache<br /><br /> Coleta de informações para o comando DBCC SQLPERF<br /><br /> Coleta de informações por algumas exibições de gerenciamento dinâmico<br /><br /> Muitos pontos de evento dos eventos estendidos<br /><br /> <br /><br /> ** \* Aviso \* \* ** Quando você usa a opção **-x** Startup, as informações disponíveis para diagnosticar problemas de desempenho e funcionais com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o são muito reduzidas.|  
|**-E**|Aumenta o número de extensões alocadas para cada arquivo em um grupo de arquivos. Essa opção pode ser útil para aplicativos de data warehouse que têm um número limitado de usuários que estão executando exames de índices ou de dados. Ela não deve ser usada em outros aplicativos porque pode afetar o desempenho de maneira prejudicial. Essa opção não tem suporte no versões de 32 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="using-startup-options-for-troubleshooting"></a>Usando opções de inicialização para solucionar problemas  
 Algumas opções de inicialização, como o modo de usuário único e o modo de configuração mínima, são usados principalmente durante a solução de problemas. Iniciar o servidor para solução de problemas com as opções **-m** ou **-f** é mais fácil na linha de comando, enquanto inicia manualmente o sqlservr. exe.  
  
> [!NOTE]  
>  Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado usando o **net start**, as opções de inicialização usam uma barra (/) em vez de hífen (-).  
  
## <a name="using-startup-options-during-normal-operations"></a>Usando opções de inicialização durante operações normais  
 Você pode desejar usar algumas opções de inicialização sempre que iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essas opções, como **-g** ou a partir de um sinalizador de rastreamento, são feitas com mais facilidade com a configuração dos parâmetros [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de inicialização usando Configuration Manager. Essas ferramentas salvam as opções de inicialização como chaves do Registro, habilitando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para sempre ser iniciado com as opções de inicialização.  
  
## <a name="compatibility-support"></a>Suporte de compatibilidade  
 Não há suporte para o parâmetro **-h**  no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Este parâmetro foi usado em versões anteriores de instâncias de 32 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para reservar espaço de endereço de memória virtual para metadados de inclusão de memória a quente quando AWE é habilitado. Para obter mais informações, consulte [Recursos do SQL Server descontinuados no SQL Server 2014](../../getting-started/discontinued-sql-server-features-in-sql-server-2014.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 [Configurar a opção de configuração de servidor scan for startup procs](configure-the-scan-for-startup-procs-server-configuration-option.md)  
  
 [Iniciar, parar, pausar, retomar, reiniciar o mecanismo de banco de dados, o SQL Server Agent ou o serviço SQL Server Browser](start-stop-pause-resume-restart-sql-server-services.md)  
  
## <a name="see-also"></a>Consulte Também  
 [PONTO de verificação &#40;&#41;Transact-SQL](/sql/t-sql/language-elements/checkpoint-transact-sql)   
 [Aplicativo sqlservr](../../tools/sqlservr-application.md)  
  
  
