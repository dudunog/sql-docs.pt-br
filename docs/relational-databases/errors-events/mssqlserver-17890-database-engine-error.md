---
description: MSSQLSERVER_17890
title: MSSQLSERVER_17890
ms.custom: ''
ms.date: 12/25/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17890 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 6a854486d1867e84bcd9b13cb148d3026a41d51f
ms.sourcegitcommit: d819173fb91af6f20ca6ee59686c35c71b060fbc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/28/2020
ms.locfileid: "97797750"
---
# <a name="mssqlserver_17890"></a>MSSQLSERVER_17890
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|17890|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|SRV_WS_TRIMMED|
|Texto da mensagem|Uma parte significativa da memória de processo do SQL Server foi transferida para o arquivo de paginação. Isso pode resultar em degradação do desempenho. Duração: %d segundos. Conjunto de trabalho (KB): %I64d, confirmado (KB): %I64d, utilização da memória: %d%%.|
||

## <a name="explanation"></a>Explicação

Você poderá receber a mensagem de erro a seguir no log de erros [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou no Log de Eventos do Aplicativo do Windows.

> Uma parte significativa da memória de processo do SQL Server foi transferida para o arquivo de paginação. Isso pode resultar em degradação do desempenho. Duração: 0 segundo. Conjunto de trabalho (KB): 3383250, confirmado (KB): 9112480, utilização da memória: 37%.

Você também poderá observar uma degradação repentina do desempenho com a execução da consulta e todas as outras operações do SQL Server.

## <a name="cause"></a>Causa

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] monitora as informações relacionadas às várias memórias sobre o processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nesse caso, ele detectou que o conjunto de trabalho do processo é inferior a 50% da memória do processo confirmada. Como resultado, esse aviso é impresso. As causas normais desse aviso são:

- O sistema operacional transfere grandes partes da memória confirmada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o arquivo de paginação.
- Isso pode ser devido a uma demanda repentinamente maior de memória de outros aplicativos ou devido às necessidades do sistema operacional.
- Isso também pode ocorrer quando alguns drivers de dispositivo solicitam alocações de memória contígua para as necessidades deles.

## <a name="user-action"></a>Ação do usuário

