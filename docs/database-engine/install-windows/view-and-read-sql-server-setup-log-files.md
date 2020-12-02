---
title: Exibir e ler arquivos de log da Instalação do SQL Server | Microsoft Docs
description: Este artigo descreve os arquivos de log que a Instalação do SQL Server cria. Os arquivos de log são colocados em uma pasta com carimbo de data/hora.
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- viewing logs
- displaying log files
- Setup [SQL Server], logs
- installation log files [SQL Server]
- installing SQL Server, logs
- errors [SQL Server], Setup
- logs [SQL Server], Setup
ms.assetid: 9d77af64-9084-4375-908a-d90f99535062
author: cawrites
ms.author: chadam
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 4cf535ee95b91a0e9b6ed3ba2b8745478736a142
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125662"
---
# <a name="view-and-read-sql-server-setup-log-files"></a>Exibir e ler arquivos de log da Instalação do SQL Server

[!INCLUDE [SQL Server -Windows Only](../../includes/applies-to-version/sql-windows-only.md)]

A Instalação do SQL Server cria arquivos de log em uma pasta com carimbo de data/hora em **\%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log** por padrão, em que *nnn* são números que correspondem à versão do SQL que está sendo instalada. O formato de nome da pasta com carimbo de data/hora é AAAAMMDD_hhmmss. Quando a Instalação é executada em um modo autônomo, os logs são criados em % temp%\sqlsetup*.log. Todos os arquivos da pasta de log são arquivados no arquivo Log\*.cab em sua respectiva pasta de log.  

   | Arquivo           | Caminho |
   | :------        | :----------------------------- |
   | **Summary.txt**    | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log |
   | **Summary_\<MachineName>\_Date.txt**  | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **Detail.txt** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss|
   | **Datastore** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\Datastore
   | **Arquivos de log MSI** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss\\\<Name>.log|
   | **ConfigurationFile.ini** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **SystemConfigurationCheck_Report.htm** | \%programfiles%\Microsoft SQL Server\\*nnn*\Setup Bootstrap\Log\YYYYMMDD_hhmmss |
   | **Para instalações autônomas** | %temp%\sqlsetup*.log |


 ![Captura de tela que mostra onde o arquivo ConfigurationFiles.ini pode ser encontrado na pasta de Inicialização da Instalação.](media/view-and-read-sql-server-setup-log-files/setup-bootstrap-example.png)

 >[!NOTE]
 > Os números no caminho *nnn* correspondem à versão do SQL que está sendo instalado. Na figura acima, o SQL 2017 foi instalado, portanto, a pasta é 140. Para o SQL 2016, a pasta seria 130 e para SQL 2014, a pasta seria 120.
  
 A instalação do SQL Server conclui três fases básicas: 
  
1.  Verificação de regras global: valida os requisitos de sistema básicos
2.  Atualização de componente: verifica se há atualizações disponíveis para a mídia de instalação
3.  Ação solicitada pelo usuário: permite que o usuário selecione e personalize recursos
  

Este fluxo de trabalho gera um único log de resumo, bem como uma das seguintes alternativas: um log de detalhes para uma instalação básica do SQL Server ou dois logs de detalhes para quando uma atualização, assim como um service pack, é instalada junto com a instalação básica. 
  
Adicionalmente, há arquivos de armazenamento de dados que contêm um instantâneo do estado de todos os objetos de configuração que estão sendo rastreados pelo processo de instalação e são úteis para solucionar problemas de erros de configuração. Arquivos de despejo XML são criados para cada fase de execução e são salvos na subpasta de log de armazenamento de dados na pasta de log com carimbo de hora. 

As seções a seguir descrevem arquivos de log da Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="summarytxt-file"></a>Arquivo Summary.txt 
  
### <a name="overview"></a>Visão geral  
 Esse arquivo mostra os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detectados durante Instalação, o ambiente de sistema operacional, valores de parâmetros de linha de comando, caso sejam especificados, e o status global de cada MSI/MSP que foi executado.
  
 O log é organizado nas seguintes seções:
  
