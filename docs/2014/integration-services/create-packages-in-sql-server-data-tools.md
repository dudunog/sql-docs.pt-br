---
title: Criar pacotes no SQL Server Data Tools | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, creating
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
ms.assetid: bb3c085b-1458-49fa-8348-6a76b6e97ea6
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 2bbf6720e5532c2e3691289bf2b801fc86e6452b
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84917282"
---
# <a name="create-packages-in-sql-server-data-tools"></a>Copiar pacotes nas Ferramentas de Dados do SQL Server
  Os pacotes criados no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] por meio do [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer são salvos no sistema de arquivos. Para salvar um pacote no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ou no repositório de pacotes, salve uma cópia do pacote. Para obter mais informações, consulte [Salvar uma cópia de um pacote](../../2014/integration-services/save-a-copy-of-a-package.md).  
  
 No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], você pode criar um novo pacote usando um dos métodos a seguir:  
  
-   Use o modelo de pacote incluído no [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
-   Criar um modelo personalizado  
  
     Para usar pacotes personalizados como modelos na criação de novos pacotes, você simplesmente os copia para a pasta DataTransformationItems. Por padrão, esta pasta está em C:\Arquivos de Programas\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject.  
  
-   Copie um pacote existente.  
  
     Se pacotes existentes incluírem a funcionalidade que deseja reutilizar, você pode criar o fluxo de controle e fluxos de dados no novo pacote mais rapidamente copiando e colando os objetos de outros pacotes. Para obter mais informações sobre como usar o copiar e colar em projetos [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , consulte [Reutilizar objetos de pacote](reuse-of-package-objects.md).  
  
     Se você criar um novo pacote copiando e colando um pacote existente, ou usando um pacote personalizado como modelo, o nome e GUID do pacote existente também serão copiados. Você deve atualizar o nome e GUID do novo pacote, para ajudar a diferenciá-lo do pacote originalmente copiado. Por exemplo, caso pacotes tenham o mesmo GUID, é mais difícil identificar o pacote ao quais os dados de log pertencem. Você pode gerar o GUID na propriedade `ID` e atualizar o valor da propriedade `Name` usando a janela Propriedades no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para obter mais informações, consulte [Definir as propriedades do pacote](set-package-properties.md) e [Utilitário dtutil](dtutil-utility.md).  
  
-   Use um pacote personalizado que você designou como um modelo.  
  
-   Executar o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
     O Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cria um pacote completo para uma importação ou exportação simples. Este assistente configura as conexões, a origem e o destino e adiciona as transformações de dados necessárias para permitir a execução imediata da importação ou exportação. Se preferir, você pode salvar o pacote para executá-lo novamente depois ou refinar e aprimorar o pacote no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Porém, se o pacote for salvo, você deverá adicioná-lo a um projeto existente do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] antes de alterar o pacote ou executá-lo no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
 Os procedimentos a seguir descrevem como criar ou excluir um pacote no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 Para obter um vídeo que demonstre como criar um pacote básico usando o modelo de pacote padrão, consulte [Criando um pacote básico (vídeo do SQL Server)](https://go.microsoft.com/fwlink/?LinkId=131023).  
  
### <a name="to-create-a-package-in-sql-server-data-tools-using-the-package-template"></a>Para criar um pacote nas Ferramentas de Dados do SQL Server usando o modelo de pacote  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no qual você deseja criar um pacote.  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse na pasta **Pacotes SSIS** e clique em **Novo Pacote SSIS**.  
  
3.  Se desejar, adicione o fluxo de controle, as tarefas do fluxo de dados e os manipuladores de eventos ao pacote. Para obter mais informações, consulte [Fluxo de Controle](control-flow/control-flow.md), [Fluxo de Dados](data-flow/data-flow.md) e [Manipuladores de Eventos do Integration Services &#40;SSIS&#41;](integration-services-ssis-event-handlers.md).  
  
4.  No menu **Arquivo** , clique em **Salvar Itens Selecionados** para salvar o novo pacote.  
  
    > [!NOTE]  
    >  Você pode salvar um pacote vazio.  
  
  
