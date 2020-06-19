---
title: Gerenciar espaços para tabela Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], managing tablespaces
- tablespaces [SQL Server replication]
ms.assetid: b8ea6c3b-01d6-4efc-bbfb-03b264530bbd
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a3624aed38a7a5bf75e0c0807aa8d3657156264f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068599"
---
# <a name="manage-oracle-tablespaces"></a>Gerenciar espaços de tabela Oracle
  Um espaço de tabela é uma unidade de armazenamento de banco de dados que é aproximadamente equivalente a um grupo de arquivo no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Os espaços de tabela permitem armazenamento e gerenciamento de objetos de banco de dados dentro de grupos individuais. Para obter mais informações, consulte a documentação Oracle.  
  
 Ao configurar uma tabela como parte de uma publicação Oracle, você pode especificar opcionalmente um espaço de tabela do Oracle existente para ser usado ao armazenar informações de log de replicação. Se não especificado, o espaço de tabela para os objetos de replicação é o espaço de tabela padrão associado com o esquema de usuário administrativo de replicação que foi configurado ao se configurar o Publicador.  
  
 **Para especificar um espaço de tabela para uma tabela de log de artigo**:  
  
-   Especifique um espaço de tabela na caixa de diálogo **Propriedades de Artigo** . Para obter mais informações sobre como acessar essa caixa de diálogo, consulte [View and Modify Publication Properties](../publish/view-and-modify-publication-properties.md).  
  
-   Use [sp_changearticle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changearticle-transact-sql). Para usar **sp_changearticle**, especifique o seguinte:  
  
    -   O nome do Publicador Oracle para o parâmetro **@publisher** .  
  
    -   O nome da publicação Oracle para o parâmetro **@publication** .  
  
    -   O nome do artigo para o parâmetro **@article** .  
  
    -   Um valor de ' tablespace ' para o parâmetro **@property** .  
  
    -   O nome do espaço de tabela para o parâmetro **@value** .  
  
## <a name="see-also"></a>Consulte Também  
 [Configurar um Publicador Oracle](configure-an-oracle-publisher.md)   
 [Objetos criados no Publicador Oracle](objects-created-on-the-oracle-publisher.md)  
  
  