-   Um resumo global da execução  
-   As propriedades e a configuração do computador em que a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] foi executada  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Recursos do produto instalados anteriormente no computador  
-   Descrição da versão de instalação e propriedades do pacote de instalação
-   Configurações de entrada em runtime que são fornecidas durante instalação  
-   Local do arquivo de configuração  
-   Detalhes dos resultados de execução  
-   Regras globais  
-   Regras específicas ao cenário de instalação  
-   Regras com falha  
-   Local do arquivo de relatório de regras


  >[!NOTE]
  > Observe que ao aplicar patches, pode haver diversas subpastas (uma para cada instância na qual o patch está sendo aplicado e uma para recursos compartilhados) que contêm um conjunto similar de arquivos (ou seja, %programfiles%\MicrosoftSQL Server\130\Setup Bootstrap\Log\<YYYYMMDD_HHMM>\MSSQLSERVER). 
  
### <a name="location"></a>Location  
 O arquivo summary.txt está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\.
  
 Para localizar erros no arquivo de texto resumido, pesquise o arquivo usando as palavras-chave "error" ou "failed".
  
## <a name="summary_machinename_yyyymmdd_hhmmsstxt-file"></a>Summary_\<MachineName>_YYYYMMDD_HHMMss.txt file
  
### <a name="overview"></a>Visão geral  
 O arquivo de base summary_engine é semelhante ao arquivo de resumo e é gerado durante o fluxo de trabalho principal.
  
### <a name="location"></a>Location  
 O arquivo Summary_\<MachineName>_YYYYMMDD_HHMMss.txt está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.
  
  
## <a name="detailtxt-file"></a>Arquivo Detail.txt
  
### <a name="overview"></a>Visão geral
 O arquivo Detail.txt é gerado para o fluxo de trabalho principal, como instalação ou atualização, e fornece os detalhes da execução. Os logs do arquivo são gerados com base na hora em que cada ação para a instalação foi invocada. O arquivo de texto mostra a ordem na qual as ações foram executadas, bem como suas dependências.  
  
### <a name="location"></a>Location  
 O arquivo detail.txt está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\Detail.txt.  
  
 Se ocorrer um erro durante o processo de Instalação, a exceção ou o erro será registrado no final desse arquivo. Para localizar os erros nesse arquivo, primeiro examine o final do arquivo e depois efetue uma pesquisa do arquivo pelas palavras-chave "error" ou "exception"
    
## <a name="msi-log-files"></a>Arquivos de log MSI
  
### <a name="overview"></a>Visão geral  
 Os arquivos de log MSI fornecem detalhes do processo de pacote de instalação. Eles são gerados pelo MSIEXEC durante a instalação do pacote especificado.  
  
 Tipos de arquivos de log MSI:
  
-   \<Feature>_\<Architecture>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Language>\_\<Interaction>.log   
-   \<Feature>_\<Architecture>\_\<Interaction>\_\<workflow>.log  
  
### <a name="location"></a>Location  
 Os arquivos de log MSI estão localizados em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\<Name\>.log.  
  
 No final do arquivo, há um resumo da execução, que inclui o status de êxito ou falha e propriedades. Para localizar o erro no arquivo MSI, pesquise "value 3" e revise o texto antes e depois.  
  
## <a name="configurationfileini-file"></a>Arquivo ConfigurationFile.ini
  
### <a name="overview"></a>Visão geral  
 O arquivo de configuração contém as configurações de entrada que são fornecidas durante instalação. Pode ser usado para reiniciar a instalação sem ser necessário inserir as configurações manualmente. Entretanto, as senhas das contas, o PID e alguns parâmetros não são salvos no arquivo de configuração. As configurações podem ser adicionadas ao arquivo ou fornecidas por meio da linha de comando ou da interface do usuário de Instalação. Para obter mais informações, veja [Instalar o SQL Server 2016 usando um arquivo de configuração](./install-sql-server-using-a-configuration-file.md).  
  
### <a name="location"></a>Location  
 O arquivo ConfigurationFile.ini está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.  
  
## <a name="systemconfigurationcheck_reporthtm-file"></a>Arquivo SystemConfigurationCheck_Report.htm
  
### <a name="overview"></a>Visão geral  
 O relatório de verificação da configuração do sistema contém uma breve descrição de cada regra executada, bem como o status de execução.
  
### <a name="location"></a>Location  
O arquivo SystemConfigurationCheck_Report.htm está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\*nnn*\Setup Bootstrap\Log\\<YYYYMMDD_HHMM>\\.

[!INCLUDE[get-help-options](../../includes/paragraph-content/get-help-options.md)]
  
## <a name="see-also"></a>Confira também  
 [Instalar o SQL Server 2017](../../database-engine/install-windows/install-sql-server.md)