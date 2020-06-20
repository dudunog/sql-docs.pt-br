---
title: Regenerar os procedimentos transacionais personalizados para refletir alterações de esquema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- custom procedures [SQL Server replication]
- transactional replication, replicating schema changes
- schemas [SQL Server replication], replicating changes
ms.assetid: ccf68a13-e748-4455-8168-90e6d2868098
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7b41b5309816e037ce3619e880b796e0653c7506
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063710"
---
# <a name="regenerate-custom-transactional-procedures-to-reflect-schema-changes"></a>Regenerar os procedimentos transacionais personalizados para refletir alterações de esquema
  Por padrão, a replicação transacional faz todas as alterações de dados nos Assinantes por meio de um conjunto de procedimentos armazenados gerados por procedimentos internos para cada artigo de tabela na publicação. Os três procedimentos (um de cada para inserir, atualizar e excluir) são copiados para o Assinante e executados quando uma inserção, atualização ou exclusão for replicada para o Assinante. Quando uma alteração de esquema é feita em uma tabela do Publicador [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , a replicação regenera esses procedimentos automaticamente, chamando o mesmo conjunto de procedimentos de script interno, de modo que os novos procedimentos correspondam ao novo esquema (a replicação de alterações de esquema não tem suporte para Publicadores Oracle).  
  
 Também é possível especificar procedimentos personalizados para substituir um ou mais procedimentos padrão. Os procedimentos personalizados devem ser alterados se a alteração do esquema afetar o procedimento. Por exemplo, se um procedimento fizer referência a uma coluna descartada em uma alteração de esquema, as referências à coluna deverão ser removidas do procedimento. Há dois modos para que a replicação propague um novo procedimento personalizado aos Assinantes:  
  
-   A primeira opção é usar um procedimento de script personalizado para substituir os padrões usados pela replicação:  
  
    1.  Ao executar [sp_addarticle &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql), verifique se o **@schema_option** bit 0x02 é **verdadeiro**.  
  
    2.  Execute [sp_register_custom_scripting &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql) e especifique um valor de ' Insert ', ' Update ' ou ' Delete ' para o parâmetro **@type** e o nome do procedimento de script personalizado para o parâmetro **@value** .  
  
     Na próxima alteração de esquema, a replicação chamará esse procedimento armazenado para substituir a definição pelo novo procedimento armazenado personalizado definido pelo usuário e depois propagará o procedimento para cada Assinante.  
  
-   A segunda opção é usar um script que contenha uma nova definição de procedimento personalizada:  
  
    1.  Ao executar [sp_addarticle &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql), defina o **@schema_option** bit 0x02 como **false** para que a replicação não gere automaticamente procedimentos personalizados no Assinante.  
  
    2.  Antes de cada alteração de esquema, crie um novo arquivo de script e registre o script com replicação executando [sp_register_custom_scripting &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql). Especifique um valor de ' custom_script ' para o parâmetro **@type** e o caminho para o script no Publicador para o parâmetro **@value** .  
  
     Na próxima vez em que for feita uma alteração de esquema relevante, esse script será executado em cada Assinante dentro da mesma transação como o comando DDL. Após concluir a alteração de esquema, o registro do script será removido. Você deve registrar de novo o script para que ele seja executado depois de uma alteração de esquema subsequente.  
  
## <a name="see-also"></a>Consulte Também  
 [Especificar como as alterações são propagadas para artigos transacionais](transactional-articles-specify-how-changes-are-propagated.md)   
 [Fazer alterações de esquema em bancos de dados de publicação](../publish/make-schema-changes-on-publication-databases.md)  
  
  
