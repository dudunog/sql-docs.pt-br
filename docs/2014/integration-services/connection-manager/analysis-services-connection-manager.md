---
title: Gerenciador de conexões do Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], Analysis Services
- connection managers [Integration Services], Analysis Services
- Analysis Services connection manager
ms.assetid: 9f9cadad-a1d0-4db5-98f5-df5dbbec1be4
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 43dbe6d3a1a239f7a094189219de12953807bedb
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84921187"
---
# <a name="analysis-services-connection-manager"></a>Gerenciador de conexões do Analysis Services
  Um gerenciador de conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] habilita um pacote para se conectar a um servidor que executa um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou a um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que fornece acesso a dados de cubos e dimensões. Você só pode se conectar a um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] enquanto estiver desenvolvendo pacotes no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Em tempo de execução, os pacotes são conectados ao servidor e ao banco de dados em que foi implantado o projeto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 As tarefas Executar DDL do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e Processamento do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e os destinos, como o destino Treinamento do Modelo de Mineração de Dados, usam um gerenciador de conexões do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Para obter mais informações sobre bancos de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [Bancos de dados de modelo multidimensional &#40;SSAS&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/multidimensional-model-databases-ssas).  
  
## <a name="configuration-of-the-analysis-services-connection-manager"></a>Configuração do Gerenciador de Conexões do Analysis Services  
 Quando você adiciona um [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Gerenciador de conexões a um pacote, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] o cria um Gerenciador de conexões que é resolvido como uma [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] conexão em tempo de execução, define as propriedades do Gerenciador de conexões e adiciona o Gerenciador de conexões à `Connections` coleção no pacote. A propriedade `ConnectionManagerType` do gerenciador de conexões é definida como `MSOLAP100`.  
  
 Você pode configurar um gerenciador de conexões do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] das seguintes maneiras:  
  
-   Forneça uma cadeia de conexão configurada para atender aos requisitos do provedor Microsoft OLE Provider para Analysis Services.  
  
-   Especifique uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou o projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que deseja conectar.  
  
-   Se estiver se conectando a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], especifique o modo de autenticação.  
  
-   Indique se a conexão criada a partir do gerenciador de conexões será retida em tempo de execução.  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , clique em um dos seguintes tópicos:  
  
-   [Referência da interface do usuário da caixa de diálogo Adicionar Gerenciador de Conexões do Analysis Services](add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 Para obter informações sobre como configurar um gerenciador de conexões programaticamente, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionando conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
  
