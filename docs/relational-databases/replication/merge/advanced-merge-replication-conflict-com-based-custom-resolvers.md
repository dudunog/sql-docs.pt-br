---
description: Conflito de replicação de mesclagem avançada – resolvedores personalizados baseados em COM
title: Resolvedores personalizados baseados em COM | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- COM-based resolvers [SQL Server replication]
- custom resolvers [SQL Server replication]
ms.assetid: 94195797-ad7a-4962-a8e3-b259cd13aa38
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 569669c45eb973993e932263ea8c87b7f3b4c0a4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465234"
---
# <a name="advanced-merge-replication-conflict---com-based-custom-resolvers"></a>Conflito de replicação de mesclagem avançada – resolvedores personalizados baseados em COM
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Resolvedores personalizados fornecem maior flexibilidade do que o mecanismo de resolução padrão, e podem implementar a lógica comercial exigida por aplicativos usando dados replicados. Um resolvedor personalizado com base em COM é uma biblioteca de vínculo dinâmico (DLL) que implementa a interface COM **ICustomResolver** , seus métodos e propriedades e outras interfaces de suporte e definições de tipo criadas especificamente para resolução de conflito.  
  
> [!NOTE]  
>  Se possível, recomenda-se o uso de um manipulador de lógica de negócios em vez de um resolvedor personalizado com base em COM. Para obter mais informações sobre manipuladores de lógica de negócios, consulte [Executar lógica de negócios durante a sincronização de mesclagem](../../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md).  
  
 Para criar um resolvedor COM personalizado, é possível usar a biblioteca de tipos fornecida em replrec.dll; por padrão, essa biblioteca é instalada em [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM.  
  
 Antes de gravar um resolvedor COM personalizado, é necessário decidir:  
  
-   Os tipos de alterações de linhas que você quer resolver, como atualizações, inserções e exclusões, e se o resolvedor deve ser chamado durante o carregamento de alterações de mesclagem, o download de alterações de mesclagem ou ambos. É possível especificar um tipo de alteração, todas as alterações ou qualquer combinação. O resolvedor de conflito padrão de mesclagem controla quaisquer conflitos não controlados por um resolvedor personalizado.  
  
-   Quando usar controle de coluna ao resolver o conflito. Quando rastreamento de nível de coluna estiver habilitado, somente dados naquelas colunas em que existir um conflito serão sinalizados como conflito, caso contrário os dados serão mesclados. No entanto, conflitos são resolvidos da mesma forma que rastreamento em nível de linha: o vencedor de prioridade substitui toda a coluna de dados (mas os dados podem ser uma mistura de valores do Publicador, Assinantes ou alguns valores alterados que não eram nem do Publicador e nem dos Assinantes). Para obter mais informações, consulte [Detectar e resolver conflitos de replicação de mesclagem](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md).  
  
 Para implementar um resolvedor de conflito personalizado com base em COM, consulte [Implementar um resolvedor de conflitos personalizado para um artigo de mesclagem](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)  
  
 Um resolvedor personalizado é especificado para um artigo, não para uma publicação inteira. O mesmo resolvedor pode ser usado com mais de um artigo, mas a lógica em resolvedores personalizados é em geral específica para uma determinada tabela. Se a tabela usada no artigo for modificada depois que o resolvedor for criado (por exemplo, renomeando o nome da coluna que é usada em resolução de conflito), o resolvedor personalizado pode precisar ser modificado e recompilado.  
  
 Para especificar um resolvedor personalizado, consulte [Especificar um resolvedor de artigo de mesclagem](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Detecção e resolução de conflito de replicação de mesclagem avançada](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Microsoft COM-Based Resolvers](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)  
  
  
