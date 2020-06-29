---
title: Implantação de pacote (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, deploying
- deploying packages [Integration Services]
- SQL Server Integration Services packages, deploying
- deploying packages [Integration Services], about deploying packages
- packages [Integration Services], deploying
- SSIS packages, deploying
ms.assetid: 0f5fc7be-e37e-4ecd-ba99-697c8ae3436f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 32627eddf5e7a696decd549e9b87ebb5c3b9d031
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85423753"
---
# <a name="package-deployment-ssis"></a>Implantação de pacotes (SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui ferramentas e assistentes que simplificam a implantação de pacotes do computador de desenvolvimento para o servidor de produção ou para outros computadores.  
  
 Há quatro etapas no processo de implantação de pacotes:  
  
1.  A primeira etapa é opcional e envolve a criação de configurações de pacotes que atualizam as propriedades dos elementos dos pacotes em tempo de execução. As configurações são incluídas automaticamente quando se implantam os pacotes.  
  
2.  A segunda etapa é desenvolver o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para criar um utilitário de implantação de pacote. O utilitário de implantação para o projeto contém os pacotes que você quer implantar  
  
3.  A terceira etapa é copiar a pasta de implantação que foi criada quando você desenvolveu o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para o computador de destino.  
  
4.  A quarta etapa é executar no computador de destino o Assistente de Instalação de Pacotes para instalar os pacotes no sistema de arquivos ou em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obter informações sobre como criar um utilitário de implantação, consulte [Criar um utilitário de implantação](../create-a-deployment-utility.md).  
  
 Para obter informações sobre como implantar pacotes usando o utilitário de implantação, consulte [Implantar pacotes usando o utilitário de implantação](../deploy-packages-by-using-the-deployment-utility.md).  
  
 Para obter informações sobre como criar configurações de pacote, consulte [Criar configurações de pacote](../create-package-configurations.md).  
  
  
