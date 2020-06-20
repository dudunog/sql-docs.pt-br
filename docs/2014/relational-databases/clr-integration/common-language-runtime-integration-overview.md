---
title: Visão geral da integração CLR (Common Language Runtime) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- managed code [SQL Server]
- common language runtime [SQL Server], about CLR integration
- cross-language integration
- integrating CLR [SQL Server]
- .NET Framework [SQL Server], common language runtime
- code access security [CLR integration]
- managed code [SQL Server], CLR integration
ms.assetid: 7be9e644-36a2-48fc-9206-faf59fdff4d7
author: rothja
ms.author: jroth
ms.openlocfilehash: 5d858dde63a43a0b929f3e091d0c0b295b268f5b
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970676"
---
# <a name="common-language-runtime-clr-integration-overview"></a>Visão geral da integração CLR (Common Language Runtime)
  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]agora apresenta a integração do componente Common Language Runtime (CLR) do .NET Framework para [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows. O CLR fornece código gerenciado com serviços como integração entre idiomas, segurança de acesso do código, gerenciamento do tempo de vida de objetos e suporte à depuração e à criação de perfis. Para usuários e desenvolvedores de aplicativos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], a integração CLR significa que agora você pode gravar procedimentos armazenados, gatilhos, tipos definidos pelo usuário, funções definidas pelo usuário (escalares e com valor de tabela) e funções de agregação definidas pelo usuário usando qualquer linguagem do .NET Framework, incluindo o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic .NET e o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C#. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] inclui o .NET Framework 4 pré-instalado.  
  
 Estes são alguns dos principais benefícios dessa integração:  
  
-   **Um modelo de programação melhor.** Em muitos aspectos, as linguagens do .NET Framework são mais sofisticadas do que o Transact-SQL, oferecendo construções e recursos não disponíveis anteriormente aos desenvolvedores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os desenvolvedores também podem aproveitar a potência da Biblioteca do .NET Framework, que fornece um abrangente conjunto de classes que podem ser usadas para resolver problemas de programação de forma rápida e eficiente.  
  
-   **Proteção e segurança aprimoradas.** O código gerenciado é executado em um ambiente CLR, hospedado pelo Mecanismo de Banco de Dados. Isso é aproveitado pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para fornecer uma alternativa mais segura e protegida para os procedimentos armazenados estendidos disponíveis em versões anteriores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   **Capacidade de definir tipos de dados e funções de agregação.** Os tipos definidos pelo usuário e as agregações definidas pelo usuário são dois novos objetos de banco de dados gerenciados que ampliam os recursos de armazenamento e consulta do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   **Desenvolvimento simplificado por meio de um ambiente padronizado.** O desenvolvimento do banco de dados será integrado em versões futuras do ambiente de desenvolvimento do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Studio .NET. Os desenvolvedores usam as mesmas ferramentas para desenvolver e depurar scripts e objetos do banco de dados que usavam para escrever componentes e serviços de camada intermediária ou da camada de cliente do .NET Framework.  
  
-   **Potencial para desempenho e escalabilidade aprimorada.** Em muitas situações, os modelos de compilação e execução da linguagem do .NET Framework oferecem um desempenho aprimorado em relação ao Transact-SQL.  
  
 A tabela a seguir lista os tópicos desta seção.  
  
 [Visão geral da integração CLR](clr-integration-overview.md)  
 Descreve os tipos de objetos que podem ser criados por meio da integração CLR e analisa os requisitos para criar objetos de banco de dados usando a integração CLR.  
  
 [Novidades da integração CLR](clr-integration-what-s-new.md)  
 Descreve os novos recursos desta versão.  
  
 [Arquitetura da integração CLR](../../database-engine/dev-guide/architecture-of-clr-integration.md)  
 Descreve as metas de design da integração CLR.  
  
 [Habilitando integração CLR](clr-integration-enabling.md)  
 Descreve como habilitar a integração CLR.  
  
## <a name="see-also"></a>Consulte Também  
 [Instalando o .NET Framework](https://technet.microsoft.com/library/ms166014\(v=SQL.105\).aspx)   
 [Desempenho da integração CLR](clr-integration-architecture-performance.md)  
  
  
