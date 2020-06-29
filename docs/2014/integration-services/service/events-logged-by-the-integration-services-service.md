---
title: Eventos registrados em log pelo serviço Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- service [Integration Services], events
- events [Integration Services], service
- Integration Services service, events
ms.assetid: d4122dcf-f16f-47a0-93a2-ffa3d0d4f9cf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 70649de39a1eb3ef699b8d0521324eeefa7d5cda
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85421853"
---
# <a name="events-logged-by-the-integration-services-service"></a>Eventos registrados em log pelo serviço Integration Services Service
  O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] registra várias mensagens no log de eventos de Aplicativo do Windows. O serviço registra essas mensagens quando é iniciado e interrompido e quando ocorrem determinados problemas.  
  
 Este tópico contém informações sobre as mensagens de evento comuns registradas pelo serviço no log de eventos de Aplicativo. O serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] registra em log todas as mensagens descritas neste tópico com uma Origem de Evento de SQLISService.  
  
 Para obter informações gerais sobre o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], consulte [Serviço do Integration Services &#40;Serviço SSIS&#41;](integration-services-service-ssis-service.md).  
  
## <a name="messages-about-the-status-of-the-service"></a>Mensagens sobre o status do serviço  
 Quando você seleciona o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para instalação, o serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é instalado e iniciado e o Tipo de Inicialização é definido como Automático.  
  
|ID do evento|Nome simbólico|Texto|Observações|  
|--------------|-------------------|----------|-----------|  
|256|DTS_MSG_SERVER_STARTING|Como iniciar o serviço do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)].|O serviço está prestes a iniciar.|  
|257|DTS_MSG_SERVER_STARTED|Serviço do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] iniciado.|O serviço foi iniciado.|  
|260|DTS_MSG_SERVER_START_FAILED|Falha ao iniciar o Serviço do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)].%nErro: %1|Não foi possível iniciar o serviço. Essa incapacidade de iniciar pode ser o resultado de uma instalação danificada ou de uma conta de serviço inadequada.|  
|258|DTS_MSG_SERVER_STOPPING|Interrompendo o Serviço do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)].% n%nInterromper todos os pacotes em execução ao sair:%1|O serviço está sendo interrompido e, se você configurá-lo para fazer isso, todos os pacotes em execução serão interrompidos. Você pode definir um valor verdadeiro ou falso no arquivo de configuração que determina se o serviço deve interromper a execução de pacotes quando o próprio serviço é interrompido. A mensagem desse evento inclui o valor desta configuração.|  
|259|DTS_MSG_SERVER_STOPPED|Serviço do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] interrompido.%nVersão do servidor %1|O serviço parou.|  
  
## <a name="messages-about-the-configuration-file"></a>Mensagens sobre o arquivo de configuração  
 As configurações do serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] são armazenadas em um arquivo XML que pode ser modificado. Para obter mais informações, consulte [Configurando o Serviço Integration Services &#40;Serviço SSIS#41;](../configuring-the-integration-services-service-ssis-service.md).  
  
|ID do evento|Nome simbólico|Texto|Observações|  
|--------------|-------------------|----------|-----------|  
|274|DTS_MSG_SERVER_MISSING_CONFIG_REG|Serviço do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)]: %na configuração de Registro que especifica o arquivo de configuração não existe. %nTentando carregar o arquivo de configuração padrão.|A entrada do Registro que contém o caminho do arquivo de configuração não existe ou está vazia.|  
|272|DTS_MSG_SERVER_MISSING_CONFIG|O arquivo de configuração de serviço do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] não existe.%nCarregando com as configurações padrão.|O arquivo de configuração não existe no local especificado.|  
|273|DTS_MSG_SERVER_BAD_CONFIG|O arquivo de configuração de serviço do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)] está incorreto.%nErro ao ler o arquivo de configuração: %1%n%nCarregando o servidor com as configurações padrão.|Não foi possível ler o arquivo de configuração ou ele não é válido. Talvez esse erro seja o resultado de um erro de sintaxe XML no arquivo.|  
  
## <a name="other-messages"></a>Outras mensagens  
  
|ID do evento|Nome simbólico|Texto|Observações|  
|--------------|-------------------|----------|-----------|  
|336|DTS_MSG_SERVER_STOPPING_PACKAGE|Serviço do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssIS](../../includes/ssis-md.md)]: interrompendo a execução do pacote.%nIdentificação de instância do pacote: %1%nIdentificação do pacote: %2%nNome do pacote: %3%nDescrição do pacote: %4%nPacote|O serviço está tentando interromper um pacote em execução. Você pode monitorar e interromper pacotes em execução no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para obter informações sobre como gerenciar pacotes no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], consulte [Gerenciamento de pacotes &#40;Serviço SSIS&#41;](package-management-ssis-service.md).|  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter informações sobre como exibir entradas de log, consulte [Exibir entradas de log na janela Eventos de Log](../view-log-entries-in-the-log-events-window.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Eventos registrados em log por um pacote do Integration Services](../performance/events-logged-by-an-integration-services-package.md)  
  
  
