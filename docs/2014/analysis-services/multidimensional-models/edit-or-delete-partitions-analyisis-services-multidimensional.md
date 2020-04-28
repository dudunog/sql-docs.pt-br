---
title: Editar ou excluir partições (serviços Analysiss – multidimensional) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- modifying partitions
- partitions [Analysis Services], modifying
ms.assetid: fb7a64ca-d021-4926-b92d-83476fbc40a3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 089b99663753a9e9424e991ca5245c73ea577e49
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175755"
---
# <a name="edit-or-delete-partitions-analyisis-services---multidimensional"></a>Editar ou excluir partições (Analysis Services – Multidimensional)
  As partições do cubo são modificadas usando a guia **Partições** do Designer de Cubo no [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)]. A guia **Partições** lista as partições para todos os grupos de medidas de um cubo. Essa guia também lista as partições de write-back habilitadas para gravação.

 Para editar as partições de qualquer grupo de medidas, expanda o grupo de medidas na guia **partições** . as partições de um grupo de medidas são listadas por número ordinal em um formato de tabela com as colunas listadas na tabela a seguir.

 As configurações de um grupo de medidas vinculado devem ser editadas no cubo de origem.

 A exclusão de partições ocorre automaticamente quando você mescla uma partição de origem em uma partição de destino. A partição especificada como a origem é excluída após a conclusão da mesclagem. Você também pode excluir partições manualmente no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] ou na guia Partições no [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)]. Clique com o botão direito do mouse e escolha **Excluir**. Lembre-se de que, ao excluir uma partição, você também exclui dados e agregações. Como precaução, verifique se você tem um backup recente do banco de dados caso precise reverter essa etapa mais tarde.

> [!NOTE]
>  Outra opção é usar scripts XMLA que automatizam tarefas para criar, mesclar e excluir partições. O script XMLA pode ser criado e executado no [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], ou pacotes SSIS personalizados que são executados como uma tarefa agendada. Para obter mais informações, consulte [Automatizar tarefas administrativas do Analysis Services com SSIS](../instances/automate-analysis-services-administrative-tasks-with-ssis.md).

## <a name="partition-source"></a>Origem da partição
 Especifica a tabela de origem ou a consulta nomeada para a partição. Para alterar a tabela de origem, clique na célula e, em seguida, clique no botão de procura (**...**).

 ![Coluna de origem no painel Partição](../media/ssas-partitionsource.png "Coluna de origem no painel Partição")

 Se a partição for baseada em uma consulta, clique no botão Procurar (**...**) para editar a consulta. A propriedade **Origem** é editada para a partição. Para obter mais informações, consulte [Alterar uma origem de partição para usar uma tabela de fatos diferente](change-a-partition-source-to-use-a-different-fact-table.md).

 Você pode especificar uma tabela na exibição da fonte de dados que tenha a mesma estrutura da tabela de origem original (na fonte de dados externa do qual são recuperados dados). A origem pode estar em qualquer fonte de dados ou exibição da fonte de dados do banco de dados de cubo.

## <a name="storage-settings"></a>Configurações de armazenamento
 No Designer de Cubo, na guia Partições, você pode clicar em **Configurações de Armazenamento** para escolher uma das configurações padrão para o armazenamento MOLAP, ROLAP ou HOLAP, ou para personalizar configurações para um modo de armazenamento e o cache pró-ativo. O padrão é MOLAP pois ele apresenta o desempenho mais rápido de consulta. Para obter mais informações sobre cada configuração, consulte [Definir armazenamento de partição &#40;Analysis Services – Multidimensional&#41;](set-partition-storage-analysis-services-multidimensional.md).

 O armazenamento pode ser configurado separadamente para cada partição de cada grupo de medidas em um cubo. Você também pode definir configurações de armazenamento padrão para um cubo ou grupo de medidas. O armazenamento é configurado na guia **Partições** do Assistente para Cubos.

## <a name="see-also"></a>Consulte Também
 [Criar e gerenciar uma partição Local &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md) [de criação de agregações &#40;partições de mesclagem Analysis Services multidimensionais](designing-aggregations-analysis-services-multidimensional.md) [no&#41;Analysis Services SSAS – &#40;multidimensional](merge-partitions-in-analysis-services-ssas-multidimensional.md)


