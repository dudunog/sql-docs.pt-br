---
title: Instrução Create Table do SQL (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.createtablesql.f1
ms.assetid: 0d6f6b3b-d023-4770-a8a9-65b2977c8d05
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d3fc2054711708a27691f2d7219c33749f11b977
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85424953"
---
# <a name="create-table-sql-statement-sql-server-import-and-export-wizard"></a>Instrução Create Table SQL (Assistente de Importação e Exportação do SQL Server)
  Use a caixa de diálogo **instrução SQL CREATE TABLE** para exibir a instrução que foi gerada automaticamente ou para modificá-la para suas finalidades. Se você modificar essa instrução, também poderá fazer alterações associadas ao mapeamento de coluna e poderá manter a instrução SQL editada manualmente.  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] gera uma instrução CREATE TABLE padrão baseada na fonte de dados conectada. A instrução CREATE TABLE padrão não incluirá o atributo FILESTREAM mesmo que a tabela de origem inclua uma coluna com o atributo FILESTREAM declarado. Para executar um componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com o atributo FILESTREAM, implemente primeiro o armazenamento FILESTREAM no banco de dados de destino. Em seguida, adicione o atributo FILESTREAM à instrução CREATE TABLE na caixa de diálogo **Criar Tabela** . Para obter mais informações, consulte [Dados de blob &#40;objeto binário grande&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 Para obter mais informações sobre este assistente, consulte [Assistente de Importação e Exportação do SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para saber mais sobre as opções de inicialização do assistente, bem como as permissões necessárias para executar o assistente com êxito, consulte [executar o assistente de importação e exportação do SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 O objetivo do Assistente de Importação e Exportação do SQL Server é copiar dados de uma origem para um destino. O assistente também pode criar um banco de dados de destino e tabelas de destino para você. No entanto, se for necessário copiar vários bancos de dados ou tabelas, ou outros tipos de objetos de banco de dados, será necessário usar o Assistente para Copiar Banco de Dados. Para obter mais informações, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opções  
 **Instrução SQL**  
 Exiba a instrução SQL gerada automaticamente e permite que ela seja editada.  
  
> [!NOTE]  
>  Se desejar incluir um retorno de carro na instrução SQL, pressione CTRL+ENTER. Se você pressionar somente ENTER, a caixa de diálogo será fechada.  
  
 **AutoGenerate**  
 Restaure a instrução SQL padrão, caso ela tenha sido modificada, clicando em **Gerar Automaticamente**.  
  
  
