---
title: Habilitar log de pacote no SQL Server Data Tools | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], enabling
ms.assetid: b69a8593-5bb0-4f04-87d2-f8e7bd7eb4fc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8ef64ee84a90a74d2206fa8cc766e45b1a691566
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66059276"
---
# <a name="enable-package-logging-in-sql-server-data-tools"></a>Habilitar o log de pacote no SQL Server Data Tools
  Este procedimento descreve como adicionar registros a um pacote, configurar os registros no nível do pacote e salvar a configuração dos registros em um arquivo XML. Você só pode adicionar os registros no nível do pacote, mas o pacote não precisa executar os registros para habilitar os registros nos contêineres incluídos no pacote.  
  
> [!IMPORTANT]  
>  Se você implantar o projeto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no servidor [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , o nível de log definido para a execução do pacote substituirá o log do pacote configurado usando o [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 Por padrão, os contêineres de um pacote usam a mesma configuração de registro que o seu contêiner pai. Para obter informações sobre como definir opções de log para contêineres individuais, consulte [Configurar o registro em log por meio de um arquivo de configuração salvo](../../2014/integration-services/configure-logging-by-using-a-saved-configuration-file.md).  
  
### <a name="to-enable-logging-in-a-package"></a>Para habilitar registros em um pacote  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No menu **SSIS** , clique em **Registrar em Log**.  
  
3.  Selecione um provedor de log na lista **Tipo de provedor** e clique em **Adicionar**.  
  
4.  Na coluna **Configuração**, selecione um gerenciador de conexões ou clique em **\<New connection>** para criar um novo gerenciador de conexões do tipo apropriado para o provedor de logs. Dependendo do provedor selecionado, use um dos seguintes gerenciadores de conexões:  
  
    -   Para arquivos de texto, use um gerenciador de conexões de Arquivo. Para obter mais informações, consulte [File Connection Manager](connection-manager/file-connection-manager.md)  
  
    -   Para o [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)], use um Gerenciador de conexões de arquivo.  
  
    -   Para o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], use um gerenciador de conexões OLE DB. Para obter mais informações, consulte [OLE DB Connection Manager](connection-manager/ole-db-connection-manager.md).  
  
    -   Para o Log de Eventos de Windows, não faça nada. [!INCLUDE[ssIS](../includes/ssis-md.md)] cria o log automaticamente.  
  
    -   Para arquivos XML, use um gerenciador de conexões de Arquivo.  
  
5.  Repita as etapas 3 e 4 para cada log a ser usado no pacote.  
  
    > [!NOTE]  
    >  Um pacote pode utilizar mais de um log de cada tipo.  
  
6.  Opcionalmente, marque a caixa de seleção no nível de pacote, selecione os logs a serem atualizados no registro no nível do pacote e clique na guia **Detalhes** .  
  
7.  Na guia **Detalhes** , selecione **Eventos** para registrar todas as entradas de log ou desmarque **Eventos** para selecionar eventos individuais.  
  
8.  Opcionalmente, clique em **Avançado** para especificar quais informações registrar.  
  
    > [!NOTE]  
    >  Por padrão, todas informações são registradas.  
  
9. Na guia **Detalhes** , clique em **Salvar.** A caixa de diálogo **Salvar como** é exibida. Localize a pasta em que deseja salvar as configurações de registro, digite um nome de arquivo para as novas configurações de log e clique em **Salvar**.  
  
10. Clique em **OK**.  
  
11. Para salvar o pacote atualizado, clique em **Salvar Itens Selecionados** no menu **Arquivo** .  
  
## <a name="see-also"></a>Consulte Também  
 [Log de&#41; Integration Services &#40;SSIS](performance/integration-services-ssis-logging.md)   
 [Registro em Log do Integration Services &#40;SSIS&#41;](performance/integration-services-ssis-logging.md)  
  
  
