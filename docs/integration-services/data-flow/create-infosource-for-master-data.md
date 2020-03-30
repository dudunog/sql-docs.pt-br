---
title: Criar InfoSource para dados mestre | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b52a9a89-8380-4a02-8a83-dcfb46ae860e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1fb9be98dbbdf2935fe79c6f579be7ab0e357624
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71293203"
---
# <a name="create-infosource-for-master-data"></a>Criar InfoSource para Dados Mestres

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Use a caixa de diálogo **Criar InfoSource para os Dados Mestres** para criar um novo InfoSource para dados mestres no sistema SAP Netweaver BW.  
  
 Você pode abrir a caixa de diálogo **Criar InfoSource para os Dados Mestres** da página **Gerenciador de Conexões** do **Editor de Destino SAP BW**. Para obter mais informações sobre o destino SAP BW, consulte [SAP BW Destination](../../integration-services/data-flow/sap-bw-destination.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
 **Para abrir a caixa de diálogo Criar InfoSource para os Dados Mestres**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o destino SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes no destino SAP BW.  
  
3.  No **Editor de Destino SAP BW**, clique em **Gerenciador de Conexões** para abrir a página **Gerenciador de Conexões** do editor.  
  
4.  Na página **Gerenciador de Conexões** , na caixa de grupo **Criar Objetos SAP BW** , selecione **InfoSource**e clique em **Criar**.  
  
5.  Na caixa de diálogo **Criar InfoSource** , selecione **Dados Mestres**e clique em **OK**.  
  
## <a name="options"></a>Opções  
 **Nome do InfoObject**  
 Digite o nome do InfoObject no qual o novo InfoSource deve ser baseado.  
  
 **Pesquisar**  
 Pesquisar InfoObject. Essa opção abre a caixa de diálogo **Pesquisar InfoObject** na qual é possível selecionar o InfoObject. Para obter mais informações sobre essa caixa de diálogo, consulte [Look Up InfoObject](../../integration-services/data-flow/look-up-infoobject.md).  
  
 Depois de selecionar um InfoObject, o componente preenche a caixa de texto **Nome do InfoObject** com o nome do InfoObject selecionado.  
  
 **Novo**  
 Criar um novo InfoObject. Essa opção abre a caixa de diálogo **Criar Novo InfoObject** na qual é possível criar o novo InfoObject. Para obter mais informações sobre essa caixa de diálogo, consulte [Create New InfoObject](../../integration-services/data-flow/create-new-infoobject.md).  
  
 Depois de criar um InfoObject, o componente preenche a caixa de texto **Nome do InfoObject** com o nome do novo InfoObject.  
  
 **Descrição breve**  
 Insira uma descrição curta para o novo InfoSource.  
  
 **Descrição longa**  
 Insira uma descrição longa para o novo InfoSource.  
  
 **Sistema de origem**  
 Selecione o sistema de origem a ser associado ao novo InfoSource.  
  
 **Aplicativo**  
 Insira o nome do aplicativo cliente a ser associado ao novo InfoSource.  
  
 **Atributos**  
 Indica que os dados mestres consistem em atributos.  
  
 **Textos**  
 Indica que os dados mestres consistem em atributos.  
  
 **Salvar e Ativar**  
 Salvar e ativar o novo InfoSource.  
  
## <a name="see-also"></a>Consulte Também  
 [Criar InfoSource](../../integration-services/data-flow/create-infosource.md)   
 [Ajuda F1 do Microsoft Connector para SAP BW](../../integration-services/microsoft-connector-for-sap-bw-f1-help.md)  
  
  
