---
title: Selecionar tabelas e colunas Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- selTabCol
ms.assetid: bf73f80e-a954-4c5f-874e-17fdd4082715
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 042536288541a1c019772d97c3fd19a4e659c4dc
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86923888"
---
# <a name="select-oracle-tables-and-columns"></a>Selecionar tabelas e colunas Oracle

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Use a página Selecione tabelas e colunas Oracle para selecionar as tabelas do banco de dados de origem Oracle onde as alterações são capturadas. Esta página tem os seguintes elementos:  
  
## <a name="options"></a>Opções  
 **Lista Tabela**  
 A lista de tabelas tem três colunas:  
  
-   **Nome da tabela Oracle**: o nome da tabela, incluindo esquema de tabela.  
  
-   **Instância de Captura**: é o nome da instância de captura usada para nomear objetos do Change Data Capture específicos. A instância de captura não pode ser NULL.  
  
     Se não for especificado, o nome será derivado do nome do esquema de origem mais o nome da tabela de origem, no formato `<schema-name>_<table-name>`. O nome da instância de captura não pode exceder 100 caracteres e deve ser exclusivo no banco de dados.  
  
     Você pode clicar em qualquer célula nesta coluna para editar manualmente **capture_instance**.  
  
-   **Security Role**: o nome da função de banco de dados de associação usada para controlar o acesso aos dados de alteração.  
  
     Você pode clicar em qualquer célula nesta coluna para editar manualmente **security_role**.  
  
 **Adicionar tabelas**  
 Clique em **Adicionar Tabelas** para abrir a caixa de diálogo Seleção de Tabela em que você pode [Selecionar as tabelas Oracle para capturar alterações](../../integration-services/change-data-capture/select-oracle-tables-for-capturing-changes.md).  
  
 **Editar**  
 Selecione uma tabela da lista e selecione **Editar** para abrir a caixa de diálogo **Propriedades** para a tabela em que você pode [Fazer alterações nas tabelas selecionadas para capturar alterações](../../integration-services/change-data-capture/make-changes-to-the-tables-selected-for-capturing-changes.md).  
  
 **Remover**  
 Selecione uma tabela da lista e clique em **Remover** para remover a tabela da instância CDC.  
  
 Depois que você [Selecionar tabelas Oracle para capturar alterações](../../integration-services/change-data-capture/select-oracle-tables-for-capturing-changes.md) e/ou [Fizer alterações nas tabelas selecionadas para capturar alterações](../../integration-services/change-data-capture/make-changes-to-the-tables-selected-for-capturing-changes.md) usando as caixas de diálogo corretas, clique em **Avançar** para [Gerar e executar scripts de log suplementares](../../integration-services/change-data-capture/generate-and-run-the-supplemental-logging-script.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Como criar a instância de banco de dados de alteração do SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Editar tabelas](../../integration-services/change-data-capture/edit-tables.md)   
 [Adicionar tabelas a uma instância CDC](../../integration-services/change-data-capture/add-tables-to-a-cdc-instance.md)   
 [Editar as propriedades da tabela](../../integration-services/change-data-capture/edit-the-table-properties.md)  
  
  
