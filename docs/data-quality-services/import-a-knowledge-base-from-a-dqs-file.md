---
title: Importar uma base de dados de conhecimento de um arquivo .dqs
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 9b9786fe-9e80-429a-afcb-dc3b3dd6f0b0
author: swinarko
ms.author: sawinark
ms.openlocfilehash: eb9487a3f633aa60dcfd66557d3fb9d33f62ad54
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85895430"
---
# <a name="import-a-knowledge-base-from-a-dqs-file"></a>Importar uma base de dados de conhecimento de um arquivo .dqs

[!INCLUDE [SQL Server - Windows only ASDBMI  ](../includes/applies-to-version/sqlserver.md)]

  Este tópico descreve como importar uma base de dados de conhecimento inteira de um arquivo de dados .dqs no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Você cria o arquivo de dados exportando uma base de dados de conhecimento existente do aplicativo [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] (consulte [exportar uma Base de dados de conhecimento para um arquivo. DQS](../data-quality-services/export-a-knowledge-base-to-a-dqs-file.md)).  
  
 O uso de um arquivo de dados .dqs para exportar o conteúdo de uma base de dados de conhecimento e, depois, importar o conteúdo para outra base de dados de conhecimento no mesmo [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] ou em outro [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] simplifica o processo de geração de conhecimento, economizando tempo e esforço. Isso permite que você compartilhe uma base de dados de conhecimento e seu conhecimento com outras pessoas, fazendo-as ganhar tempo. O arquivo .dqs conterá todas as informações da base de dados de conhecimento, inclusive domínios e a política de correspondência, exceto as informações de dados de referência anexadas. Os dados publicados e não publicados serão importados.  
  
 Um arquivo de dados .dqs é criptografado e, portanto, não pode ser exibido.  
  
 Quando você importa uma base de dados de conhecimento, pode usar o mesmo nome, a menos que o nome da base de dados de conhecimento já exista no aplicativo cliente; nesse caso, você deverá renomeá-la.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
 Para importar uma base de dados de conhecimento de um arquivo .dqs, é necessário já ter exportado a base de dados de conhecimento para o arquivo .dqs.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para importar uma base de dados de conhecimento de um arquivo de dados .dqs.  
  
##  <a name="import-a-knowledge-base-from-a-dqs-file"></a><a name="Import"></a>Importar uma base de dados de conhecimento de um arquivo. DQS  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Execute o aplicativo Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Nova base de dados de conhecimento**.  
  
3.  Digite um nome para a base de dados de conhecimento.  
  
4.  Clique na seta para baixo para **Criar base de dados de conhecimento de**e selecione **Importar do arquivo DQS**.  
  
5.  Para **Selecionar o arquivo de dados**, clique em **Procurar**.  
  
6.  Na caixa de diálogo **Importar do Arquivo de Dados** , vá para a pasta que contém o arquivo .dqs que você deseja importar e clique no nome do arquivo. Clique em **Abrir**.  
  
7.  Verifique que a base de dados de conhecimento e os domínios corretos são exibidos na lista **Domínio** .  
  
8.  Selecione a atividade a ser executada e clique em **Criar**.  
  
9. Na caixa de diálogo **Importar Base de Dados de Conhecimento** , verifique se a linha de status indica que a importação foi concluída. Clique em **OK**.  
  
10. Conclua as tarefas de descoberta de conhecimento, gerenciamento de domínio ou política de correspondência que você precisa executar e clique em **Concluir**.  
  
11. Clique em **Publicar** para publicar o conhecimento na base de dados de conhecimento ou em **Não** para não publicá-lo.  
  
12. Se você publicou a base de dados de conhecimento, clique em **OK**.  
  
13. Na home page do Data Quality Services, verifique se a base de dados de conhecimento está listada em **Bases de dados de conhecimento recentes**.  
  
##  <a name="follow-up-after-importing-a-knowledge-base-from-a-dqs-file"></a><a name="FollowUp"></a> Acompanhamento: após importar uma base de dados de conhecimento de um arquivo .dqs  
 Após importar uma base de dados de conhecimento de um arquivo .dqs, você poderá adicionar o conhecimento à base de dados de conhecimento ou usar a base de dados de conhecimento em um projeto de limpeza ou de correspondência, de acordo com o conteúdo da base de dados de conhecimento. Para obter mais informações, consulte [Executar a descoberta de conhecimento](../data-quality-services/perform-knowledge-discovery.md), [Gerenciando um domínio](../data-quality-services/managing-a-domain.md), [Gerenciando um domínio de composição](../data-quality-services/managing-a-composite-domain.md), [Criar uma política de conciliação](../data-quality-services/create-a-matching-policy.md), [Limpeza de dados](../data-quality-services/data-cleansing.md) ou [Correspondência de dados](../data-quality-services/data-matching.md).  
  
  
