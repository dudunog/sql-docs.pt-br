---
title: Ambientes multiusuários
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- users [SQL Server], multiuser environments
- conflict resolution [Visual Database Tools]
- multiple users making database changes
- multiuser environments [Visual Database Tools]
- database modifications [SQL Server]
- version control [Visual Database Tools]
- Visual Database Tools [SQL Server], multiuser environments
ms.assetid: 330bd48c-9427-4967-b58e-b7c492d5ee36
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 75346207a2f91744c78db783bf40edd679ebcbb8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75258338"
---
# <a name="multiuser-environments-visual-database-tools"></a>Ambientes multiusuários (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Um ambiente multiusuário é um ambiente em que outros usuários podem se conectar e fazer alterações no mesmo banco de dados em que você está trabalhando. Como resultado, vários usuários podem estar trabalhando ao mesmo tempo com os mesmos objetos de banco de dados. Assim, um ambiente multiusuário apresenta a possibilidade de o banco de dados ser afetado por alterações de outros usuários enquanto você faz alterações e vice-versa.  
  
Um assunto fundamental quando se trabalha com bancos de dados em um ambiente multiusuário diz respeito a permissões de acesso. As permissões que você tem para o banco de dados determinam a extensão do trabalho que pode ser realizado no banco de dados. Por exemplo, para fazer alterações em objetos de um banco de dados, você deve ter permissões de gravação adequadas para o banco de dados. Para obter mais informações sobre permissões em seu banco de dados, consulte a documentação do banco de dados. Para obter mais informações, consulte [Permissões e Visual Database Tools &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/permissions-and-visual-database-tools-visual-database-tools.md).  
  
Quando você salva alterações em tabelas, o Designer de Tabela verifica se o banco de dados não foi modificado desde a gravação das últimas alterações. Se outro usuário tiver feito alterações, você será notificado de que o banco de dados foi modificado. Talvez seja necessário reconciliar essas mudanças. Para obter mais informações, veja [Reconciliar alterações feitas por vários usuários &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/reconcile-changes-made-by-multiple-users-visual-database-tools.md).  
  
Em um ambiente multiusuário, algumas considerações especiais devem ser levadas em conta para evitar alterações conflitantes. Para obter mais informações, consulte [Problemas de evolução do banco de dados &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/issues-of-database-evolution-visual-database-tools.md).  
  
Um modo de evitar problemas é trabalhar em uma cópia do banco de dados, como um banco de dados de teste. Quando você fizer alterações, poderá criar um script para ser executado e fazer as alterações no banco de dados original após a resolução dos conflitos offline. Para obter mais informações, veja [Bancos de dados de desenvolvimento, teste e produção &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/development-test-and-production-databases-visual-database-tools.md).  
  
