---
title: Configurar níveis de severidade para arquivos de log do DQS
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.admin.config.log.f1
helpviewer_keywords:
- severity levels
- log files,severity levels
- dqs log files,severity levels
- logging,severity levels
- configure severity levels
ms.assetid: 66ffcdec-4bf7-4dd5-a221-fd9baefeeef4
author: swinarko
ms.author: sawinark
ms.openlocfilehash: e8b2c1a1ec0bb6c1417fa68720f2d345c6bc4ccb
ms.sourcegitcommit: 6be9a0ff0717f412ece7f8ede07ef01f66ea2061
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85813833"
---
# <a name="configure-severity-levels-for-dqs-log-files"></a>Configurar níveis de severidade para arquivos de log do DQS

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Este tópico descreve como configurar níveis de severidade para várias atividades e módulos no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) usando o [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Níveis de severidade definem a intensidade de eventos que ocorrem no DQS. Eventos DQS têm os seguintes níveis de severidade, na ordem decrescente de severidade:  
  
-   **Fatal**: erros críticos em runtime que podem causar resultados severos/inesperados.  
  
-   **Erro**: outros erros em runtime.  
  
-   **Aviso**: avisos sobre eventos que podem resultar em um erro.  
  
-   **Informações**: informações sobre eventos em geral que não são um erro ou um aviso. Por exemplo, um processo de DQS foi iniciado.  
  
-   **Depuração**: informações detalhadas (detalhado) sobre o evento.  
  
 Ao configurar níveis de severidade para várias atividades e módulos do DQS, você está filtrando as informações a serem registradas e gravando no arquivo de log do DQS para a respectiva atividade ou módulo do DQS. Por exemplo, se você definir o nível de severidade de uma atividade do DQS como **Aviso**, apenas as mensagens de aviso e severidade mais alta (Erro e Fatal) associadas com a atividade do DQS serão registradas.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 É necessário ter a função dqs_administrator no banco de dados DQS_MAIN para configurar definições de severidade de log.  
  
##  <a name="configure-severity-levels-at-activity-level"></a><a name="ConfigureActivity"></a>Configurar níveis de severidade no nível de atividade  
 Você pode definir configurações de severidade de log para as seguintes atividades no DQS: gerenciamento de domínio, descoberta de conhecimento, política de correspondência, limpeza de dados, correspondência de dados e serviços de dados de referência. Para fazer isso:  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Execute o aplicativo Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Configuração**.  
  
3.  Em seguida, clique na guia **configurações de log** . As seguintes atividades do DQS são listadas para as quais você pode selecionar um nível de severidade: **Gerenciamento de domínio**, **descoberta de conhecimento**, **projeto de limpeza (ex. RDS)**, **política de correspondência e projeto de correspondência**e **RDS**.  
  
4.  Para obter uma atividade do DQS, selecione o nível de severidade a ser registrado. Você pode selecionar uma destas opções: **Fatal**, **Erro**, **Aviso**, **Informações**e **Depuração**. Por exemplo, se você deseja que apenas mensagens fatais sejam gravadas nos arquivos de log do DQS para a atividade de descoberta de base de dados de conhecimento, selecione **Fatal** na lista suspensa na atividade **Descoberta da Base de Dados de Conhecimento** .  
  
    > [!NOTE]  
    >  Por padrão, **Erro** é selecionado para cada uma das atividades. Isso implica que mensagens de erro e fatais sejam gravadas nos arquivos de log do DQS para cada atividade, por padrão.  
  
5.  Clique em **fechar**  
  
##  <a name="configure-severity-levels-at-module-level-advanced"></a><a name="ConfigureModule"></a>Configurar níveis de severidade no nível do módulo (avançado)  
 A seção **Avançado** na guia **Configurações de Log** permite que você defina configurações de severidade de log em um nível de módulo. Módulos são assemblies do sistema DQS que implementam várias funcionalidades em um recurso no DQS. Por exemplo, a atividade de gerenciamento de domínio contém várias funcionalidades, como a definição de regras de domínio, a definição de condições de regra, a definição de regras do domínio cruzado para domínios compostos e assim por diante.  
  
 Às vezes, o nível de granularidade no nível de atividade não é suficiente. Talvez você queira investigar um problema que está ocorrendo em um módulo específico de uma atividade. Convém ter uma opção para configurar severidade de log no nível de módulo para isolar e controlar o problema com mais precisão.  
  
 A configuração de severidade de log especificada no nível de atividade determina a configuração de severidade de log de todos os módulos que constituem a atividade. Entretanto, se houver qualquer conflito entre as configurações de severidade de log nos níveis de atividade e de módulo, as configurações de severidade no nível de módulo serão consideradas.  
  
> [!NOTE]
>  -   Por padrão, o módulo **Microsoft.Ssdqs.Core.Startup** está pré-configurado na seção **Avançado** com o nível de severidade definido como **Informações**. Isso ocorre para habilitar o log de eventos de severidade Informações e mais alta (Aviso, Erro e Fatal) que estão relacionados ao início e à interrupção de serviços do DQS.  
> -   Você deverá configurar níveis de severidade de log apenas no nível de módulo se for um usuário do DQS avançado que esteja familiarizado com os assemblies do sistema DQS.  
  
 Para configurar níveis de severidade de log no nível de módulo:  
  
1.  Na guia **Configurações de Log** , clique na seta para baixo em **Avançado** para exibir a área.  
  
2.  Na grade que aparece, selecione um nome do módulo da lista suspensa na coluna **Módulo** .  
  
3.  Depois, selecione um nível de severidade para o módulo da lista suspensa na coluna **Severidade** . Você pode selecionar uma destas opções: **Fatal**, **Erro**, **Aviso**, **Informações**e **Depuração**.  
  
     Por exemplo, na atividade de gerenciamento de domínio, você pode definir um nível de granularidade para a funcionalidade de definição de regra de domínio diferente da atividade de gerenciamento de domínio, selecionando o módulo **Microsoft.Ssdqs.DomainRules.Define** e um nível de severidade de log diferente. Da mesma forma, você pode definir um outro nível de granularidade para a funcionalidade de regra de domínio cruzado, selecionando o módulo **Microsoft.Ssdqs.DomainRules.Condition.CrossDomain** e um nível de severidade de log diferente.  
  
4.  Repita as etapas 2 e 3 para outros módulos, caso necessário. Você também pode adicionar ou excluir linhas à grade clicando nos ícones **Adicionar Módulo** e **Remover Módulo** .  
  
5.  Clique em **fechar**  
  
## <a name="see-also"></a>Consulte Também  
 [Definir configurações avançadas para arquivos de log do DQS](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)  
  
  
