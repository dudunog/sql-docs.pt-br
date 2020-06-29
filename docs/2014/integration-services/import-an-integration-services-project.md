---
title: Importar um projeto de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3301c328-b0f5-4517-915c-93713413e453
author: chugugrace
ms.author: chugu
ms.openlocfilehash: af91900ce22ecd3d42a8d83557e1780e30c5ca73
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85436843"
---
# <a name="import-an-integration-services-project"></a>Importar um projeto do Integration Services
  Use o **Assistente de Projeto de Importação** do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para criar um projeto de um arquivo de implantação existente (.ispac) ou de um projeto implantado no catálogo do Integration Services. Este recurso é especialmente útil quando você não tiver a cópia original do projeto, mas desejar criar um de um arquivo .ispac ou catálogo SSISDB.  
  
### <a name="to-import-a-project"></a>Para importar um projeto  
  
1.  No [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] , clique em **novo**  >  **projeto** no menu **arquivo** .  
  
2.  Na área **Modelos Instalados** da janela **Novo Projeto** , expanda **Business Intelligence**e clique em **Integration Services**.  
  
3.  Selecione **Assistente de Importação de Projeto do Integration Services** da lista de tipos de projetos.  
  
4.  Digite o nome do novo projeto a ser criado na caixa de texto **Nome** .  
  
5.  Digite o caminho ou o local para o projeto na caixa de texto **Localização** ou clique em **Procurar** para selecionar um.  
  
6.  Digite um nome para a solução na caixa de texto **Nome da solução** .  
  
7.  Clique em **OK** para iniciar a caixa de diálogo **Assistente de Importação de Projeto do Integration Services** .  
  
8.  Clique em **Avançar** para alternar para a página **Selecionar Origem** .  
  
9. Se você estiver importando de um arquivo **.ispac** , digite o caminho incluindo o nome de arquivo na caixa de texto **Caminho** . Clique em **Procurar** para navegar até a pasta onde você deseja que a solução seja armazenada e digite o nome do arquivo na caixa de texto **Nome de arquivo** e clique em **Abrir**.  
  
     Se você estiver importando de um **Catálogo do Integration Services**, digite o nome da instância de banco de dados na caixa de texto **Nome do servidor** ou clique em **Procurar** e selecione a instância de banco de dados que contém o catálogo.  
  
     Clique em **Procurar** ao lado da caixa de texto **Caminho** , expanda a pasta no catálogo, selecione o projeto que você deseja importar e clique em **OK**.  
  
     Clique em **Avançar** para alternar para a página **Revisar** .  
  
10. Revise as informações e clique em **Importar** para criar um projeto baseado no projeto existente que você selecionou.  
  
11. Opcional: clique em **Salvar Relatório** para salvar os resultados em um arquivo  
  
12. Clique em **Fechar** para fechar a caixa de diálogo **Assistente de Importação de Projeto do Integration Services** .  
  
  
