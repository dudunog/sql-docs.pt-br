---
title: Implantar soluções de modelo usando XMLA | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- XML scripts [Analysis Services]
- scripts [Analysis Services], deployment
- deploying [Analysis Services], XML scripts
- Analysis Services deployments, XML scripts
ms.assetid: a8cb1837-fcac-4730-bea4-a72cf94d9f7c
author: minewiskan
ms.author: owend
ms.openlocfilehash: b78490c5ab6ad3ba5e52bb82d4be254e3f5f102b
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546874"
---
# <a name="deploy-model-solutions-using-xmla"></a>Implantar soluções de modelo usando XMLA
  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], a opção **CREATE To** do comando **Script de Banco de Dados como** cria um script XML de um banco de dados inteiro do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou de um de seus objetos constituintes. O script resultante pode ser executado em outro computador para recriar o esquema (metadados) do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . O script gera o banco de dados inteiro e não há nenhum mecanismo para atualizar de maneira incremental objetos já implantados ao usar o script. Depois de executar o script e implantar o banco de dados, o banco de dados recém-criado deve ser processado antes de os usuários poderem navegar nele.  
  
 Para obter mais informações sobre o comando **Script de Banco de Dados como** , consulte [Documentar e gerar scripts de um banco de dados do Analysis Services](document-and-script-an-analysis-services-database.md).  
  
## <a name="modifying-object-properties-in-the-xml-script"></a>Modificando as propriedades do objeto no script XML  
 Ao usar o comando **Script de Banco de Dados como** , você não pode modificar propriedades específicas (como o nome do banco de dados, as cadeias de caracteres de conexão da fonte de dados e as configurações de segurança) dos objetos do banco de dados. Essas propriedades devem ser modificadas manualmente no script depois que o script tiver sido gerado ou devem ser modificadas no banco de dados implantado depois de executar o script.  
  
> [!IMPORTANT]  
>  O script XML não conterá a senha se isso for especificado na cadeia de caracteres de conexão para uma fonte de dados ou para propósitos de representação. Considerando que a senha é necessária para propósitos de processamento nesse cenário, você precisará adicioná-la manualmente ao script XML antes de ele ser executado ou adicioná-la depois que o script XML tiver sido executado.  
  
## <a name="see-also"></a>Consulte Também  
 [Implantar soluções de modelo usando o assistente de implantação](deploy-model-solutions-using-the-deployment-wizard.md)   
 [Sincronizar bancos de dados do Analysis Services](synchronize-analysis-services-databases.md)  
  
  
