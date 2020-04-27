---
title: Funções e permissões (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- security [Analysis Services], about security
- security [Analysis Services - multidimensional data], about security
ms.assetid: bb885447-868b-4686-853c-8241f63d4370
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f536ae91cde1301b9499b2d36957d25c877be9c7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66073059"
---
# <a name="roles-and-permissions-analysis-services"></a>Funções e permissões (Analysis Services)
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece um modelo de autorização com base em funções que concede acesso a operações, objetos e dados. Todos os usuários que acessam uma instância ou banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] devem fazer isso dentro do contexto de uma função.  
  
 Como um administrador de sistema do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , você é responsável pela concessão de associações à **função de administrador do servidor** que transmite acesso irrestrito às operações no servidor. Essa função tem permissões fixas e não pode ser personalizada. Por padrão, os membros do grupo Administradores local são automaticamente administradores do sistema do Analysis Services.  
  
 Aos usuários não administrativos que consultam ou processam dados são concedidos acesso por meio das **funções de banco de dados**. Tanto os administradores de sistema quanto os administrador de banco de dados podem criar as funções que descrevem níveis de acesso diferentes em um determinado banco de dados e, depois, atribuir a associação a cada usuário que solicitar acesso. Cada função tem um conjunto personalizado de permissões para acessar objetos e operações em um determinado banco de dados. Você pode atribuir permissões nestes níveis: banco de dados, objetos interiores como cubos e dimensões (mas não perspectivas) e linhas.  
  
 É prática comum criar funções e atribuir associação como operações separadas. Frequentemente, o designer de modelos adiciona funções durante a fase de design. Desse modo, todas as definições de função são refletidas nos arquivos de projeto que definem o modelo. A associação de função geralmente é distribuída depois, à medida que o banco de dados vai para produção, em geral pelos administradores de banco de dados que criam scripts que podem ser desenvolvidos, testados e executados como uma operação independente.  
  
 Toda a autorização é predicada em uma identidade de usuário do Windows válida. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa a autenticação do Windows exclusivamente para autenticar identidades de usuário. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]não fornece nenhum método de autenticação proprietário. Consulte [metodologias de autenticação com suporte pelo Analysis Services](../instances/authentication-methodologies-supported-by-analysis-services.md).  
  
> [!IMPORTANT]  
>  As permissões são aditivas para cada usuário ou grupo do Windows, em todas as funções no banco de dados. Se uma função nega a um usuário ou grupo permissão para executar certas tarefas ou exibir certos dados, mas outra função concede essa permissão a esse usuário ou grupo, o usuário ou o grupo terá permissão para executar a tarefa ou exibir os dados.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Autorizando o acesso a objetos e operações &#40;Analysis Services&#41;](authorizing-access-to-objects-and-operations-analysis-services.md)  
  
-   [Conceder permissões de banco de dados &#40;Analysis Services&#41;](grant-database-permissions-analysis-services.md)  
  
-   [Conceder permissões de cubo ou modelo &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md)  
  
-   [Conceder permissões de processo &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md)  
  
-   [Conceder permissões para ler definição em metadados de objetos &#40;Analysis Services&#41;](grant-read-definition-permissions-on-object-metadata-analysis-services.md)  
  
-   [Conceder permissões em um objeto de fonte de dados &#40;Analysis Services&#41;](grant-permissions-on-a-data-source-object-analysis-services.md)  
  
-   [Conceder permissões em estruturas e modelos de mineração de dados &#40;Analysis Services&#41;](grant-permissions-on-data-mining-structures-and-models-analysis-services.md)  
  
-   [Conceder permissões em uma dimensão &#40;Analysis Services&#41;](grant-permissions-on-a-dimension-analysis-services.md)  
  
-   [Conceder acesso personalizado a dados da dimensão &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md)  
  
-   [Conceder acesso personalizado a dados de célula &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Criar e Gerenciar Funções &#40;SSAS Tabular&#41;](../tabular-models/roles-ssas-tabular.md)  
  
  
