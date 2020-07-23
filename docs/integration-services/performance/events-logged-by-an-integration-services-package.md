---
title: Eventos registrados em log por um pacote do Integration Services | Microsoft Docs
ms.custom: supportability
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- package [Integration Services], events
- events [Integration Services], package
ms.assetid: 55a0951a-46f3-4f0f-9972-74cec9cc26b7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: cd247b193540076a1d0f922e94e752b1ea0456bb
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86919135"
---
# <a name="events-logged-by-an-integration-services-package"></a>Eventos registrados em log por um pacote do Integration Services

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] registra várias mensagens de eventos no log de eventos de Aplicativo do Windows. Um pacote registra estas mensagens quando é iniciado e interrompido e quando ocorrem determinados problemas.  
  
 Este tópico contém informações sobre as mensagens de evento comuns registradas por um pacote no log de eventos de Aplicativo. Por padrão, um pacote registra algumas dessas mensagens mesmo que você não tenha habilitado o log no pacote. Todavia, existem outras mensagens que serão registradas em log pelo pacote apenas se você tiver habilitado o log nele. Independentemente de o pacote registrar essas mensagens em log por padrão ou de o log estar habilitado, a Origem do Evento das mensagens é SQLISPackage.  
  
 Para obter informações gerais sobre como executar pacotes SSIS, consulte [Execução de projetos e pacotes](../packages/run-integration-services-ssis-packages.md).  
  
 Para obter informações sobre como solucionar problemas de execução de pacotes, consulte [Solucionando problemas de ferramentas para execução de pacotes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="messages-about-the-status-of-the-package"></a>Mensagens sobre o status do pacote  
 Normalmente quando um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é executado, ele registra em log várias mensagens sobre o andamento e o status do pacote. A tabela a seguir lista essas mensagens.  
  
> [!NOTE]  
>  O pacote registrará em log as mensagens listadas na tabela abaixo mesmo que você não tenha habilitado o log no pacote.  
  
|ID do evento|Nome simbólico|Texto|Observações|  
|--------------|-------------------|----------|-----------|  
|12288|DTS_MSG_PACKAGESTART|Pacote "" iniciado.|A execução do pacote foi iniciada.|  
|12289|DTS_MSG_PACKAGESUCCESS|Pacote "" concluído com êxito.|O pacote foi executado com êxito e não está mais sendo executado.|  
|12290|DTS_MSG_PACKAGECANCEL|Pacote "%1!s!" foi cancelado.|O pacote não está mais sendo executado, pois foi cancelado.|  
|12291|DTS_MSG_PACKAGEFAILURE|Falha no pacote "".|O pacote não foi executado com êxito e foi interrompido.|  
  
 Por padrão, em uma nova instalação, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é configurado para não registrar determinados eventos relacionados à execução de pacotes no log de eventos do Aplicativo. Essa configuração impede entradas excessivas no log de eventos quando você usa o recurso Coletor de Dados da versão atual do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Os eventos registrados são EventID 12288, "Pacote iniciado" e EventID 12289, "Pacote concluído com êxito". Para registrar esses eventos no log de eventos do Aplicativo, abra o Registro para edição. Em seguida, no Registro, localize o nó HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS e altere o valor DWORD da configuração LogPackageExecutionToEventLog de 0 para 1. No entanto, em uma instalação de atualização, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] é configurado para registrar esses dois eventos. Para desabilitar o log, altere o valor da configuração do LogPackageExecutionToEventLog de 1 para 0.  
  
## <a name="messages-associated-with-package-logging"></a>Mensagens associadas ao log de pacote  
 Se você habilitou o registro em log no pacote, o log de eventos de Aplicativo é um dos destinos suportados pelos recursos de log opcionais em pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
 Quando você habilitou o registro em log no pacote e o local dos logs é o log de eventos de Aplicativo, o pacote registra em log entradas que pertencem às seguintes informações:  
  
-   Mensagens sobre o estágio da execução do pacote.  
  
-   Mensagens sobre eventos específicos que ocorrem durante a execução do pacote.  
  
### <a name="messages-about-the-stages-of-package-execution"></a>Mensagens sobre os estágios da execução do pacote.  
  
