---
title: Opções de inicialização do serviço do Mecanismo de Banco de Dados | Microsoft Docs
ms.custom: ''
ms.date: 08/01/2019
ms.prod: sql
ms.prod_service: high-availability
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
- single-user mode [SQL Server], startup parameter
- overriding default startup parameters
- minimal configuration mode [SQL Server], startup parameter
- default startup parameters
- temporarily override default startup parameters [SQL Server]
- startup parameters [SQL Server]
- starting SQL Server, parameters
ms.assetid: d373298b-f6cf-458a-849d-7083ecb54ef5
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4518428d6dd583e5d9fe2a4da06f052b8b75da70
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75252867"
---
# <a name="database-engine-service-startup-options"></a>Opções de inicialização do serviço Mecanismo de Banco de Dados

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

As opções de inicialização designam certos locais de arquivos necessários durante inicialização e especificam algumas condições que abrangem o servidor. A maioria dos usuários não precisa especificar opções de inicialização a menos que você esteja solucionando problemas do [!INCLUDE[ssDE](../../includes/ssde-md.md)] ou tenha um problema incomum e é instruído a usar uma opção de inicialização pelo Suporte de Cliente do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!WARNING]  
>  O uso impróprio de opções de inicialização pode afetar o desempenho do servidor e impedir o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de iniciar.  
>
>  Inicie o SQL Server no Linux com o usuário “mssql” para evitar problemas futuros de inicialização. Exemplo: `sudo -u mssql /opt/mssql/bin/sqlservr [STARTUP OPTIONS]` 
  
## <a name="about-startup-options"></a>Sobre as opções de inicialização  
 Quando você instala o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a Instalação grava um conjunto de opções de inicialização padrão no Registro do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Você pode usar essas opções de inicialização para especificar um arquivo de banco de dados  mestre alternado, mestre arquivo de log de banco de dados ou arquivo de log de erros. Se o [!INCLUDE[ssDE](../../includes/ssde-md.md)] não conseguir localizar os arquivos necessários, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não será iniciado.  
  
 As opções de inicialização podem ser definidas com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. Para obter informações, veja [Configurar opções de inicialização do servidor &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md).  
  
## <a name="list-of-startup-options"></a>Lista de opções de inicialização  
### <a name="default-startup-options"></a>Opções de inicialização padrão  

|Opções|Descrição|  
|-----------------------------|-----------------|  
|**-d**  *master_file_path*|O caminho totalmente qualificado para o arquivo de banco de dados mestre (geralmente, C:\Arquivos de Programas\Microsoft SQL Server\MSSQL.*n*\MSSQL\Data\master.mdf). Se você não fornecer essa opção, os parâmetros de registro existentes serão usados.|  
|**-e**  *error_log_path*|O caminho totalmente qualificado para o arquivo de log de erros (normalmente, C:\Arquivos de Programa\Microsoft SQL Server\MSSQL.*n*\MSSQL\LOG\ERRORLOG). Se você não fornecer essa opção, os parâmetros de registro existentes serão usados.|  
|**-l**  *master_log_path*|O caminho totalmente qualificado para o arquivo de log do banco de dados mestre (geralmente, C:\Arquivos de Programas\Microsoft SQL Server\MSSQL.*n*\MSSQL\Data\mastlog.ldf). Se você não especificar essa opção, serão usados os parâmetros de registro existentes.|  
  
### <a name="other-startup-options"></a>Outras opções de inicialização   

