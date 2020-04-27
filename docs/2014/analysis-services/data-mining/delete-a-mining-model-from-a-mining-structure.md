---
title: Excluir um modelo de mineração de uma estrutura de mineração | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], mining models
- deleting mining models
- removing mining models
- mining models [Analysis Services], deleting
ms.assetid: 9ab1506b-856e-4762-a663-5adf15ac71e3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d4e32a40946eb9e513ad22cd837773187843151
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66084777"
---
# <a name="delete-a-mining-model-from-a-mining-structure"></a>Excluir um modelo de mineração de uma estrutura de mineração
  Você pode excluir modelos de mineração usando o Designer de Mineração de Dados, o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]ou instruções DMX.  
  
### <a name="delete-a-mining-model-using-sql-server-data-tools"></a>Exclua um modelo de mineração usando as Ferramentas de Dados do SQL Server  
  
1.  Selecione a guia **Modelos de Mineração** no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Clique com o botão direito do mouse no modelo a ser excluído e selecione **Excluir**.  
  
     A caixa de diálogo **Excluir Objetos** é aberta.  
  
3.  Clique em **OK**.  
  
### <a name="delete-a-mining-model-using-sql-server-management-studio"></a>Exclua um modelo de mineração usando o SQL Server Management Studio  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra o banco de dados [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que contém o modelo.  
  
2.  Expanda **Estruturas de Mineração**e, depois, **Modelos de Mineração**.  
  
3.  Clique com o botão direito do mouse no modelo a ser excluído e selecione **Excluir**.  
  
     A exclusão do modelo não leva à exclusão dos dados de treinamento, mas apenas dos metadados e de quaisquer padrões criados durante o treinamento do modelo.  
  
### <a name="delete-a-mining-model-using-dmx"></a>Excluir um modelo de mineração usando DMX  
  
-   [DROP MINING MODEL &#40;DMX&#41;](/sql/dmx/drop-mining-model-dmx)  
  
## <a name="see-also"></a>Consulte Também  
 [Tarefas e instruções do modelo de mineração](mining-model-tasks-and-how-tos.md)  
  
  
