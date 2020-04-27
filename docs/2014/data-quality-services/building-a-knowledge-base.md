---
title: Criando uma base de dados de conhecimento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 51eff161-6ecd-4ee4-8187-1dd8ef4814bd
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 01d0b016f6b7e1ea3c83cd42f52facb56f825b77
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65481167"
---
# <a name="building-a-knowledge-base"></a>Criando uma base de dados de conhecimento
  Uma base de dados de conhecimento no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) é um repositório de conhecimento sobre seus dados que lhe permitem compreender os dados e manter sua integridade. Uma base de dados de conhecimento consiste em domínios, cada um representando os dados em um campo de dados. A base de dados de conhecimento é usada pelo DQS para executar a limpeza e a eliminação de duplicação de dados em um banco de dados. Para preparar a base de dados de conhecimento para a limpeza de dados, você pode executar uma análise assistida por computador de um exemplo de dados e gerenciar interativamente valores nos domínios. O DQS lhe permite importar conhecimento, criar regras e relações, alterar valores de dados diretamente e aproveitar um banco de dados padrão.  
  
## <a name="in-this-section"></a>Nesta seção  
 É possível executar as seguintes operações em uma base de dados de conhecimento:  
  
|||  
|-|-|  
|Criar uma nova base de dados de conhecimento do zero, a partir de uma base de dados de conhecimento existente ou a partir de um arquivo de dados .dqs.|[Criar uma base de dados de conhecimento](../../2014/data-quality-services/create-a-knowledge-base.md)|  
|Abrir uma base de dados de conhecimento existente para executar a descoberta da base de dados de conhecimento, o gerenciamento de domínio, ou adicionar uma política de correspondência.|[Abrir uma base de dados de conhecimento](../../2014/data-quality-services/open-a-knowledge-base.md)|  
|Executar ações de gerenciamento em uma base de dados de conhecimento, inclusive abri-la, desbloqueá-la, descartar seu trabalho nela, renomeá-la, excluí-la ou exibir suas propriedades.|[Gerenciar uma base de dados de conhecimento](../../2014/data-quality-services/manage-a-knowledge-base.md)|  
|Adicionar conhecimento a uma base de dados de conhecimento através de descoberta de conhecimento; gerenciamento de valor de domínio; adicionando uma política de comparação; importando um conhecimento, domínio ou valores; ou usando a base de dados de conhecimento padrão, Dados do DQS.|[Adicionando conhecimento a uma base de dados de conhecimento](../../2014/data-quality-services/adding-knowledge-to-a-knowledge-base.md)|  
|Analisar um exemplo de dados para critérios de qualidade de dados.|[Executar a descoberta da base de dados de conhecimento](../../2014/data-quality-services/perform-knowledge-discovery.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descrição da tarefa|Tópico|  
|----------------------|-----------|  
|Importar ou exportar conhecimento para/de uma base de dados de conhecimento.|[Importando e exportando conhecimento](../../2014/data-quality-services/importing-and-exporting-knowledge.md)|  
|Criar um domínio único e adicionar conhecimento ao domínio.|[Gerenciando um domínio](../../2014/data-quality-services/managing-a-domain.md)|  
|Criar um domínio composto e adicionar conhecimento ao domínio.|[Gerenciando um domínio composto](../../2014/data-quality-services/managing-a-composite-domain.md)|  
  
  
