---
title: Tarefa Criar Cluster do Azure HDInsight | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpcreatecltask.f1
- sql11.dts.designer.afpcreatecltask.f1
ms.assetid: a8ec413a-38d3-45df-887e-6f5f4d9f8465
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a2e0d73034bc131b0cc65d475f00efd4f54612b3
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85433913"
---
# <a name="azure-hdinsight-create-cluster-task"></a>Tarefa Criar Cluster do Azure HDInsight
A **Tarefa Criar Cluster do Azure HDInsight** permite que um pacote do SSIS crie um cluster do Azure HDInsight na assinatura e grupo de recursos do Azure especificados.
  
> [!NOTE]  
> - Criar um novo cluster HDInsight pode levar entre 10 e 20 minutos.  
> - Há um custo associado à criação e execução de um cluster Azure HDInsight. Consulte [Preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/) para obter mais detalhes.  
  
Para adicionar uma **Tarefa Criar Cluster do Azure HDInsight**, arraste e solte-a no Designer SSIS e clique duas vezes ou, com o botão direito do mouse, clique em **Editar** para ver a caixa de diálogo **Editor de Tarefa Criar Cluster do Azure HDInsight** a seguir.  
  
A tabela a seguir fornece uma descrição para os campos nessa caixa de diálogo.  
  
|||  
|-|-|  
|**Campo**|**Descrição**|  
|AzureResourceManagerConnection|Selecione um Gerenciador de Conexão do Azure Resource Manager existente ou crie um novo que será usado para criar o cluster HDInsight.|  
|AzureStorageConnection|Selecione um Gerenciador de conexão de armazenamento do Azure existente ou crie um novo, relacionado a uma conta de armazenamento do Azure, que será associado com o cluster HDInsight.|
|SubscriptionId|Especifique a ID da assinatura na qual o cluster HDInsight será criado.|
|ResourceGroup|Especifique o grupo de recursos do Azure no qual o cluster HDInsight será criado.|
|Location|Especifique o local do cluster HDInsight. O cluster deve ser criado no mesmo local que a conta de Armazenamento do Azure especificada.|  
|ClusterName|Especifique um nome para o cluster HDInsight que será criado.|  
|clusterSize|Especifique o número de nós a serem criados no cluster.|  
|BlobContainer|Especifique o nome do contêiner de armazenamento padrão a ser associado ao cluster HDInsight.|  
|UserName|Especifique o nome de usuário a ser usado para conectar-se ao cluster HDInsight.|  
|Senha|Especifique a senha a ser usada para conectar-se ao cluster HDInsight.|
|SshUserName|Especifique o nome de usuário usado para acessar remotamente o cluster HDInsight usando SSH.|
|SshPassword|Especifique a senha usada para acessar remotamente o cluster HDInsight usando SSH.|
|FailIfExists|Especifique se a tarefa deve falhar ou não caso o cluster já exista.|  
  
> [!NOTE]  
> O local do cluster HDInsight e da conta de Armazenamento do Azure deve ser o mesmo.
