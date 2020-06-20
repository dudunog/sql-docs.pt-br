---
title: Gerenciar arquivos de log do DQS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
helpviewer_keywords:
- logging
- log files
- dqs log files
ms.assetid: 4fccfd24-aede-4882-be69-ec1e82682e16
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 6e22df90d4e5cb08ac5836f78f4940559be266ec
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937527"
---
# <a name="manage-dqs-log-files"></a>Gerenciar arquivos de log do DQS
  Arquivos de log do[!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) o ajudam a diagnosticar e solucionar problemas no [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]e no [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)]. São gerados arquivos de log separados para o [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)], o [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]e o [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)].  
  
 Você pode usar o [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] para definir a configuração de severidade de log para recursos e módulos do [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] . Adicionalmente, você também pode definir outras configurações (avançadas) para os arquivos de log do DQS, alterando manualmente os parâmetros de configuração de log DQS no banco de dados DQS_MAIN e um arquivo XML no computador [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] .  
  
##  <a name="data-quality-server-log-file"></a><a name="DQSServer"></a>Arquivo de log do Data Quality Server  
 O arquivo de log [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] , DQServerLog.DQS_MAIN.log, inclui logs de atividades que são executadas no [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]. Se você tiver instalado a instância padrão do SQL Server, o arquivo DQServerLog.DQS_MAIN.log estará disponível em C:\Arquivos de Programas\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Log. O arquivo de log [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] contém as seguintes informações, delimitadas por uma barra (|):  
  
-   Data e Hora  
  
-   Nome do thread  
  
-   ID do thread  
  
-   Severidade do log (FATAL, ERROR, WARN, INFO e DEBUG)  
  
    > [!NOTE]  
    >  A severidade de log DEBUG equivale a Detalhado.  
  
-   UID (ID de infraestrutura de DQS interna)  
  
-   Namespace  
  
-   Classe e método  
  
-   Mensagem  
  
 Além disso, o arquivo de log exibe também informações sobre a versão do aplicativo, o nome de computador, o nome do usuário e o sistema operacional.  
  
 Uma entrada de exemplo no arquivo de log [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] tem a seguinte aparência:  
  
```  
23-08-2013 01:45:29|[]|4|INFO|PUID|InfInfoModuleStarting|Microsoft.Ssdqs.Core.Startup.ServerInit|Starting DQS ServerInit: version [12.0.0.0], machine name [DQS-TEST], user name [NT Service\MSSQLSERVER], operating system [Microsoft Windows NT 6.1.7600.0]...  
```  
  
 O arquivo DQServerLog.DQS_MAIN.log é um arquivo rolante; um novo arquivo de log é criado quando o arquivo de log existente excede o limite de tamanho do arquivo rolante especificado nos parâmetros de configuração de log do [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] . Para obter mais informações, consulte [Configure Advanced Settings for DQS Log Files](../../2014/data-quality-services/configure-advanced-settings-for-dqs-log-files.md).  
  
##  <a name="data-quality-client-log-file"></a><a name="DQSClient"></a>Data Quality Client arquivo de log  
 O arquivo de log [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , DQClientLog.log, inclui logs do lado do cliente. O arquivo de log [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] está disponível em %APPDATA%\SSDQS\Log. O arquivo de log [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] contém um conjunto de informações semelhante ao do arquivo de log de servidor, mas para o lado do cliente.  
  
 Assim como no arquivo de log [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] , o arquivo de log [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] também é um arquivo rolante; um novo arquivo de log é criado quando o arquivo de log existente excede o limite de tamanho do arquivo rolante especificado nos parâmetros de configuração de log do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Para obter mais informações, consulte [Configure Advanced Settings for DQS Log Files](../../2014/data-quality-services/configure-advanced-settings-for-dqs-log-files.md).  
  
##  <a name="dqs-cleansing-component-log-file"></a><a name="DQSCleansing"></a>Arquivo de log do componente de limpeza DQS  
 O arquivo de log [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] , DQSSSISLog.log, inclui logs de atividades executados usando o [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)]. O arquivo de log de componente [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] está disponível em %APPDATA%\SSDQS\Log. O arquivo de log [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)] contém um conjunto de informações semelhante ao do arquivo de log de servidor, mas para o [!INCLUDE[ssDQSCleansing](../includes/ssdqscleansing-md.md)].  
  
##  <a name="related-tasks"></a><a name="RT"></a> Tarefas relacionadas  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Descreve como definir configurações de severidade de log para arquivos de log DQS usando o [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].|[Configurar níveis de severidade para arquivos de log do DQS](../../2014/data-quality-services/configure-severity-levels-for-dqs-log-files.md)|  
|Descreve como definir manualmente configurações avançadas para arquivos de log DQS.|[Definir configurações avançadas para arquivos de log do DQS](../../2014/data-quality-services/configure-advanced-settings-for-dqs-log-files.md)|  
  
## <a name="see-also"></a>Consulte Também  
 [administração do dqs](../../2014/data-quality-services/dqs-administration.md)  
  
  
