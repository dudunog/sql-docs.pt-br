---
title: Conceder permissões em um objeto de fonte de dados (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.roledesignerdialog.datasources.f1
helpviewer_keywords:
- read/write permissions
- user access rights [Analysis Services], data sources
- security [Analysis Services], data sources
- connection strings [Analysis Services]
- data sources [Analysis Services], security
ms.assetid: b4e302d3-c93b-4383-aa4a-37d15c129830
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4a869d2033adaa57be0ace522787332c03a69bcb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66074996"
---
# <a name="grant-permissions-on-a-data-source-object-analysis-services"></a>Conceder permissões em um objeto de fonte de dados (Analysis Services)
  Normalmente, a maioria dos usuários do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não precisa de acesso às fontes de dados subjacentes a um projeto do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Os usuários normalmente só consultam os dados no banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Porém, no contexto de mineração de dados, como executar previsões com base em um modelo de mineração, um usuário tem que unir os dados obtidos de um modelo de mineração com os dados fornecidos pelo usuário. Para conectar-se à fonte de dados que contém os dados fornecidos pelo usuário, o usuário usa uma consulta DMX (extensões DMX) que contém as cláusulas [OPENQUERY &#40;DMX&#41;](/sql/dmx/source-data-query-openquery) e [OPENROWSET &#40;DMX&#41;](/sql/dmx/source-data-query-openrowset).  
  
 Para executar uma consulta DMX que se conecta a uma fonte de dados, o usuário deve ter acesso ao objeto de fonte de dados do banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Por padrão, somente administradores de servidor ou de banco de dados têm acesso a objetos de fonte de dados. Isso significa que um usuário não pode acessar um objeto de fonte de dados, a menos que um administrador lhe conceda permissões.  
  
> [!IMPORTANT]  
>  Por razões de segurança, o envio de consultas DMX com o uso de uma cadeia de conexão aberta na cláusula OPENROWSET está desabilitado.  
  
## <a name="set-read-permissions-to-a-data-source"></a>Definir permissões de leitura a uma fonte de dados  
 A uma função de banco de dados podem ser concedidas permissões de leitura ou nenhuma permissão de acesso a um objeto de fonte de dados.  
  
1.  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se à instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], expanda **Funções** para o banco de dados adequado no Pesquisador de Objetos e clique em uma função de banco de dados (ou crie uma nova função de banco de dados).  
  
2.  No painel **Acesso a Fontes de Dados** , localize o objeto de fonte de dados na lista **Fonte de Dados** e escolha **Leitura** na lista **Acesso** da fonte de dados. Se essa opção não estiver disponível, verifique o painel **Geral** para ver se Controle Total está selecionado. Controle Total já está fornecendo a permissão, você não pode substituir as permissões na fonte de dados.  
  
## <a name="working-with-the-connection-string-used-by-a-data-source-object"></a>Trabalhando com a cadeia de caracteres de conexão usada por um objeto de fonte de dados  
 O objeto de fonte de dados contém a cadeia de caracteres de conexão que é usada para conectar-se à fonte de dados subjacente. Essa cadeia de caracteres de conexão pode especificar um dos seguintes itens:  
  
-   **Especificar um nome de usuário e uma senha**  
  
     Se a cadeia de caracteres de conexão que um objeto de fonte de dados usa especificar um nome e uma senha de usuário, convém criar vários objetos de fonte de dados, cada um com contas de usuário diferentes. A criação de vários objetos de fontes de dados permite aos usuários acessar certos objetos de fonte de dados e impede que esses usuários acessem outros objetos de fonte de dados. Esses outros objetos de fonte de dados podem ser usados pelo próprio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para processar objetos, como cubos e modelos de mineração.  
  
-   **Especificar a Autenticação do Windows**  
  
     Se a cadeia de caracteres de conexão que um objeto de fonte de dados usa especificar a Autenticação do Windows, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] conseguirá representar o cliente. Se a fonte de dados estiver em um computador remoto, os dois computadores deverão ser confiados para representação usando autenticação Kerberos ou a consulta normalmente falhará. Consulte [Configurar o Analysis Services para delegação restrita de Kerberos](../instances/configure-analysis-services-for-kerberos-constrained-delegation.md) para obter mais informações.  
  
     Se o cliente não permitir representação (pela propriedade Impersonation Level no OLE DB e outros componentes do cliente), o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tentará fazer uma conexão anônima à fonte de dados subjacente. Conexões anônimas a fontes de dados remotas raramente são bem-sucedidas, pois a maioria das fontes de dados não aceita conexões anônimas).  
  
## <a name="see-also"></a>Consulte Também  
 [Fontes de dados em modelos multidimensionais](data-sources-in-multidimensional-models.md)   
 [Propriedades da cadeia de conexão &#40;Analysis Services&#41;](../instances/connection-string-properties-analysis-services.md)   
 [Metodologias de autenticação com suporte pelo Analysis Services](../instances/authentication-methodologies-supported-by-analysis-services.md)   
 [Conceder acesso personalizado a dados de dimensão &#40;Analysis Services&#41;](grant-custom-access-to-dimension-data-analysis-services.md)   
 [Conceder permissões de cubo ou modelo &#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md)   
 [Conceder acesso personalizado a dados de célula &#40;Analysis Services&#41;](grant-custom-access-to-cell-data-analysis-services.md)  
  
  
