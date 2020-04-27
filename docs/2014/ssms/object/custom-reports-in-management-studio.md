---
title: Relatórios personalizados no Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.summary.new.custom.report.f1
helpviewer_keywords:
- SQL Server Management Studio [SQL Server], custom reports
ms.assetid: 1ba3f758-f39b-4f5f-91ca-516cedc78979
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e02e5f55032f7a5d4e11e1ee4c908e84a83e00f8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68188285"
---
# <a name="custom-reports-in-management-studio"></a>Relatórios personalizados no Management Studio
  No [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], muitos nós do Pesquisador de Objetos exibem um conjunto de relatórios padrão criados pela [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Esses relatórios resumem as informações de servidor que costumam ser solicitadas. Começando com o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 2, os administradores podem executar relatórios personalizados que foram criados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
## <a name="implementation"></a>Implementação  
 Relatórios personalizados são armazenados como arquivos de definição de relatório (.rdl) e criados na linguagem RDL (Report Definition Language). A RDL contém informações de layout e recuperação de dados de um relatório no formato XML. Ela consiste em um esquema aberto. Os desenvolvedores podem estender a RDL com atributos e elementos adicionais. Os relatórios podem executar qualquer instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] válida dentro do relatório.  
  
 Se o Pesquisador de Objetos estiver conectado a um servidor, os relatórios personalizados poderão ser executados no contexto da seleção atual do Pesquisador de Objetos se fizerem referência a parâmetros de relatório desse nó. Desse modo, um relatório pode usar o contexto atual (como o banco de dados atual) ou um contexto consistente (especificando, por exemplo, um banco de dados designado como parte da instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] contida no relatório personalizado).  
  
## <a name="running-a-custom-report"></a>Executando um relatório personalizado  
 É possível executar um relatório personalizado no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] das seguintes maneiras:  
  
-   Clique com o botão direito do mouse em um nó do Pesquisador de Objetos, aponte para **Relatórios** e clique em **Relatórios Personalizados**. Na caixa de diálogo **Abrir Arquivo** , localize uma pasta contendo arquivos .rdl e abra o arquivo de relatório apropriado.  
  
-   Clique com o botão direito do mouse em um nó do Pesquisador de Objetos, aponte para **Relatórios**, aponte para **Relatórios Personalizados**e selecione um relatório personalizado na lista de arquivos usados mais recentemente.  
  
## <a name="limitations"></a>Limitações  
 Quando trabalhar com relatórios personalizados, leve em consideração estas limitações:  
  
-   Para evitar a execução não intencional de código mal-intencionado, não é possível configurar o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para executar um relatório automaticamente, mesmo que o sistema de arquivos esteja configurado para associar arquivos .rdl ao [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Relatórios não podem ser executados programaticamente no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e não podem ser executados da linha de comando através do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
-   Você pode executar relatórios personalizados em um contexto que não produza os valores esperados. Por exemplo, você pode executar um relatório sobre replicação no contexto de um banco de dados que não está envolvido na replicação ou pode executar um relatório como um usuário que não tem permissão para acessar as informações necessárias para gerar um relatório preciso. O criador do relatório personalizado é responsável pela validade da estrutura do relatório e seu contexto.  
  
-   Não é possível adicionar um relatório personalizado à lista de relatórios padrão.  
  
-   O código processado pelo relatório pode afetar o desempenho do servidor.  
  
-   Relatórios personalizados não darão suporte a sub-relatórios.  
  
-   O texto de comando de cada consulta no relatório não deve ser definido por meio de uma expressão.  
  
-   Todos os parâmetros de consulta usados em um comando (consulta) só podem fazer referência a um único parâmetro de relatório e não podem usar operadores de expressão.  
  
-   Só existe suporte para tipos de comandos de relatório (consultas) Texto e Procedimento Armazenado.  
  
-   A estrutura de relatório não oferece nenhum escape de parâmetros para consultas. Os autores das consultas devem ter certeza de que suas consultas estão livres de ataques de injeção SQL.  
  
## <a name="managing-custom-reports"></a>Gerenciando relatórios personalizados  
 Os usuários que têm muitos relatórios personalizados devem organizá-los utilizando pastas do sistema de arquivos com permissões adequadas no sistema de arquivos NTFS.  
  
## <a name="permissions"></a>Permissões  
 Relatórios personalizados executados usando as permissões do usuário atual. Para impedir que um usuário mal-intencionado altere as consultas executadas pelo relatório, as permissões na pasta do sistema de arquivos que contém os arquivos de relatório devem ser definidas com acesso restrito.  
  
 O usuário e a conta utilizada pelo serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exigem acesso de leitura na pasta do sistema de arquivos que contém os arquivos de relatório.  
  
 Qualquer comando [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] válido pode ser inserido em um relatório, mas o comando não será executado.  
  
> [!CAUTION]  
>  Qualquer instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] válida pode ser inserida em um relatório e executada dele. Quando um relatório é executado utilizando-se uma conta de usuário com altos privilégios, qualquer uma dessas instruções inseridas pode ser executada sem desafio.  
  

  
## <a name="see-also"></a>Consulte Também  
 [Adicionar um relatório personalizado a Management Studio](add-a-custom-report-to-management-studio.md)   
 [Cancelar supressão de executar avisos de relatório personalizado](unsuppress-run-custom-report-warnings.md)   
 [Usar relatórios personalizados com propriedades de nó do Pesquisador de Objetos](use-custom-reports-with-object-explorer-node-properties.md)  
  
  
