---
title: Configurar recursos do SQL Server compatíveis
ms.date: 03/14/2017
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: c8121ede-1aec-459b-b7b0-1408bb3e62fb
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: d558dad38492bcd9ce2bad0eb00a887a2225de33
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "73844566"
---
# <a name="configure-compatible-sql-server-features-with-stretch-database"></a>Configurar recursos do SQL Server compatíveis com o Stretch Database
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


Siga etapas simples para configurar os seguintes recursos do SQL Server para trabalhar com o Stretch Database.
-   Always On
-   Always Encrypted
-   Criptografia de Dados Transparente (TDE)
-   Tabelas temporais

## <a name="configure-always-on-with-stretch-database"></a>Configurar o Always On com o Stretch Database
Se você estiver usando o Always On com o Stretch Database, certifique-se de que a chave mestra do banco de dados está disponível nas réplicas secundárias. O Stretch Database usa a chave mestra de banco de dados para proteger as credenciais que ele usa para se conectar ao banco de dados remoto do Azure.

Depois de configurar o grupo de disponibilidade Always On, execute o procedimento armazenado **sp_control_dbmasterkey_password** em cada réplica secundária e forneça a senha para o banco de dados habilitado para o Stretch. Para obter mais informações e exemplos, consulte [sp_control_dbmasterkey_password](../../relational-databases/system-stored-procedures/sp-control-dbmasterkey-password-transact-sql.md). 

## <a name="configure-always-encrypted-with-stretch-database"></a>Configurar o Always Encrypted com o Stretch Database
Se você quiser usar o Always Encrypted e o Stretch Database juntos, você precisará configurar a criptografia nas colunas selecionadas antes de ativar o Stretch Database na tabela.

Se você já tiver ativado o Stretch Database na tabela, e desejar usar colunas Always Encrypted, você precisará fazer o seguinte.
1.   Desabilite o Stretch Database na tabela e recupere os dados remotos do Azure. Para obter mais informações, consulte [Desabilitar Stretch Database e trazer de volta dados remotos](../../sql-server/stretch-database/disable-stretch-database-and-bring-back-remote-data.md).
2.   Configure o Always Encrypted nas colunas selecionadas.
3. Reabilite o Stretch Database na tabela. Para obter mais informações, consulte [Enable Stretch Database for a database](../../sql-server/stretch-database/enable-stretch-database-for-a-table.md).

## <a name="configure-transparent-data-encryption-tde-with-stretch-database"></a>Configurar a TDE (Criptografia de Dados Transparente) com o Stretch Database

Se a TDE estiver habilitada no banco de dados local, ela não será automaticamente habilitada no ponto de extremidade remoto do Stretch Database. Você deverá se lembrar de habilitar a TDE no ponto de extremidade remoto depois de habilitar o Stretch no seu banco de dados.

## <a name="configure-temporal-tables-with-stretch-database"></a>Configurar tabelas temporais com Stretch Database
Se você estiver usando tabelas temporais, você poderá habilitar o Stretch Database na tabela de histórico, mas não na tabela atual.
-   Para obter orientação sobre como usar tabelas temporais com o Stretch Database, consulte [Gerenciar a Retenção de Dados Históricos em Tabelas Temporais com Versão do Sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md).
-   Para filtrar linhas para migrar da tabela de histórico usando uma janela deslizante, consulte [Selecionar linhas para migrar usando uma função de filtro](../../sql-server/stretch-database/select-rows-to-migrate-by-using-a-filter-function-stretch-database.md).
-   Não é possível habilitar o Stretch Database na tabela de histórico temporal se ela tem otimização de memória. Não há suporte para tabelas com otimização de memória.
