---
title: Propriedades do banco de dados (página Controle de Alterações) | Microsoft Docs
description: Saiba como usar a guia ChangeTracking na caixa de diálogo Propriedades do Banco de Dados para exibir ou modificar as configurações de controle de alterações de um banco de dados.
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.changetracking.f1
ms.assetid: 9b929640-bc62-449b-9b06-b5a77b8cf372
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b0abdb96d6d01ac1d630e8489013c381518573b6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756237"
---
# <a name="database-properties-changetracking-page"></a>Propriedades do Banco de Dados (página Controle de Alterações)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Use essa página para exibir ou modificar configurações de controle de alterações para o banco de dados selecionado. Para obter mais informações sobre as opções disponíveis nessa página, veja [Habilitar e desabilitar o controle de alterações &#40;SQL Server&#41;](../../relational-databases/track-changes/enable-and-disable-change-tracking-sql-server.md).  
  
## <a name="options"></a>Opções  
 **Controle de alterações**  
 Use para habilitar ou desabilitar o controle de alterações para o banco de dados.  
  
 Para habilitar o controle de alterações, deve-se ter permissão para modificar o banco de dados.  
  
 Definindo-se o valor como **Verdadeiro** define-se uma opção de banco de dados que permite que o controle de alterações seja habilitado em tabelas individuais.  
  
 Pode-se também configurar o controle de alterações usando [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md).  
  
 **Período de Retenção**  
 Especifica o período mínimo para manter informações de controle de alterações no banco de dados. Os dados serão removidos somente se o valor **Auto Clean-Up** for **Verdadeiro**.  
  
 O valor padrão é 2.  
  
 **Unidades de Período de Retenção**  
 Especifica as unidades para o valor de período de retenção. Pode-se selecionar **Dias**, **Horas**ou **Minutos**. O valor padrão é **Dias**.  
  
 O período de retenção mínimo é de 1 minuto. Não há um período máximo de retenção.  
  
 **Auto Clean-Up**  
 Indica se as informações de controle de alterações são automaticamente removidas depois do período de retenção especificado.  
  
 Habilitar a opção **Auto Clean-Up** redefine qualquer período de retenção personalizado anterior ao período de retenção padrão de 2 dias.  
  
## <a name="see-also"></a>Consulte Também  
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
  
