---
title: Caixa de diálogo Configurar Logs do SSIS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.configuredtslogs.loggingdetails.f1
- sql12.dts.designer.configuredtslogs.providersandlogs.f1
- sql12.dts.designer.configuredtslogs.containers.f1
helpviewer_keywords:
- Configure SSIS Logs dialog box
ms.assetid: 4b980275-cd9a-4943-8c36-727d51f9a484
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1f881435de01c7c21b80bff00b43c2399d0f7d75
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66060593"
---
# <a name="configure-ssis-logs-dialog-box"></a>caixa de diálogo Configurar Logs do SSIS
  Use a caixa de diálogo **Configurar Logs de SSIS** para definir as opções do log para um pacote.  
  
 **O que você deseja fazer?**  
  
1.  [Abrir a caixa de diálogo Configurar Logs de SSIS](#open_dialog)  
  
2.  [Configurar as opções no painel Contêineres](#container)  
  
3.  [Configurar as opções na guia Provedores e Logs](#provider)  
  
4.  [Configurar as opções na guia Detalhes](#detail)  
  
##  <a name="open-the-configure-ssis-logs-dialog-box"></a><a name="open_dialog"></a>Abrir a caixa de diálogo Configurar Logs do SSIS  
 **Para abrir a caixa de diálogo Configurar Logs de SSIS**  
  
-   No [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer, clique em **Log** no menu **SSIS** .  
  
##  <a name="configure-the-options-in-the-containers-pane"></a><a name="container"></a>Configurar as opções no painel contêineres  
 Use o painel **Contêineres** da caixa de diálogo **Configurar Logs do SSIS** para habilitar o pacote e seus contêineres para logs.  
  
### <a name="options"></a>Opções  
 **Contêineres**  
 Marque as caixas de seleção na exibição hierárquica para ativar o pacote e seus contêineres para logs:  
  
-   Se elas não forem marcadas, o contêiner não será ativado para logs. Selecione-as para ativar os logs.  
  
-   Quando esmaecido, o contêiner usa as opções de log pai. Esta opção não está disponível para o pacote.  
  
-   Quando marcado, o contêiner define suas próprias opções de log.  
  
 Se um contêiner estiver esmaecido e você quiser definir as opções de log no contêiner, clique duas vezes em sua caixa de seleção. O primeiro clique apaga a caixa de seleção e o segundo clique a seleciona, permitindo escolher os provedores de log que serão usados e selecionar as informações que serão registradas.  
  
##  <a name="configure-the-options-on-the-providers-and-logs-tab"></a><a name="provider"></a>Configurar as opções na guia provedores e logs  
 Use a guia **Provedores e Logs** da caixa de diálogo **Configurar Logs do SSIS** para criar e configurar logs para a captura de eventos do tempo de execução.  
  
### <a name="options"></a>Opções  
 **Tipo de provedor**  
 Selecione um tipo de provedor de log da lista.  
  
 **Adicionar**  
 Adicione um log do tipo especificado à coleção de provedores de log do pacote.  
  
 **Nome**  
 Habilite ou desabilite logs para contêineres ou tarefas selecionadas no painel **Contêineres** da caixa de diálogo **Configurar Logs do SSIS** usando as caixas de seleção. O campo de nome é editável. Use o nome padrão para o provedor ou digite um nome exclusivo.  
  
 **Descrição**  
 O campo de descrição é editável. Clique e modifique a descrição padrão do log.  
  
 **Configuração**  
 Selecione um Gerenciador de conexões existente na lista ou clique em \< **nova conexão...**> para criar um novo Gerenciador de conexões. Dependendo do tipo de provedor de log, você poderá configurar um gerenciador de conexões OLE DB ou um gerenciador de conexões Arquivo. O provedor de log do [!INCLUDE[msCoName](../includes/msconame-md.md)] Log de Eventos do Windows não requer conexão.  
  
 Tópicos relacionados: [Gerenciador de conexões OLE DB](connection-manager/ole-db-connection-manager.md) , [Gerenciador de Conexões de Arquivos](connection-manager/file-connection-manager.md)  
  
 **Delete (excluir)**  
 Selecione um provedor de log e clique em **Excluir**.  
  
##  <a name="configure-the-options-on-the-details-tab"></a><a name="detail"></a>Configurar as opções na guia detalhes  
 Use a guia **Detalhes** da caixa de diálogo **Configurar Logs do SSIS** para especificar eventos e detalhes informativos a serem habilitados para log. As informações selecionadas se aplicam a todos os provedores de logs no pacote. Por exemplo, você não pode gravar determinadas informações na instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e informações diferentes em um arquivo de texto.  
  
### <a name="options"></a>Opções  
 **Eventos**  
 Ative ou desative eventos para log.  
  
 **Descrição**  
 Exiba uma descrição do evento.  
  
 **Avançado**  
 Marque ou desmarque os eventos para log e marque ou desmarque informações que serão usadas no log de cada evento. Clique em **Básico** para ocultar todos os detalhes de log, exceto a lista de eventos. As informações a seguir estão disponíveis para log:  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Ele**|O nome do computador no qual o evento de log ocorreu.|  
|**Operador**|O nome de usuário da pessoa que iniciou o pacote.|  
|**SourceName**|O nome do pacote, contêiner ou tarefa no qual o evento de log ocorreu.|  
|**SourceID**|O Identificador Global Exclusivo (GUID) do pacote, contêiner ou tarefa no qual o evento de log ocorreu.|  
|**ExecutionID**|O Identificador Global Exclusivo da instância de execução do pacote.|  
|**MessageText**|Uma mensagem associada à entrada de log.|  
|**DataBytes**|Reservado para uso futuro.|  
  
 **Basic**  
 Marque ou desmarque os eventos para log. Esta opção oculta os detalhes de log, exceto a lista de eventos. Se você selecionar um evento, por padrão, todos os detalhes de log serão selecionados para esse evento. Clique em **Avançado** para mostrar todos os detalhes de log.  
  
 **Carregar**  
 Especifique um arquivo XML existente para ser usado como modelo para definir as opções de log.  
  
 **Salvar**  
 Salve os detalhes de configuração como um modelo para um arquivo XML.  
  
  
