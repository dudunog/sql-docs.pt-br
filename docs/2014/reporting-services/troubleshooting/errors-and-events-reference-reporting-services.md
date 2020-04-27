---
title: Referência de erros e eventos (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- messages [Reporting Services]
- errors [Reporting Services]
- Reporting Services, errors and events
- troubleshooting [Reporting Services], errors
- events [Reporting Services]
ms.assetid: 818b4cc1-e65d-4f1a-bf7d-fe269e6dd739
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2708c2609d23c6094cd69bddd08d958a85262d88
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66099315"
---
# <a name="errors-and-events-reference-reporting-services"></a>Referência de erros e eventos (Reporting Services)
  Este tópico fornece informações sobre erros e eventos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]o. Os arquivos de log do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] também contêm informações de erro. Para obter mais informações sobre os tipos de arquivos de log que estão disponíveis e como exibir os logs, consulte [Fontes e arquivos de log do Reporting Services](../report-server/reporting-services-log-files-and-sources.md).  
  
## <a name="cause-and-resolution-for-reporting-services-error-messages"></a>Causa e resolução de mensagens de erro do Reporting Services  
 Causa e informações de resolução estão disponíveis para os erros mais frequentemente procurados nos sites da Web da [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Para obter informações, consulte [Causa e resolução de erros do Reporting Services](cause-and-resolution-of-reporting-services-errors.md).  
  
## <a name="report-server-events"></a>Eventos do servidor de relatório  
 Os eventos a seguir do servidor de relatório são registrados no log do aplicativo do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
|ID do evento|Type|Categoria|Fonte|Descrição|  
|--------------|----------|--------------|------------|-----------------|  
|106|Erro|Agendamento|Servidor de relatório|O SQL Server Agent deve estar em execução quando você define uma operação agendada (por exemplo, assinatura e entrega de relatório).|  
|[107](../../relational-databases/errors-events/mssqlserver-107-database-engine-error.md)|Erro|Inicialização/desligamento|Servidor de relatório<br /><br /> Processador de agendamento e entrega|A *\<Source>* não pode se conectar ao banco de dados do servidor de relatório. Para obter mais informações, consulte [Serviço Windows do Servidor de Relatório &#40;MSSQLServer&#41; 107](../../relational-databases/errors-events/mssqlserver-107-database-engine-error.md).|  
|108|Erro|Extensão|Servidor de relatório<br /><br /> Gerenciador de Relatórios|A *\<Source>* não pode carregar uma extensão de entrega, de processamento de dados ou de renderização.<br /><br /> Provavelmente, esse é o resultado de uma implantação incompleta ou remoção de uma extensão. Para obter mais informações, consulte [Implantando uma extensão de processamento de dados](../extensions/data-processing/deploying-a-data-processing-extension.md) e [Implantando uma extensão de entrega](../extensions/delivery-extension/deploying-a-delivery-extension.md).|  
|109|Informações|Gerenciamento|Servidor de relatório<br /><br /> Gerenciador de Relatórios|Um arquivo de configuração foi modificado. Para saber mais, confira [Arquivos de Configuração do Reporting Services](../report-server/reporting-services-configuration-files.md).|  
|110|Aviso|Gerenciamento|Servidor de relatório<br /><br /> Gerenciador de Relatórios|Uma configuração em um dos arquivos de configuração foi modificada e não é mais válida. Um valor padrão será usado em vez disso. Para saber mais, confira [Arquivos de Configuração do Reporting Services](../report-server/reporting-services-configuration-files.md).|  
|111|Erro|Registro em log|Servidor de relatório<br /><br /> Gerenciador de Relatórios|A *\<Source>* não pode criar o log de rastreamento. Para obter mais informações, consulte [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md).|  
|112|Aviso|Segurança|Servidor de relatório|O servidor de relatório detectou uma possível negação de ataque de serviço. Para obter mais informações, consulte [Segurança e proteção do Reporting Services](../security/reporting-services-security-and-protection.md).|  
|113|Erro|Registro em log|Servidor de relatório|O servidor de relatório não pode criar um contador de desempenho.|  
|114|Erro|Inicialização/desligamento|Gerenciador de Relatórios|O Gerenciador de Relatórios não pode se conectar ao serviço Servidor de Relatório.|  
|115|Aviso|Agendamento|Processador de agendamento e entrega|Uma tarefa agendada na fila do SQL Server Agent foi modificada ou excluída.|  
|116|Erro|Interna|Servidor de relatório<br /><br /> Gerenciador de Relatórios<br /><br /> Processador de agendamento e entrega|Ocorreu um erro interno.|  
|117|Erro|Inicialização/desligamento|Servidor de relatório|O banco de dados do servidor de relatório é uma versão inválida.|  
|118|Aviso|Registro em log|Servidor de relatório<br /><br /> Gerenciador de Relatórios|O arquivo de rastreamento não está mais no local do diretório previsto; um novo arquivo de rastreamento será criado no diretório padrão. Para obter mais informações, consulte [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md).|  
|119|Erro|Ativação|Servidor de relatório<br /><br /> Processador de agendamento e entrega|A *\<Source>* não recebeu acesso ao conteúdo do banco de dados do servidor de relatório.|  
|120|Erro|Ativação|Servidor de relatório|A chave simétrica não pode ser descriptografada. Provavelmente, houve uma alteração na conta na qual o serviço é executado. Para obter mais informações, consulte [Configurar e gerenciar chaves de criptografia &#40;Gerenciador de Configurações do SSRS&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|121|Erro|Inicialização/desligamento|Servidor de relatório|Falha ao iniciar o serviço RPC (Chamada de Procedimento Remoto).|  
|122|Aviso|Entrega|Processador de agendamento e entrega|O Processador de Agendamento e Entrega não pode se conectar ao servidor de SMTP usado para entrega de email. Para obter mais informações sobre conexões de servidor SMTP, consulte [configurar um servidor de relatório para entrega de email &#40;SSRS Configuration Manager&#41;](../../sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md).|  
|123|Aviso|Registro em log|Servidor de relatório<br /><br /> Gerenciador de Relatórios|Falha no servidor de relatório ao gravar o log de rastreamento. Para obter mais informações sobre logs de rastreamento, consulte [Log de rastreamento do serviço Servidor de Relatório](../report-server/report-server-service-trace-log.md).|  
|124|Informações|Ativação|Servidor de relatório|O serviço Servidor de Relatório foi iniciado. Para obter mais informações, consulte [Inicializar um Servidor de Relatório &#40;Gerenciador de Configurações do SSRS&#41;](../install-windows/ssrs-encryption-keys-initialize-a-report-server.md).|  
|125|Informações|Ativação|Servidor de relatório|A chave usada para criptografar dados foi extraída com êxito. Para obter mais informações sobre chaves, consulte [Configurar e gerenciar chaves de criptografia &#40;Gerenciador de Configurações do SSRS&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|126|Informações|Ativação|Servidor de relatório|A chave usada para criptografar dados foi aplicada com êxito. Para obter mais informações sobre chaves, consulte [Configurar e gerenciar chaves de criptografia &#40;Gerenciador de Configurações do SSRS&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|127|Informações|Ativação|Servidor de relatório|O conteúdo criptografado foi removido com êxito do banco de dados do servidor de relatório. Para obter mais informações sobre como excluir dados criptografados não recuperáveis, consulte [Configurar e gerenciar chaves de criptografia &#40;Gerenciador de Configurações do SSRS&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md).|  
|128|Erro|Ativação|Servidor de relatório|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Componentes de edições diferentes não podem ser usados juntos.|  
|129|Erro|Gerenciamento|Servidor de relatório<br /><br /> Processador de agendamento e entrega|Uma definição de arquivo de configuração criptografada não pode ser descriptografada.|  
|130|Erro|Gerenciamento|Servidor de relatório<br /><br /> Processador de agendamento e entrega|A *\<Source>* não pode localizar o arquivo de configuração. Arquivos de configuração são exigidos pelo servidor de relatório.|  
|131|Erro|Segurança|Servidor de relatório<br /><br /> Processador de agendamento e entrega|Um valor de dados de usuário criptografado não pôde ser descriptografado.|  
|132|Erro|Segurança|Servidor de relatório|Ocorreu uma falha durante a criptografia de dados de usuário. O valor não pode ser salvo.|  
|133|Erro|Gerenciamento|Servidor de relatório<br /><br /> Gerenciador de Relatórios<br /><br /> Processador de agendamento e entrega|Falha no carregamento da configuração do arquivo. Esse erro poderá ocorrer se o XML não for válido.|  
|134|Erro|Gerenciamento|Servidor de relatório|Falha no servidor de relatório ao criptografar valores para uma configuração em um arquivo de configuração.|  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar assinaturas do Reporting Services](../subscriptions/monitor-reporting-services-subscriptions.md)   
 [Fontes e arquivos de log do Reporting Services](../report-server/reporting-services-log-files-and-sources.md)  
  
  
