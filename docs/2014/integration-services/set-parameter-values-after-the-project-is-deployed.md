---
title: Definir valores de parâmetro depois que o projeto for implantado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: c9dcca4d-f1a0-45ec-b078-f4d372589baf
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 910de9d388e60ae3664153e2f6cb3bb5203b289c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66055774"
---
# <a name="set-parameter-values-after-the-project-is-deployed"></a>Definir valores de parâmetros depois que o projeto foi implantado
  O Assistente de Implantação permite definir valores de parâmetros padrão de servidor ao implantar seu projeto no catálogo. Depois que seu projeto estiver no catálogo, você pode usar o Pesquisador de Objetos do SQL Server Management Studio (SSMS) ou o Transact-SQL para definir valores padrão de servidor.  
  
### <a name="to-set-server-defaults-with-ssms-object-explorer"></a>Para definir padrões de servidor com Pesquisador de Objetos do SSMS:  
  
1.  Selecione e clique com o botão direito do mouse no projeto sob o nó **Integration Services**.  
  
2.  Clique em **Propriedades** para abrir janela da caixa de diálogo **Propriedades do Projeto**.  
  
3.  Abra a página de parâmetros com um clique em **Parâmetros** sob **Selecionar uma página**.  
  
4.  Selecione o parâmetro desejado na lista **Parâmetros**. Observação: a coluna **Contêiner** ajuda a distinguir os parâmetros de projeto dos parâmetros de pacote.  
  
5.  Na coluna **Valor**, especifique o valor do parâmetro padrão de servidor desejado.  
  
 Para definir padrões de servidor com Transact-SQL, use o procedimento armazenado [catalog.set_object_parameter_value &#40;Banco de Dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-object-parameter-value-ssisdb-database). Para exibir os padrões atuais de servidor, consulte a exibição [catalog.object_parameters &#40;Banco de Dados SSISDB&#41;](/sql/integration-services/system-views/catalog-object-parameters-ssisdb-database). Para apagar um valor padrão de servidor, use o procedimento armazenado [catalog.clear_object_parameter_value &#40;Banco de Dados SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-clear-object-parameter-value-ssisdb-database).  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services parâmetros&#41; &#40;SSIS](integration-services-ssis-package-and-project-parameters.md)  
  
  
