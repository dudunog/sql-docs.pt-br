---
title: Gerenciar alterações em exibições de fonte de dados e fontes de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- modifying data sources
- modifying data source views
- data source views [Analysis Services], schema updates
- data sources [Analysis Services], schema updates
ms.assetid: 928c9f63-365a-43fd-9bbd-78828cc7e54d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ac551a708433e973ada499f0e7504bc75516e756
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074765"
---
# <a name="manage-changes-to-data-source-views-and-data-sources"></a>Gerenciar alterações em exibições da fonte de dados e em fontes de dados
  Quando o Assistente de Geração de Esquema é executado novamente, ele reutiliza a fonte de dados e a exibição da fonte de dados usadas na geração original. Se você adicionar uma fonte de dados ou uma exibição da fonte de dados, o assistente não a usará. Se você excluir a fonte de dados ou a exibição da fonte de dados original depois da geração inicial, execute o assistente desde o início. Também são excluídas todas as configurações anteriores do assistente. Todos os objetos existentes em um banco de dados subjacente que estavam vinculados a uma fonte de dados ou exibição de fonte de dados excluída serão tratados como objetos criados pelo usuário na próxima vez que você executar o Assistente de Geração de Esquema.  
  
 Se a exibição da fonte de dados não refletir o estado real do banco de dados subjacente no momento da geração, o Assistente de Geração de Esquema pode encontrar erros ao gerar o esquema para o banco de dados da área de assunto. Por exemplo, se a exibição da fonte de dados especificar que o tipo de dados de uma coluna é **int**, mas, na verdade, o tipo de dados da coluna for **string**, o Assistente de Geração de Esquema definirá o tipo de dados da chave estrangeira como **INT** de acordo com a exibição da fonte de dados e, em seguida, não conseguirá criar a relação, pois o tipo de dados real é **string**.  
  
 Por outro lado, se você alterar a cadeia de conexão da fonte de dados para um banco de dados diferente daquele usado na geração anterior, nenhum erro será gerado. O novo banco de dados será usado e nenhuma alteração será feita no banco de dados anterior.  
  
## <a name="see-also"></a>Consulte Também  
 [Entendendo a geração com incremento](understanding-incremental-generation.md)  
  
  
