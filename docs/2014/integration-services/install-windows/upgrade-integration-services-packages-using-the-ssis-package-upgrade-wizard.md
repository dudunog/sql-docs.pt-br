---
title: Fazer upgrade de pacotes do Integration Services usando o Assistente para Upgrade de Pacote SSIS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, upgrading
- upgrading Integration Services packages
ms.assetid: 9359275a-48f5-4d1e-8ae7-e797759e3ccf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8ae4a90731e2204cbaf59a20b0b5eb3dacac9930
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85424943"
---
# <a name="upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard"></a>Atualizar pacotes do Integration Services usando o Assistente de Atualização de Pacote SSIS
  Você pode atualizar pacotes criados nas versões anteriores do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para o formato do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usado pelo [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece o Assistente de Atualização de Pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] para ajudar neste processo. Como é possível configurar o assistente para fazer backup dos pacotes originais, você poderá continuar usando esses pacotes caso tenha dificuldades com a atualização.  
  
 O Assistente de Atualização de Pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] é instalado junto com o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
> [!NOTE]  
>  O Assistente de Atualização de Pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] está disponível nas edições Standard, Enterprise e Developer do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obter mais informações sobre como atualizar pacotes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , veja [Atualizar pacotes do Integration Services](upgrade-integration-services-packages.md).  
  
 O restante deste tópico descreve como executar o assistente e fazer backup dos pacotes originais.  
  
## <a name="running-the-ssis-package-upgrade-wizard"></a>Executando o Assistente de Atualização de Pacote SSIS  
 Você pode executar o Assistente de Atualização de Pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ou do prompt de comando.  
  
#### <a name="to-run-the-wizard-from-sql-server-data-tools"></a>Para executar o assistente das Ferramentas de Dados do SQL Server  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], crie ou abra um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  No Gerenciador de Soluções, clique com o botão direito do mouse no nó **Pacotes SSIS** e clique em **Atualizar Todos os Pacotes** para atualizar todos os pacotes neste nó.  
  
    > [!NOTE]  
    >  Quando você abre um projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém pacotes do [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] ou do [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)], o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] abre automaticamente o Assistente de Atualização de Pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)].  
  
#### <a name="to-run-the-wizard-from-sql-server-management-studio"></a>Para executar o assistente do SQL Server Management Studio  
  
-   No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se ao [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], expanda o nó **Pacotes Armazenados** e clique com o botão direito do mouse no nó **Sistema de Arquivos** ou **MSDB** e clique em **Atualizar Pacotes**.  
  
#### <a name="to-run-the-wizard-at-the-command-prompt"></a>Para executar o assistente no prompt de comando  
  
-   No prompt de comando, execute o arquivo SSISUpgrade.exe na pasta **C:\Program Files\Microsoft SQL Server\120\DTS\Binn**  
  
## <a name="backing-up-the-original-packages"></a>Fazendo backup de pacotes originais  
 Para fazer backup de pacotes originais, esses pacotes originais e os pacotes atualizados devem ser armazenados na mesma pasta no sistema de arquivos. Dependendo do modo como você executa o assistente, o local de armazenamento pode ser selecionado automaticamente.  
  
-   Quando você executa o Assistente de Atualização de Pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] do [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], esse assistente armazena automaticamente os pacotes originais e atualizados na mesma pasta no sistema de arquivos.  
  
-   Quando você executa o Assistente de Atualização de Pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou no prompt de comando, pode especificar locais de armazenamento diferentes para os pacotes originais e atualizados. Para fazer backup de pacotes originais, não se esqueça de especificar que os pacotes originais e os pacotes atualizados devem ser armazenados na mesma pasta no sistema de arquivos. Se você especificar qualquer outra opção de armazenamento, o assistente não poderá fazer backup dos pacotes originais.  
  
 Quando o assistente faz backup dos pacotes originais, ele armazena uma cópia desses pacotes em uma pasta **SSISBackupFolder** . O assistente cria essa pasta **SSISBackupFolder** como uma subpasta da pasta que contém os pacotes originais e os pacotes atualizados.  
  
#### <a name="to-back-up-the-original-packages-in-sql-server-management-studio-or-at-the-command-prompt"></a>Para fazer backup dos pacotes originais no SQL Server Management Studio ou no prompt de comando  
  
1.  Salve os pacotes originais em um local no sistema de arquivos.  
  
    > [!NOTE]  
    >  A opção de backup no assistente funciona apenas com pacotes que foram armazenados no sistema de arquivos.  
  
2.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou no prompt de comando, execute o Assistente de Atualização de Pacote do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
3.  Na página **Selecionar Local de Origem** do assistente, defina a propriedade **Origem do pacote** como **Sistema de Arquivos**.  
  
4.  Na página **Selecionar Local de Destino** do assistente, selecione **Salvar no local de origem** para salvar os pacotes atualizados no mesmo local que os pacotes originais.  
  
    > [!NOTE]  
    >  A opção de backup no assistente está disponível somente quando os pacotes atualizados são armazenados na mesma pasta que os pacotes originais.  
  
5.  Na página **Selecionar Opções de Gerenciamento de Pacote** do assistente, selecione a opção **Fazer backup dos pacotes originais** .  
  
#### <a name="to-back-up-the-original-packages-in-sql-server-data-tools"></a>Para fazer backup dos pacotes originais nas Ferramentas de Dados do SQL Server  
  
1.  Salve os pacotes originais em um local no sistema de arquivos.  
  
2.  Na página **Selecionar Opções de Gerenciamento de Pacote** do assistente, selecione a opção **Fazer backup dos pacotes originais** .  
  
    > [!WARNING]  
    >  A opção **fazer backup de pacotes originais** não é exibida quando você abre um [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] projeto do ou no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] , que inicia automaticamente o assistente.  
  
3.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], execute o Assistente de Atualização de Pacote [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
  
