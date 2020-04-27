---
title: Exportar uma base de dados de conhecimento para um arquivo .dqs | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a324ead5-c8aa-4e26-abe3-ef415add00f8
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 1d1b2e20347cafb4717880de8fd224950f76b036
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65480730"
---
# <a name="export-a-knowledge-base-to-a-dqs-file"></a>Exportar uma base de dados de conhecimento para um arquivo .dqs
  Este tópico descreve como exportar uma base de dados de conhecimento inteira para um arquivo de dados .dqs no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Você pode exportar um domínio ou uma base de dados de conhecimento inteira para um arquivo de dados. Para obter informações sobre como exportar um domínio, consulte [Exportar um domínio para um arquivo .dqs](../../2014/data-quality-services/export-a-domain-to-a-dqs-file.md).  
  
 A exportação de uma base de dados de conhecimento para um arquivo .dqs e sua subsequente importação como outra base de dados de conhecimento simplifica o processo de geração de conhecimento, economizando tempo e esforço. Isso permite que você compartilhe uma base de dados de conhecimento e seu conhecimento com outras pessoas. O arquivo .dqs conterá todas as informações da base de dados de conhecimento, inclusive domínios e a política de correspondência, exceto as informações de dados de referência anexadas. Você deve anexar novamente os domínios requeridos aos serviços de dados de referência, se necessário, depois de importar o arquivo .dqs. Os dados publicados e não publicados em uma base de dados de conhecimento são exportados.  
  
 O arquivo de dados .dqs criado pelo processo de exportação é criptografado; portanto, o conteúdo não pode ser exibido.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Pré-requisitos  
 Para exportar uma base de dados de conhecimento para um arquivo de dados .dqs, você precisa ter criado e aberto uma base de dados de conhecimento. Você não precisa ter um arquivo .dqs para exportação; um arquivo será criado para você.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Você deve ter a função dqs_kb_editor ou dqs_administrator no banco de dados DQS_MAIN para exportar uma base de dados de conhecimento para um arquivo de dados .dqs.  
  
##  <a name="export-a-knowledge-base-to-a-dqs-file"></a><a name="Export"></a>Exportar uma base de dados de conhecimento para um arquivo. DQS  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Execute o aplicativo Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , abra uma base de dados de conhecimento na atividade Gerenciamento de Domínio.  
  
3.  Na página Gerenciamento de Domínio (com qualquer guia selecionada), clique no ícone **Exportar dados da Base de Dados de Conhecimento** , acima da lista de domínios, e clique em **Exportar Base de Dados de Conhecimento**. Outra alternativa é clicar com o botão direito do mouse na lista de **domínios** , passar o mouse sobre **Exportar**e clicar em **Exportar Base de Dados de Conhecimento**.  
  
4.  Na caixa de diálogo **Exportar para Arquivo de Dados**, vá para a pasta na qual você deseja salvar o arquivo, nomeie o arquivo ou mantenha o nome da base de dados de conhecimento, mantenha **Arquivos de Dados do DQS (\*.dqs)** como o tipo **Salvar como** e, em seguida, clique em **Salvar**.  
  
5.  Na caixa de diálogo **Exportar Base de Dados de Conhecimento** , verifica se a linha de status indica que a exportação foi concluída. Clique em **OK**.  
  
##  <a name="follow-up-after-exporting-a-domain-to-a-dqs-file"></a><a name="FollowUp"></a> Acompanhamento: após exportar um domínio para um arquivo .dqs  
 Após exportar uma base de dados de conhecimento para um arquivo .dqs, você poderá importar a base de dados de conhecimento para o mesmo [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] (com um novo nome) ou para outro [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
  