|Opções |Descrição|   
|---------------------------|-----------------|  
|**-c**|Reduz o tempo de inicialização ao iniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no prompt de comando. Normalmente, o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] inicia como um serviço chamando o Gerenciador de Controle de Serviços. Como o [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] não é iniciado como um serviço quando o prompt de comando é iniciado, use **-c** para ignorar esta etapa.|  
|**-f**|Inicia uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com configuração mínima. Isso será útil se a definição de um valor de configuração (por exemplo, sobrecarga de confirmação de memória) impediu o servidor de ser iniciado. Iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de configuração mínima coloca o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único. Para obter mais informações, veja a descrição de **-m** a seguir.|  
|**-kDecimalNumber**| Esse parâmetro de inicialização limita o número de solicitações de E/S de ponto de verificação por segundo, em que **DecimalNumber** representa a velocidade do ponto de verificação em MB por segundo.  Alterar esse valor pode afetar a velocidade de fazer backups ou passar pelo processo de recuperação; portanto, continue com cuidado. Para saber mais sobre esse parâmetro de inicialização, confira o hot fix em que o [parâmetro -k](https://support.microsoft.com/help/929240/fix-i-o-requests-that-are-generated-by-the-checkpoint-process-may-caus) foi introduzido.| 
|**-m**|Inicia uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em modo de usuário único. Quando você inicia uma instância de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em modo de usuário único, só um único usuário pode conectar e o processo de CHECKPOINT não é iniciado. CHECKPOINT garante que transações concluídas sejam gravadas regularmente do cache de disco para o dispositivo de banco de dados. (Normalmente, essa opção será usada se você perceber problemas com bancos de dados do sistema que devem ser corrigidos.) Habilita a opção sp_configure allow updates. Por padrão, a permissão de atualizações está desabilitada. Iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único permite que qualquer membro do grupo de Administradores locais do computador se conecte à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como um membro da função de servidor fixa sysadmin. Para obter mais informações, veja [Conectar-se ao SQL Server quando os administradores do sistema estão bloqueados](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md). Para obter mais informações sobre o modo de usuário único, veja [Iniciar o SQL Server no modo de usuário único](../../database-engine/configure-windows/start-sql-server-in-single-user-mode.md).|  
|**Nome do Aplicativo -mClient**|Limita as conexões a um aplicativo cliente especificado. Por exemplo, `-mSQLCMD`  limita conexões a uma única conexão, e essa conexão deve se identificar como o programa cliente SQLCMD. Use essa opção quando estiver iniciando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no modo de usuário único e se um aplicativo cliente desconhecido estiver usando a única conexão disponível. Use `"Microsoft SQL Server Management Studio - Query"` para se conectar com o Editor de Consultas do SSMS. A opção Editor de Consultas do SSMS não pode ser configurada com o [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] Configuration Manager, pois ele inclui o caractere traço, que é rejeitado pela ferramenta.<br /><br /> O nome do aplicativo cliente diferencia maiúsculas de minúsculas. Serão necessárias aspas duplas se o nome do aplicativo contiver espaços ou caracteres especiais.<br /><br />**Exemplos ao iniciar na linha de comando:**<br /><br />`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\sqlservr -s MSSQLSERVER -m"Microsoft SQL Server Management Studio - Query"` <br /><br />`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Binn\sqlservr -s MSSQLSERVER -mSQLCMD` <br /><br /> **Observação de segurança:** Não use essa opção como um recurso de segurança. O aplicativo cliente fornece o nome do aplicativo cliente e pode fornecer um nome falso como parte da cadeia de conexão.|  
|**-n**|Não usa o log de aplicativo do Windows para registrar eventos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se você iniciar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com **-n**, recomendamos que você também use a opção de inicialização **-e** . Caso contrário, eventos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não são registrados no log.|  
|**-s**|Permite iniciar uma instância nomeada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sem o parâmetro **-s** definido, a instância padrão tentará iniciar. Você deve passar para o diretório BINN apropriado da instância em um prompt de comando antes de iniciar o **sqlservr.exe**. Por exemplo, se Instance1 tiver de usar `\mssql$Instance1` para seus binários, o usuário deverá estar no diretório `\mssql$Instance1\binn` para iniciar **sqlservr.exe -s instance1**.|  
|**-T**  *trace#*|Indica que uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser iniciada com um sinalizador de rastreamento especificado (*trace#* ) em vigor. São usados sinalizadores de rastreamento para iniciar o servidor com comportamento fora do padrão. Para obter mais informações, veja, [Sinalizadores de rastreamento &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md).<br /><br /> **Importante:** Ao especificar um sinalizador de rastreamento com a opção **-T**, use um "T" maiúsculo para passar o número do sinalizador de rastreamento. Um "t" minúsculo é aceito através de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas isso define outros sinalizadores de rastreamento internos que só são exigidos através de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] engenheiros de suporte. (Parâmetros especificados na janela de inicialização do Painel de Controle não são legíveis.)|  
|**-x**|Desabilita os seguintes recursos de monitoramento:<br /> - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contadores de monitoramento de desempenho<br /> - Manutenção da hora da CPU e as estatísticas de taxa de acertos de cache<br /> - Coleta de informações para o comando DBCC SQLPERF<br /> - Coleta de informações por algumas exibições de gerenciamento dinâmico<br /> - Muitos pontos de evento dos eventos estendidos<br /><br /> **Aviso:** Quando você usa a opção de inicialização **-x**, as informações disponíveis para diagnosticar problemas de desempenho e funcionais com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são bastante reduzidas.|  
|**-E**|Aumenta o número de extensões alocadas para cada arquivo em um grupo de arquivos. Essa opção pode ser útil para aplicativos de data warehouse que têm um número limitado de usuários que estão executando exames de índices ou de dados. Ela não deve ser usada em outros aplicativos porque pode afetar o desempenho de maneira prejudicial. Essa opção não tem suporte no versões de 32 bits do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
## <a name="using-startup-options-for-troubleshooting"></a>Usando opções de inicialização para solucionar problemas  
 Algumas opções de inicialização, como o modo de usuário único e o modo de configuração mínima, são usados principalmente durante a solução de problemas. Iniciar o servidor para solucionar problemas com as opções **-m** ou **-f** é mais fácil na linha de comando, enquanto o sqlservr.exe é iniciado manualmente.  
  
> [!NOTE]  
>  Quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado usando o **net start**, as opções de inicialização usam uma barra (/) em vez de hífen (-).  
  
## <a name="using-startup-options-during-normal-operations"></a>Usando opções de inicialização durante operações normais  
 Você pode desejar usar algumas opções de inicialização sempre que iniciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essas opções, como inicialização com um sinalizador de rastreamento, são mais fáceis com a configuração dos parâmetros de inicialização usando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager. Essas ferramentas salvam as opções de inicialização como chaves do Registro, habilitando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para sempre ser iniciado com as opções de inicialização.  
  
## <a name="compatibility-support"></a>Suporte de compatibilidade  

Para ver opções que foram removidas de versões anteriores, confira [Aplicativo sqlservr](../../tools/sqlservr-application.md#compatibility-support).

## <a name="related-tasks"></a>Related Tasks  
[Configurar a opção de configuração do servidor scan for startup procs](../../database-engine/configure-windows/configure-the-scan-for-startup-procs-server-configuration-option.md)  
[Iniciar, parar, pausar, retomar, reiniciar o Mecanismo de Banco de Dados, o SQL Server Agent ou o serviço SQL Server Browser](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)
[Configurar opções de inicialização do servidor &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/scm-services-configure-server-startup-options.md)
  
## <a name="see-also"></a>Consulte Também  
 [CHECKPOINT &#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)   
 [Aplicativo sqlservr](../../tools/sqlservr-application.md)  
  
  