|ID do evento|Nome simbólico|Texto|Observações|  
|--------------|-------------------|----------|-----------|  
|12544|DTS_MSG_EVENTLOGENTRY|Nome do Evento: %1%r Mensagem: %9%r Operador: %2%r Nome da Origem: %3%r ID da Origem: %4%r ID de Execução: %5%r Hora de Início: %6%r Hora de Término: %7%r Código de Dados: %8|Quando você configura o log de pacotes para o log de eventos de Aplicativo, várias mensagens usam esse formato genérico.|  
|12556|DTS_MSG_EVENTLOGENTRY_PACKAGESTART|Nome do Evento: %1%r Mensagem: %9%r Operador: %2%r Nome da Origem: %3%r ID da Origem: %4%r ID de Execução: %5%r Hora de Início: %6%r Hora de Término: %7%r Código de Dados: %8|O pacote foi iniciado.|  
|12547|DTS_MSG_EVENTLOGENTRY_PREVALIDATE|Nome do Evento: %1%r Mensagem: %9%r Operador: %2%r Nome da Origem: %3%r ID da Origem: %4%r ID de Execução: %5%r Hora de Início: %6%r Hora de Término: %7%r Código de Dados: %8|A validação do objeto está prestes a começar.|  
|12548|DTS_MSG_EVENTLOGENTRY_POSTVALIDATE|Nome do Evento: %1%r Mensagem: %9%r Operador: %2%r Nome da Origem: %3%r ID da Origem: %4%r ID de Execução: %5%r Hora de Início: %6%r Hora de Término: %7%r Código de Dados: %8|A validação do objeto foi concluída.|  
|12552|DTS_MSG_EVENTLOGENTRY_PROGRESS|Nome do Evento: %1%r Mensagem: %9%r Operador: %2%r Nome da Origem: %3%r ID da Origem: %4%r ID de Execução: %5%r Hora de Início: %6%r Hora de Término: %7%r Código de Dados: %8|Esta mensagem genérica informa o andamento do pacote.|  
|12546|DTS_MSG_EVENTLOGENTRY_POSTEXECUTE|Nome do Evento: %1%r Mensagem: %9%r Operador: %2%r Nome da Origem: %3%r ID da Origem: %4%r ID de Execução: %5%r Hora de Início: %6%r Hora de Término: %7%r Código de Dados: %8|O objeto concluiu seu trabalho.|  
|12557|DTS_MSG_EVENTLOGENTRY_PACKAGEEND|Nome do Evento: %1%r Mensagem: %9%r Operador: %2%r Nome da Origem: %3%r ID da Origem: %4%r ID de Execução: %5%r Hora de Início: %6%r Hora de Término: %7%r Código de Dados: %8|A execução do pacote foi concluída.|  
  
### <a name="messages-about-events-that-occur"></a>Mensagens sobre eventos que ocorrem  
 A tabela a seguir lista apenas algumas das mensagens geradas por eventos. Para obter uma lista mais completa de erros, avisos e mensagens informativas usados pelo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , consulte [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md).  
  
|ID do evento|Nome simbólico|Texto|Observações|  
|--------------|-------------------|----------|-----------|  
|12251|DTS_MSG_EVENTLOGENTRY_TASKFAILED|Nome do Evento: %1%r Mensagem: %9%r Operador: %2%r Nome da Origem: %3%r ID da Origem: %4%r ID de Execução: %5%r Hora de Início: %6%r Hora de Término: %7%r Código de Dados: %8|A tarefa falhou.|  
|12250|DTS_MSG_EVENTLOGENTRY_ERROR|Nome do Evento: %1%r Mensagem: %9%r Operador: %2%r Nome da Origem: %3%r ID da Origem: %4%r ID de Execução: %5%r Hora de Início: %6%r Hora de Término: %7%r Código de Dados: %8|Esta mensagem reporta um erro ocorrido.|  
|12249|DTS_MSG_EVENTLOGENTRY_WARNING|Nome do Evento: %1%r Mensagem: %9%r Operador: %2%r Nome da Origem: %3%r ID da Origem: %4%r ID de Execução: %5%r Hora de Início: %6%r Hora de Término: %7%r Código de Dados: %8|Esta mensagem reporta um aviso ocorrido.|  
|12258|DTS_MSG_EVENTLOGENTRY_INFORMATION|Nome do Evento: %1%r Mensagem: %9%r Operador: %2%r Nome da Origem: %3%r ID da Origem: %4%r ID de Execução: %5%r Hora de Início: %6%r Hora de Término: %7%r Código de Dados: %8|Esta mensagem reporta informações não associadas a um erro ou aviso.|  

## <a name="view-log-entries-in-the-log-events-window"></a>Exibir entradas de log na janela Eventos de Log
  Este procedimento descreve como executar um pacote e exibir as entradas de log que ele grava. Você pode exibir as entradas de log em tempo real. As entradas de log, gravadas na janela **Eventos de Log** , também podem ser copiadas e salvas para uma análise posterior.  
  
 Não é necessário gravar as entradas de log em um log para gravar as entradas na janela **Eventos de Log** .  
  
### <a name="to-view-log-entries"></a>Para exibir entradas de log  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No menu **SSIS** , clique em **Eventos de Log**. Opcionalmente, você pode exibir a janela **Eventos de Log** mapeando o comando View.LogEvents com uma combinação de teclas escolhidas por você na página **Teclado** da caixa de diálogo **Opções** .  
  
3.  No menu **Depurar** , clique em **Iniciar Depuração**.  
  
     Quando o runtime encontra os eventos e as mensagens personalizadas habilitadas para registro, as entradas de log para cada evento ou mensagem são gravadas na janela **Eventos de Log** .  
  
4.  No menu **Depurar** , clique em **Parar Depuração**.  
  
     As entradas de log permanecem disponíveis na janela **Eventos de Log** até que você execute novamente o pacote, execute um pacote diferente ou feche o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
5.  Exibir as entradas de log na janela **Eventos de Log** .  
  
6.  Opcionalmente, clique nas entradas de log para copiar, clique com o botão direito do mouse e clique em **Copiar**.  
  
7.  Opcionalmente, clique duas vezes em uma entrada de log e, na caixa de diálogo **Entrada de Log** , exiba os detalhes de uma única entrada de log.  
  
8.  Na caixa de diálogo **Entrada de Log** , clique nas setas para baixo e para cima para exibir a entrada de log anterior ou posterior e clique no ícone de cópia para copiar a entrada de log.  
  
9. Abra um editor de textos, cole e salve a entrada de log em um arquivo de texto.
