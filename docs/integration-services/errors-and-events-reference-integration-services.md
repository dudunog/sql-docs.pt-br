---
description: Referência de erros e eventos (Integration Services)
title: Referência de erros e eventos (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, events
- events [Integration Services]
- errors [Integration Services]
- Integration Services, errors
ms.assetid: cf4f0f14-8087-42d7-9b67-e4929228abd6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 814c5bb9915e448f97f0c769033d5fd695f76d95
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88391702"
---
# <a name="errors-and-events-reference-integration-services"></a>Referência de erros e eventos (Integration Services)

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  Esta seção da documentação contém informações sobre vários erros e eventos relacionados ao [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Causa e informações de resolução estão incluídas para mensagens de erro.  
  
 Para obter mais informações sobre mensagens de erro do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , incluindo uma lista da maior parte dos erros do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e suas descrições, consulte [Referência de mensagens e erros do Integration Services](../integration-services/integration-services-error-and-message-reference.md). No entanto a lista atual não inclui informações de solução de problemas.  
  
> [!IMPORTANT]  
>  Muitas das mensagens de erro que você pode ver quando está trabalhando com o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] originam-se de outros componentes. Entre eles, provedores OLE DB, outros componentes de banco de dados, como o [!INCLUDE[ssDE](../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , ou outros serviços ou componentes, como o sistema de arquivos, servidor SMTP, MSMQ (serviço de enfileiramento de mensagens) e assim por diante. Para obter informações sobre essas mensagens externas de erro, consulte a documentação específica do componente.  
  
## <a name="error-messages"></a>Mensagens de erro  
  
|Nome simbólico de erro|Descrição|  
|----------------------------|-----------------|  
|DTS_E_CACHELOADEDFROMFILE|Indica que o pacote não pode ser executado porque uma Transformação Cache está tentando gravar dados no cache na memória. No entanto, um gerenciador de conexões de Cache já carregou um arquivo de cache no cache na memória.|  
|DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER|Indica que o pacote não pode ser executado porque ocorreu uma falha na conexão especificada.|  
|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMN|Indica que um componente de fluxo de dados está tentando passar dados de cadeia de caracteres Unicode para outro componente que espera dados de cadeia de caracteres não Unicode na coluna correspondente ou vice-versa.|  
|DTS_E_CANNOTCONVERTBETWEENUNICODEANDNONUNICODESTRINGCOLUMNS|Indica que um componente de fluxo de dados está tentando passar dados de cadeia de caracteres Unicode para outro componente que espera dados de cadeia de caracteres não Unicode na coluna correspondente ou vice-versa.|  
|DTS_E_CANTINSERTCOLUMNTYPE|Indica que a coluna não pode ser adicionada à tabela de banco de dados porque a conversão entre o tipo de dados de coluna e o tipo de dados de coluna de banco de dados do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] não têm suporte.|  
|DTS_E_CONNECTIONNOTFOUND|Indica que o pacote não pode ser executado porque o gerenciador de conexões especificado não pode ser localizado.|  
|DTS_E_CONNECTIONREQUIREDFORMETADATA|Indica que o Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] deve conectar-se a uma fonte de dados para recuperar metadados novos ou atualizados para uma origem ou destino e que não é possível conectar-se à fonte de dados.|  
|DTS_E_MULTIPLECACHEWRITES|Indica que o pacote não pode ser executado porque uma Transformação Cache está tentando gravar dados no cache na memória. No entanto outra Transformação Cache já foi gravada no cache na memória.|  
|DTS_E_PRODUCTLEVELTOLOW|Indica que o pacote não pode ser executado porque a versão apropriada do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] não foi instalada.|  
|DTS_E_READNOTFILLEDCACHE|Indica que uma transformação Pesquisa está tentando ler dados do cache na memória ao mesmo tempo que uma transformação Cache está gravando dados no cache.|  
|DTS_E_UNPROTECTXMLFAILED|Indica que o sistema não descriptografou um nó XML protegido.|  
|DTS_E_WRITEWHILECACHEINUSE|Indica que uma Transformação Cache está tentando gravar dados no cache na memória ao mesmo tempo que uma transformação Pesquisa está lendo dados no cache na memória.|  
|DTS_W_EXTERNALMETADATACOLUMNSOUTOFSYNC|Indica que os metadados da coluna na fonte de dados não correspondem aos metadados da coluna no componente de origem ou de destino que está conectado à fonte de dados.|  
  
## <a name="events-sqlispackage"></a>Eventos (SQLISPackage)  
 Para obter mais informações, consulte [Eventos registrados por um pacote do Integration Services](../integration-services/performance/events-logged-by-an-integration-services-package.md).  
  
|Evento|Descrição|  
|-----------|-----------------|  
|SQLISPackage_12288|Indica que um pacote foi iniciado.|  
|SQLISPackage_12289|Indica que um pacote concluiu a execução com êxito.|  
|SQLISPACKAGE_12291|Indica que um pacote não pôde concluir a execução e foi interrompido.|  
|SQLISPackage_12546|Indica que uma tarefa ou outro executável em um pacote concluiu seu trabalho.|  
|SQLISPackage_12549|Indica que uma mensagem de aviso foi gerada em um pacote.|  
|SQLISPackage_12550|Indica que uma mensagem de erro foi gerada em um pacote.|  
|SQLISPackage_12551|Indica que um pacote não concluiu seu trabalho e foi interrompido.|  
|SQLISPackage_12557|Indica que um pacote concluiu a execução.|  
  
## <a name="events-sqlisservice"></a>Eventos (SQLISService)  
 Para obter mais informações, consulte [Eventos registrados pelo serviço do Integration Services](../integration-services/service/events-logged-by-the-integration-services-service.md).  
  
|Evento|Descrição|  
|-----------|-----------------|  
|SQLISService_256|Indica que o serviço está prestes a ser iniciado.|  
|SQLISService_257|Indica que o serviço foi iniciado.|  
|SQLISService_258|Indica que o serviço está prestes a ser interrompido.|  
|SQLISService_259|Indica que o serviço foi interrompido.|  
|SQLISService_260|Indica que o serviço tentou iniciar, mas não conseguiu.|  
|SQLISService_272|Indica que o arquivo de configuração não existe no local especificado.|  
|SQLISService_273|Indica que o arquivo de configuração não pôde ser lido ou não é válido.|  
|SQLISService_274|Indica que a entrada do Registro que contém o local do arquivo de configuração não existe ou está vazia.|  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de mensagens e erros do Integration Services](../integration-services/integration-services-error-and-message-reference.md)  
  
  
