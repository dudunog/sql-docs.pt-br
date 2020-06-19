---
title: Editor de Origem SAP BW (página Saída de Erro) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b6e23b0c-949a-46d1-8424-4dc3d9035e79
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c3c94fead420fcd20978d662f2849369018af50e
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84914316"
---
# <a name="sap-bw-source-editor-error-output-page"></a>Editor de Origem de SAP BW (página Saída de Erro)
  Use a página **Saída de Erro** do **Editor de Origem SAP BW** , para selecionar opções de tratamento de erro e definir propriedades em colunas de saída de erros.  
  
 Para saber mais sobre o componente de origem do SAP BW do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 para SAP BW, consulte [Origem SAP BW](sap-bw-source.md).  
  
> [!IMPORTANT]  
>  A documentação do Microsoft Connector 1.1 for SAP BW supõe familiaridade com o ambiente do SAP Netweaver BW. Para obter mais informações sobre o SAP Netweaver BW ou para obter informações sobre como configurar objetos e processos do SAP Netweaver BW, consulte sua documentação do SAP.  
  
> [!IMPORTANT]  
>  A extração de dados do SAP Netweaver BW exige licenciamento SAP adicional. Verifique esses requisitos com a SAP.  
  
 **Para abrir a página Saída de Erro**  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém a origem SAP BW.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na fonte SAP BW.  
  
3.  No **Editor de Origem SAP BW**, clique em **Saída do Erro** para abrir a página **Saída do Erro** do editor.  
  
## <a name="options"></a>Opções  
  
> [!NOTE]  
>  Se você não souber todos os valores necessários para configurar a origem, talvez precise perguntar ao administrador do SAP.  
  
 **Entrada ou Saída**  
 Exibe o nome da fonte de dados.  
  
 **Coluna**  
 Exiba as colunas externas (origem) selecionadas na página **Colunas** da caixa de diálogo **Editor de Origem SAP BW** . Para obter mais informações sobre essa caixa de diálogo, consulte [Editor de Origem SAP BW &#40;Página Colunas&#41;](sap-bw-source-editor-columns-page.md).  
  
 **Erro**  
 Especifique o que o componente de origem SAP BW deve fazer quando há um erro: ignorar a falha, redirecionar a linha ou falhar o componente.  
  
 **Truncation**  
 Especifique o que o componente de origem SAP BW deve fazer quando ocorre um truncamento: ignorar a falha, redirecionar a linha ou falhar o componente.  
  
 **Descrição**  
 Exiba a descrição do erro.  
  
 **Definir este valor para células selecionadas**  
 Especifique o que o componente de origem SAB BW deve fazer a todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
 **Aplicar**  
 Aplique a opção de tratamento de erros às células selecionadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Editor de Origem SAP BW &#40;Página Gerenciador de Conexões&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [Editor de Origem SAP BW &#40;Página Colunas&#41;](sap-bw-source-editor-columns-page.md)   
 [Editor de Origem SAP BW &#40;Página Avançado&#41;](sap-bw-source-editor-advanced-page.md)   
 [Ajuda F1 do Microsoft Connector 1.1 for SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