Você pode impedir que o sistema operacional Windows pagine a memória do pool de buffers do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bloqueando a memória alocada ao pool de buffers na memória física. Bloqueie a memória atribuindo o direito de usuário Bloquear páginas na memória à conta de usuário usada como a conta de inicialização do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Porém, antes de implementar essa solução, examine as seções [O que causa a paginação da memória do SQL Server](#what-causes-sql-server-memory-to-be-paged-out) e Considerações importantes antes de atribuir o direito de usuário "Bloquear páginas na memória" a uma instância do SQL Server

> [!NOTE]
> O uso do direito Bloquear Páginas na Memória garante que a memória gerenciada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não seja paginada. No entanto, as pilhas de threads, as imagens EXE e DLL, a memória de heap, a memória do CLR ainda podem ser paginadas pelo sistema operacional.
>
> Do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 SP1 atualização cumulativa 2 em diante, as edições Standard e Enterprise do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podem usar o direito de usuário Bloquear páginas na memória. Para obter mais informações sobre o suporte a páginas bloqueadas, veja [KB970070 – Suporte para páginas bloqueadas em sistemas com o SQL Server Standard Edition (64 bits)](https://support.microsoft.com/help/970070).

Para atribuir o direito de usuário Bloquear páginas na memória, siga estas etapas:

1. Clique em **Iniciar**, em **Executar**, digite *gpedit.msc* e clique em **OK**.
1. Observe que a caixa de diálogo Política de Grupo é exibida.
1. Expanda **Configuração do Computador** e **Configurações do Windows**.
1. Expanda **Configurações de Segurança** e então expanda **Políticas Locais**.
1. Clique em Atribuição de Direitos de Usuário e clique duas vezes em **Bloquear páginas** na memória.
1. Na caixa de diálogo **Configuração de Política de Segurança Local**, clique em **Adicionar Usuário** ou **Grupo**.
1. Na caixa de diálogo **Selecionar Usuários** ou **Grupos**, adicione a conta que tem permissão para executar o arquivo Sqlservr.exe e clique em **OK**.
1. Feche a caixa de diálogo **Política de Grupo**.
1. Reinicie o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

Depois que você atribuir o direito de usuário Bloquear páginas na memória e reiniciar o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o sistema operacional Windows deixará de transferir a memória do pool de buffers para o arquivo de paginação dentro do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No entanto, o sistema operacional Windows ainda poderá transferir a memória do pool sem buffer dentro do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um arquivo de paginação.

Você pode validar se o direito de usuário é usado pela instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verificando se a seguinte mensagem é gravada no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na inicialização: "Usando páginas bloqueadas para o pool de buffers"

Essa mensagem só se aplica ao SQL Server. Para obter mais informações sobre essa mensagem no ERRORLOG, acesse o seguinte: [É necessário atribuir o privilégio Bloquear páginas para Memória no Sistema Local?](https://techcommunity.microsoft.com/t5/sql-server-support/do-i-have-to-assign-the-lock-pages-in-memory-privilege-for-local/ba-p/315426)

Quando o sistema operacional Windows transferir a memória do pool sem buffer para o arquivo de paginação, você ainda poderá enfrentar problemas de desempenho. No entanto, as mensagens de erro mencionadas na seção "Explicação" não são registradas no log de erros do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

## <a name="what-causes-sql-server-memory-to-be-paged-out"></a>O que causa a paginação da memória do SQL Server

Há três categorias amplas de problemas que podem causar isso:

- Problemas relacionados ao aplicativo: todos os aplicativos juntos esgotaram a memória física disponível, e o sistema operacional precisa liberar um pouco de memória para novas solicitações de aplicativos para recursos. Normalmente, a abordagem aqui é encontrar quais aplicativos estão esgotando a memória e tomar as medidas necessárias para balancear a memória entre eles sem causar o esgotamento de RAM.
- Problemas de driver de dispositivo: os drivers do dispositivo podem causar a paginação do conjunto de trabalho de todos os processos se o driver chama uma função de alocação de memória incorretamente.
- Problemas do sistema operacional

Abaixo, você poderá encontrar informações sobre cada uma dessas categorias

- **Problemas relacionados ao aplicativo**: os aplicativos juntos podem consumir toda a RAM do sistema. Se forem feitas novas solicitações de memória, o sistema operacional tentará atender a elas e, se não houver memória livre, ele removerá o conjunto de trabalho de aplicativos em execução para atender às solicitações de memória. Nesses casos, você poderá observar uma queda significativa no conjunto de trabalho, para a maioria, se não todos os aplicativos. Para observar isso, colete o seguinte contador do Monitor de Desempenho de todos os aplicativos no sistema:

  - Objeto de desempenho: Processo
  - Contador: Conjunto de Trabalho
  
  Além disso, monitore o contador a seguir para correlacionar a quantidade de memória física disponível no sistema.
  
  - Objeto de desempenho: Memória
  - Contador: Memória disponível (MB)
  
  O comportamento típico que você poderá observar é a redução da Memória disponível para próximo a 0 MB e uma queda repentina dos contadores do Conjunto de Trabalho para a maioria dos processos (todos) no sistema. Se você observar esse comportamento, poderá precisar tomar medidas para reduzir o uso de memória no sistema, o que inclui, por exemplo, a redução da Memória Máxima do Servidor para o SQL Server.
  
    Os aplicativos também poderão usar o cache do sistema em excesso e poderão causar um grande crescimento do cache do sistema. Para responder ao crescimento do cache do sistema, o sistema transfere o conjunto de trabalho para o arquivo de paginação do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou de outros aplicativos. Se você tiver esse problema, use algumas funções de gerenciamento de memória no aplicativo. Essas funções controlam o espaço de cache do sistema que as operações de E/S de arquivo podem usar no aplicativo. Por exemplo, você pode usar as funções SetSystemFileCacheSize e GetSystemFileCacheSize para controlar o espaço de cache do sistema que as operações de E/S de arquivo podem usar.
  
    Você pode usar o objeto Desempenho de memória para ver os valores de vários contadores nesse objeto a fim de determinar se o conjunto de trabalho do cache do sistema usa muita memória. Por exemplo, você pode ver os contadores Bytes de Cache e Bytes Residentes de Cache do Sistema. Para obter mais informações sobre esse tópico, confira:
  
    - [Excesso de cache](/archive/blogs/ntdebugging/too-much-cache)
    - [Serviço de Cache Dinâmico do Microsoft Windows](/archive/blogs/ntdebugging/microsoft-windows-dynamic-cache-service)
    - [Você enfrenta problemas de desempenho em aplicativos e serviços quando o cache de arquivos do sistema consome a maior parte da RAM física](https://support.microsoft.com/help/976618)
  
    Baixe e implante o "Serviço de Cache Dinâmico do Microsoft Windows" para controlar a memória consumida pelo cache do sistema.

- **Problemas de driver de dispositivo**: se um driver de dispositivo usar a função `MmAllocateContiguousMemory` e se ele definir o valor do parâmetro HighestAcceptableAddress como inferior a 4 GB (gigabytes), o sistema operacional Windows poderá transferir para um arquivo de paginação o conjunto de trabalho dos processos no sistema, incluindo o processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para resolver esse problema, entre em contato com o fornecedor do driver de dispositivo para obter atualizações de driver.

    Quando um driver de dispositivo tenta alocar a memória, o sistema operacional Windows pode transferir o conjunto de trabalho de outros aplicativos para um arquivo de paginação. Esse hotfix do Windows permite que você use o rastreamento de eventos para localizar o driver de dispositivo que está causando o problema. Para obter mais informações sobre o driver específico que está causando o comportamento de remoção do conjunto de trabalho, confira [Como identificar os drivers que alocam a memória contígua](/previous-versions/windows/desktop/xperf/identifying-drivers-that-allocate-contiguous-memory).

- **Problemas do sistema operacional**: para resolver os problemas conhecidos que fazem com que o sistema operacional Windows transfira o conjunto de trabalho do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para um arquivo de paginação, aplique os hotfixes descritos nos artigos da base de dados de conhecimento da Microsoft a seguir.

  > [!NOTE]
  > Os hotfixes são cumulativos. Uma versão mais recente de um hotfix contém as versões anteriores dele.

  - O conjunto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] poderá ser removido quando o sistema estiver usando alguns recursos avançados de TCP. Para obter mais informações, confira [Como solucionar problemas de recursos avançados de desempenho de rede, como RSS e NetDMA](/troubleshoot/windows-server/networking/troubleshoot-network-performance-features-rss-netdma).

  - Se você estiver executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Windows Server 2008, precisará aplicar correções para problemas conhecidos que podem resultar na remoção do conjunto de trabalho ou no consumo de memória excessivo desnecessário por outros componentes do sistema operacional. Para obter mais informações, examine os artigos a seguir [O processo de geração de relatório pode parar de responder quando você executa o Perfmon.exe com o modelo de Diagnóstico do Active Directory para gerar um relatório em um controlador de domínio baseado no Windows Server 2008](/troubleshoot/windows-server/performance/report-generation-process-stops-responding).

  - Se você estiver executando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Windows Server 2008 R2, precisará aplicar correções para problemas conhecidos que podem resultar na remoção do conjunto de trabalho. Para obter mais informações, examine os seguintes artigos:

    - [Um computador que executa o Windows 7 ou o Windows Server 2008 R2 deixa de responder quando você executa um aplicativo grande](https://support.microsoft.com/help/979149)
    - [O desempenho insatisfatório ocorre em um computador com processadores baseados em NUMA e que executa o Windows Server 2008 R2 ou o Windows 7 se um thread solicita muita memória que esteja dentro dos primeiros 4 GB de memória](https://support.microsoft.com/help/2155311)
    - [O computador tem um desempenho insatisfatório intermitente ou para de responder quando o driver Storport é usado no Windows Server 2008 R2](https://support.microsoft.com/help/2468345)

## <a name="important-considerations-before-you-assign-the-lock-pages-in-memory-user-right"></a>Considerações importantes antes de atribuir o direito de usuário "Bloquear páginas na memória"

Você deve fazer considerações adicionais antes de atribuir o direito de usuário Bloquear páginas na memória. Se você atribuir esse direito de usuário em sistemas que estão configurados incorretamente, o sistema poderá ficar instável ou experimentar uma diminuição de desempenho no sistema inteiro. Além disso, a ID de evento 333 poderá ser registrada no log de eventos.

Se você entrar em contato com o CSS (Serviço de Suporte ao Cliente) da Microsoft para resolver esses problemas, os engenheiros de CSS poderão solicitar a você que revogue esse direito de usuário na conta de usuário usada como a conta de inicialização do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Essa etapa poderá ser necessária para coletar dados de desempenho importantes que os engenheiros de CSS poderão usar para a configuração necessária das várias opções do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e de outros aplicativos em execução no sistema. Depois que os engenheiros de CSS coletam os dados de desempenho, você pode atribuir o direito de usuário Bloquear páginas na memória à conta de inicialização do serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Antes de atribuir o direito de usuário Bloquear páginas na memória, capture um log do Monitor de Desempenho para determinar os requisitos de memória de vários aplicativos e serviços instalados no sistema. Esses aplicativos também incluem o SQL Server. Para determinar os requisitos de memória, colete as seguintes informações de linha de base:

- Verifique se você definiu as opções max server memory e min server memory corretamente. Essas opções refletem apenas o requisito de memória do pool de buffers do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Elas não incluem a memória alocada para outros componentes dentro do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os componentes incluem o seguinte:

  - Os threads de trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
  - Várias DLLs e vários componentes que o processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] carrega dentro do espaço de endereço do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]
  - As operações de backup e restauração

- As DLLs e os componentes incluem vários provedores OLE DB, procedimentos armazenados estendidos, objetos COM da Microsoft usados para o procedimento armazenado sp_OACreate, servidores vinculados e o CLR do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. A memória alocada para esses componentes se enquadra na região do pool sem buffer do espaço de endereço do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para determinar de maneira ideal a quantidade máxima de memória que todo o processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode usar, você precisa subtrair a memória alocada para componentes que não usam o pool de buffers da memória total que você deseja que seja usada no processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Em seguida, você poderá usar o valor restante para definir a opção max server memory. Antes de definir as opções max server memory e min server memory, examine cuidadosamente o tópico "Como definir as opções de memória manualmente" nos Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

- Determine o requisito de memória de outros aplicativos e dos componentes do sistema operacional Windows. Os aplicativos podem incluir outros componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], por exemplo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, os Agentes de Replicação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Reporting Services, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Analysis Services, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Integration Services e a pesquisa de texto completo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Os aplicativos que executam operações de backup e de cópia de arquivos podem usar muitas memórias. Considere as operações como cópia em massa e o Agente de Instantâneo que geram E/S de arquivo. Você precisará considerar o requisito de memória de todos esses aplicativos ao determinar o valor das opções max server memory e min server memory. Use os contadores Bytes Particulares e Conjunto de Trabalho no objeto de Processo de cada processo para determinar o requisito de memória de um processo específico.

- Por padrão, o direito de usuário Bloquear páginas na memória já foi atribuído à conta interna Sistema Local. Para obter mais informações, acesse o seguinte site da Microsoft: [É necessário atribuir o privilégio Bloquear páginas na Memória no Sistema Local?](https://techcommunity.microsoft.com/t5/sql-server-support/do-i-have-to-assign-the-lock-pages-in-memory-privilege-for-local/ba-p/315426?advanced=false&collapse_discussion=true&search_type=thread)

- Se você usar uma conta de usuário do Windows globalmente para todos os processos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um domínio, determine os direitos de usuário que são atribuídos usando uma configuração de Política de Grupo. Um processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de 32 bits pode usar essa conta como a conta de inicialização. No entanto, essa conta exige o direito de usuário Bloquear páginas na memória para habilitar o recurso AWE (`Address Windowing Extensions`). Para obter mais informações, confira o tópico "Como fornecer a quantidade máxima de memória para o SQL Server" em Manuais Online do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

- Antes de configurar as opções max server memory e min server memory para várias instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], considere os requisitos de memória do pool sem buffer para cada instância do SQL Server. Em seguida, configure essas opções para cada instância do SQL Server.

O ideal é que você colete essas informações de linha de base durante cargas de pico. Portanto, você pode determinar os requisitos de memória para vários aplicativos e componentes para dar suporte à carga de pico. Os requisitos de memória variam de um sistema para outro, dependendo das atividades e dos aplicativos em execução no sistema. Consulte as informações fornecidas na exibição de gerenciamento dinâmico sys.dm_os_process_memory para entender se o sistema está enfrentando condições de memória insuficiente. Para obter mais informações, confira [sys.dm_os_process_memory (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-process-memory-transact-sql).

## <a name="improvements-added-in-windows-server-2008-and-r2-version"></a>Aprimoramentos adicionados ao Windows Server 2008 e versão R2

O Windows Server 2008 e o Windows Server 2008 R2 aprimoram o mecanismo de alocação de memória contígua. Esse aprimoramento permite que o Windows Server 2008 e o Windows Server 2008 R2 reduza, até certa medida, os efeitos da transferência do conjunto de trabalho de aplicativos para um arquivo de paginação quando novas solicitações de memória são recebidas.

Veja abaixo uma explicação dos aprimoramentos no white paper da Microsoft "Avanços no gerenciamento de memória no Windows":

*No Windows Server 2008, a alocação de memória contígua fisicamente é muito aprimorada. As solicitações de alocação memória contígua apresentam muito mais probabilidade de serem bem sucedidas, porque o gerenciador de memória agora substitui dinamicamente as páginas, normalmente, sem remover o conjunto de trabalho nem executar operações de E/S. Além disso, muitos outros tipos de páginas, como pilhas de kernel e páginas de metadados do sistema de arquivos, entre outros, agora são candidatos para substituição. Como resultado, mais memória contígua fica em disponibilidade geral a qualquer momento especificado. Além disso, o custo de obtenção dessas alocações foi bastante reduzido.*

Para obter mais informações, confira [Problemas de remoção do conjunto de trabalho no SQL Server](https://techcommunity.microsoft.com/t5/sql-server-support/sql-server-working-set-trim-problems-consider/ba-p/315462?advanced=false&collapse_discussion=true&search_type=thread).

Os produtos de terceiros mencionados neste artigo são fabricados por empresas que são independentes da Microsoft. A Microsoft não oferece nenhuma garantia, implícita ou não, sobre o desempenho ou a confiabilidade desses produtos.
