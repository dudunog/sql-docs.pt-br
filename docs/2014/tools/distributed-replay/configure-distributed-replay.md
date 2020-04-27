---
title: Configurar Distributed Replay | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: aee11dde-daad-439b-b594-9f4aeac94335
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c5e44910c72e5162b9acb74ebbf74cd19d7ce1bc
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63149517"
---
# <a name="configure-distributed-replay"></a>Configure Distributed Replay
  Os detalhes de configuração do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay são especificados em arquivos XML no controlador do Distributed Replay, nos clientes e onde a ferramenta de administração está instalada. Esses arquivos incluem o seguinte:  
  
-   [Arquivo de configuração do controlador](#DReplayController)  
  
-   [Arquivo de configuração de cliente](#DReplayClient)  
  
-   [Arquivo de configuração de pré-processamento](#PreprocessConfig)  
  
-   [Arquivo de configuração de reprodução](#ReplayConfig)  
  
##  <a name="controller-configuration-file-dreplaycontrollerconfig"></a><a name="DReplayController"></a> Arquivo de configuração do controlador: DReplayController.config  
 Quando o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay Controller é iniciado, ele carrega o nível de log do arquivo de configuração do controlador, `DReplayController.config`. Esse arquivo está localizado na pasta em que você instalou o serviço de controlador de reprodução distribuída:  
  
 **\<caminho de instalação do controlador>\DReplayController.config**  
  
 O nível de log especificado pelo arquivo de configuração do controlador inclui o seguinte:  
  
|Configuração|Elemento XML|DESCRIÇÃO|Valores Permitidos|Obrigatório|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|Nível de log|`<LoggingLevel>`|Especifica o nível de log do serviço de controlador.|`INFORMATION` &#124; `WARNING` &#124; `CRITICAL`|Não. Por padrão, o valor é `CRITICAL`.|  
  
### <a name="example"></a>Exemplo  
 Este exemplo mostra um arquivo de configuração do controlador que foi modificado para suprimir as entradas de log `INFORMATION` e `WARNING` .  
  
```  
<?xml version='1.0'?>  
<Options>  
<LoggingLevel>CRITICAL</LoggingLevel>  
</Options>  
```  
  
##  <a name="client-configuration-file-dreplayclientconfig"></a><a name="DReplayClient"></a> Arquivo de configuração de cliente: DReplayClient.config  
 Quando o serviço cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Distributed Replay é iniciado, ele carrega as definições de configuração do arquivo de configuração de cliente, `DReplayClient.config`. Esse arquivo está localizado em cada cliente, na pasta em que você instalou o serviço de cliente de reprodução distribuída:  
  
 **\<caminho de instalação do cliente> \DReplayClient.config**  
  
 As configurações especificadas pelo arquivo de configuração de cliente incluem o seguinte:  
  
|Configuração|Elemento XML|DESCRIÇÃO|Valores Permitidos|Obrigatório|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|Controller|`<Controller>`|Especifica o nome do computador do controlador. O cliente tentará se registrar com o ambiente de Distributed Replay entrando em contato o controlador.|Você pode usar "`localhost`" ou "`.`" para fazer referência ao computador local.|Não. Por padrão, o cliente tenta se registrar com a instância de controlador que está sendo executada localmente ("`.`"), se existir.|  
|Diretório de trabalho do cliente|`<WorkingDirectory>`|É o caminho local no cliente onde os arquivos de expedição são salvos.<br /><br /> Os arquivos nesse diretório são substituídos na próxima reprodução.|Um nome de diretório completo, iniciando com a letra da unidade.|Não. Se nenhum valor for especificado, os arquivos de expedição serão salvos no mesmo local que o arquivo de configuração de cliente padrão. Se for especificado um valor e essa pasta não existir no cliente, o serviço do cliente não será iniciado.|  
|Diretório de resultado do cliente|`<ResultDirectory>`|É o caminho local no cliente onde o arquivo de rastreamento de resultado da atividade de reprodução (do cliente) é salvo.<br /><br /> Os arquivos nesse diretório são substituídos na próxima reprodução.|Um nome de diretório completo, iniciando com a letra da unidade.|Não. Se nenhum valor for especificado, o arquivo de rastreamento de resultado será salvo no mesmo local que o arquivo de configuração de cliente padrão. Se for especificado um valor e essa pasta não existir no cliente, o serviço do cliente não será iniciado.|  
|Nível de log|`<LoggingLevel>`|É o nível de log do serviço do cliente.|`INFORMATION` &#124; `WARNING` &#124; `CRITICAL`|Não. Por padrão, o valor é `CRITICAL`.|  
  
### <a name="example"></a>Exemplo  
 Este exemplo mostra um arquivo de configuração de cliente que foi modificado para especificar que o serviço de controlador está em execução em um computador diferente, um computador denominado `Controller1`. Os elementos `WorkingDirectory` e `ResultDirectory` foram configurados para usar as pastas `c:\ClientWorkingDir` e `c:\ResultTraceDir`, respectivamente. O nível de log foi alterado do valor padrão para suprimir as entradas de log `INFORMATION` e `WARNING` .  
  
```  
<?xml version='1.0'?>  
<Options>  
    <Controller>Controller1</Controller>  
    <WorkingDirectory>c:\ClientWorkingDir</WorkingDirectory>  
    <ResultDirectory>c:\ResultTraceDir</ResultDirectory>  
    <LoggingLevel>CRITICAL</LoggingLevel>  
</Options>  
```  
  
##  <a name="preprocess-configuration-file-dreplayexepreprocessconfig"></a><a name="PreprocessConfig"></a> Arquivo de configuração de pré-processamento: DReplay.exe.preprocess.config  
 Quando você usar a ferramenta de administração para iniciar o estágio de pré-processamento, ela carregará as configurações de pré-processamento do arquivo de configuração de pré-processamento, `DReplay.exe.preprocess.config`.  
  
 Use o arquivo de configuração padrão ou use o parâmetro **-c** da ferramenta de administração para especificar o local de um arquivo de configuração de pré-processamento modificado. Para obter mais informações de como usar a opção de pré-processamento da ferramenta de administração, confira [Opção de pré-processamento &#40;Ferramenta de administração do Distributed Replay&#41;](preprocess-option-distributed-replay-administration-tool.md).  
  
 O arquivo de configuração de pré-processamento padrão está localizado na pasta em que você instalou a ferramenta de administração:  
  
 **\<caminho de instalação da ferramenta de administração>\DReplayAdmin\DReplay.exe.preprocess.config**  
  
 As definições de configuração de pré-processamento são especificadas em elementos XML que são filhos do elemento `<PreprocessModifiers>` no arquivo de configuração de pré-processamento. Essas configurações incluem o seguinte:  
  
|Configuração|Elemento XML|DESCRIÇÃO|Valores Permitidos|Obrigatório|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|Incluir atividades de sessão de sistema|`<IncSystemSession>`|Indica se as atividades de sessão de sistema durante a captura serão incluídas durante a reprodução.|`Yes` &#124; `No`|Não. Por padrão, o valor é `No`.|  
|Tempo ocioso máximo|`<MaxIdleTime>`|Arredonda o tempo ocioso para um número absoluto (em segundos).|Um inteiro que é >=-1<br /><br /> `-1` indica que não houve alteração do valor original no arquivo de rastreamento original.<br /><br /> `0` indica que há alguma atividade ocorrendo em um determinado momento.|Não. Por padrão, o valor é `-1`.|  
  
### <a name="example"></a>Exemplo  
 O arquivo de configuração de pré-processamento padrão:  
  
```  
<?xml version='1.0'?>  
<Options>  
    <PreprocessModifiers>  
        <IncSystemSession>No</IncSystemSession>  
        <MaxIdleTime>-1</MaxIdleTime>  
    </PreprocessModifiers>  
</Options>  
```  
  
##  <a name="replay-configuration-file-dreplayexereplayconfig"></a><a name="ReplayConfig"></a> Arquivo de configuração de reprodução: DReplay.exe.replay.config  
 Quando você usar a ferramenta de administração para iniciar o estágio de reprodução do evento, ela carregará as configurações de reprodução do arquivo de configuração de reprodução, `DReplay.exe.replay.config`.  
  
 Use o arquivo de configuração padrão ou use o parâmetro **-c** da ferramenta de administração para especificar o local de um arquivo de configuração de reprodução modificado. Para obter mais informações de como usar a opção de reprodução da ferramenta de administração, confira [Opção de reprodução &#40;ferramenta de administração do Distributed Replay&#41;](replay-option-distributed-replay-administration-tool.md).  
  
 O arquivo de configuração de reprodução padrão está localizado na pasta em que você instalou a ferramenta de administração:  
  
 **\<caminho de instalação da ferramenta de administração>\DReplayAdmin\DReplay.exe.replay.config**  
  
 As definições de configuração de reprodução são especificadas em elementos XML que são filhos dos elementos `<ReplayOptions>` e `<OutputOptions>` do arquivo de configuração de reprodução.  
  
### <a name="replayoptions-element"></a>Elemento \<ReplayOptions>  
 As configurações especificadas pelo arquivo de configuração de reprodução no elemento `<ReplayOptions>` incluem o seguinte:  
  
|Configuração|Elemento XML|DESCRIÇÃO|Valores Permitidos|Obrigatório|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|Instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (o servidor de teste)|`<Server>`|Especifica o nome do servidor e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conexão.|*server_name*[\\*instance_name*]<br /><br /> Você não pode usar "`localhost`" ou "`.`" para representar o host local.|Não, se o nome do servidor já tiver sido especificado usando o parâmetro **-s**_target server_ com a opção **replay** da ferramenta de administração.|  
|Modo de sequenciamento|`<SequencingMode>`|Especifica o modo usado para o agendamento de eventos.|`synchronization` &#124; `stress`|Não. Por padrão, o valor é `stress`.|  
|Granularidade de escala de tensão|`<StressScaleGranularity>`|Especifica se deveriam ser dimensionadas todas as conexões no Identificador de Perfil de Serviço (SPID) junto (SPID) ou independentemente (Conexão) sob modo de tensão.|SPID &#124; Conexão|Sim. Por padrão, o valor é `SPID`.|  
|Escala de tempo de conexão|`<ConnectTimeScale>`|É usada para dimensionar o tempo de conexão em modo de estresse.|Um inteiro entre `1` e `100`.|Não. Por padrão, o valor é `100`.|  
|Escala de tempo de resposta|`<ThinkTimeScale>`|É usada para dimensionar o tempo de resposta em modo de estresse.|Um inteiro entre `0` e `100`.|Não. Por padrão, o valor é `100`.|  
|Usar o pool de conexões|`<UseConnectionPooling>`|Especifica se conexão agrupando será habilitado em cada cliente de Reprodução distribuída.|Sim &#124; Não|Sim. Por padrão, o valor é `Yes`.|  
|Intervalo do monitor de integridade|`<HealthmonInterval>`|Indica a frequência com que o monitor de integridade deve ser executado (em segundos).<br /><br /> Este valor é usado somente no modo de sincronização.|Inteiro >= 1<br /><br /> (`-1` para desabilitar)|Não. Por padrão, o valor é `60`.|  
|Tempo limite de consulta|`<QueryTimeout>`|Especifica o valor do tempo limite de consulta, em segundos. Esse valor estará em vigor somente até que a primeira linha tenha sido retornada.|Inteiro >= 1<br /><br /> (`-1` para desabilitar)|Não. Por padrão, o valor é `3600`.|  
|Threads por cliente|`<ThreadsPerClient>`|Especifica o número de threads de reprodução que devem ser usados para cada cliente de reprodução.|Um inteiro entre `1` e `512`.|Não. Se não especificado, o Distributed Replay usará o valor `255`.|  
  
### <a name="outputoptions-element"></a>Elemento \<OutputOptions>  
 As configurações especificadas pelo arquivo de configuração de reprodução no elemento `<OutputOptions>` incluem o seguinte:  
  
|Configuração|Elemento XML|DESCRIÇÃO|Valores Permitidos|Obrigatório|  
|-------------|-----------------|-----------------|--------------------|--------------|  
|Gravar contagem de linhas|`<RecordRowCount>`|Indica se a contagem de linhas de cada conjunto de resultados deve ser gravada.|`Yes` &#124; `No`|Não. Por padrão, o valor é `Yes`.|  
|Gravar conjunto de resultados|`<RecordResultSet>`|Indica se o conteúdo de todos os conjuntos de resultados deve ser gravado.|`Yes` &#124; `No`|Não. Por padrão, o valor é `No`.|  
  
### <a name="example"></a>Exemplo  
 O arquivo de configuração de reprodução padrão:  
  
```  
<?xml version='1.0'?>  
<Options>  
    <ReplayOptions>  
        <Server></Server>  
        <SequencingMode>stress</SequencingMode>  
        <ConnectTimeScale></ConnectTimeScale>  
        <ThinkTimeScale></ThinkTimeScale>  
        <HealthmonInterval>60</HealthmonInterval>  
        <QueryTimeout>3600</QueryTimeout>  
        <ThreadsPerClient></ThreadsPerClient>  
    </ReplayOptions>  
    <OutputOptions>  
        <ResultTrace>  
            <RecordRowCount>Yes</RecordRowCount>  
            <RecordResultSet>No</RecordResultSet>  
        </ResultTrace>  
    </OutputOptions>  
</Options>  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Opções de linha de comando da ferramenta de administração &#40;utilitário de Distributed Replay&#41;](administration-tool-command-line-options-distributed-replay-utility.md)   
 [SQL Server Distributed Replay](sql-server-distributed-replay.md)   
 [Fórum de Distributed Replay de SQL Server](https://social.technet.microsoft.com/Forums/sl/sqldru/)   
 [Usando Distributed Replay para teste de carga de sua SQL Server-parte 2](https://blogs.msdn.com/b/mspfe/archive/2012/11/14/using-distributed-replay-to-load-test-your-sql-server-part-2.aspx)   
 [Usando o Distributed Replay para teste de carga do SQL Server – Parte 1](https://blogs.msdn.com/b/mspfe/archive/2012/11/08/using-distributed-replay-to-load-test-your-sql-server-part-1.aspx)  
  
  
