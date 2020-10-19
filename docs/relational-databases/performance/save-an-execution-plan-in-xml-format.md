---
title: Salvar um plano de execução no formato XML | Microsoft Docs
description: Saiba como usar o SQL Server Management Studio para salvar planos de execução no formato XML e abri-los para exibição. É necessário ter as permissões apropriadas.
ms.custom: ''
ms.date: 08/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- XML query plans [SQL Server]
- opening execution plans
- XML Showplans [SQL Server]
- execution plans [SQL Server], saving
- saving execution plans
ms.assetid: c439e53b-56f3-4442-97c6-dabd48a203d8
author: julieMSFT
ms.author: jrasnick
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f10e2cd6b6b146bb7c91d9732ba04b7f6a4d5ebb
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91784728"
---
# <a name="save-an-execution-plan-in-xml-format"></a>Salvar um plano de execução em formato XML
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Use o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para salvar planos de execução como um arquivo XML e abri-los para exibição.  
  
 Para usar o recurso plano de execução em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], ou usar as opções SET Showplan XML, os usuários devem ter as permissões apropriadas para executar a consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] para qual um plano de execução está sendo gerado, e deve ser concedida a permissão SHOWPLAN para todos os bancos de dados referenciados pela consulta.  
  
### <a name="to-save-a-query-plan-by-using-the-xml-showplan-set-options"></a>Para salvar um plano de consulta usando as opções SET Showplan XML  
  
1.  Em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] abra um editor de consulta e conecte a [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Ative o [SHOWPLAN_XML](../../t-sql/statements/set-showplan-xml-transact-sql.md) com a seguinte instrução:  
  
    ```sql  
    SET SHOWPLAN_XML ON;  
    GO  
    ```  
  
    Para ativar o [STATISTICS XML](../../t-sql/statements/set-statistics-xml-transact-sql.md), use a seguinte instrução:  
  
    ```sql  
    SET STATISTICS XML ON;  
    GO  
    ```  
  
     > [!NOTE] 
     > O SHOWPLAN_XML gera informações de plano de execução de consulta de tempo de compilação para uma consulta, mas não executa a consulta. Ele também é conhecido como o plano de execução **estimado**. O STATISTICS XML gera informações do plano de execução de consulta em runtime para uma consulta e a executa. Ele também é conhecido como o plano de execução **real**.  
  
3.  Execute uma consulta. Exemplo:  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    SET SHOWPLAN_XML ON;  
    GO  
    -- Execute a query.  
    SELECT BusinessEntityID   
    FROM HumanResources.Employee  
    WHERE NationalIDNumber = '509647174';  
    GO  
    SET SHOWPLAN_XML OFF;  
    ```  
  
4.  No painel **Resultados** , clique com o botão direito do mouse em **Plano de execução XML do Microsoft SQL Server** que contém o plano de consulta e clique em **Salvar Resultados Como**.  
  
5.  Na caixa de diálogo **Salvar** \<Grid or Text> **Resultados**, na caixa **Salvar como tipo**, clique em **Todos os arquivos (\*.\*)** .  
  
6.  Na caixa **Nome do arquivo**, forneça um nome no formato \<name> **.sqlplan** e clique em **Salvar**.  

### <a name="to-save-an-execution-plan-by-using-sql-server-management-studio-options"></a>Para salvar um plano de execução usando opções do SQL Server Management Studio  
  
1.  Gere um plano de execução estimado ou um plano de execução atual usando [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para obter mais informações, consulte [Exibir o plano de execução estimado](../../relational-databases/performance/display-the-estimated-execution-plan.md) e [Exibir um plano de execução real](../../relational-databases/performance/display-an-actual-execution-plan.md).  
  
2.  Na guia **Plano de execução** do painel de resultados, clique com o botão direito do mouse no plano de execução gráfico e escolha **Salvar Plano de Execução Como**.  
  
     Como alternativa, você também pode escolher **Salvar Plano de Execução Como** no menu **Arquivo** .  
  
3.  Na caixa de diálogo **Salvar Como**, verifique se a opção **Salvar como tipo** está definida como **Arquivos de Plano de Execução (\*.sqlplan)** .  
  
4.  Na caixa **Nome do arquivo**, forneça um nome no formato \<name> **.sqlplan** e clique em **Salvar**.  
  
### <a name="to-open-a-saved-xml-query-plan-in-sql-server-management-studio"></a>Para abrir um plano de consulta XML salvo em SQL Server Management Studio  
  
1.  Em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], no menu **Arquivo** , escolha **Abrir**e então clique em **Arquivo**.  
  
2.  Na caixa de diálogo **Abrir Arquivo**, defina **Arquivos de tipo** para **Arquivos de Plano de Execução (\*.sqlplan)** para gerar uma lista filtrada dos arquivos de plano de consulta XML salvos.  
  
3.  Selecione o arquivo plano consulta XML que você quer exibir e clique em **Abrir**.  
  
     Como alternativa, no Windows Explorer, clique duas vezes em um arquivo com a extensão **.sqlplan**. O plano abre em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
## <a name="see-also"></a>Consulte Também  
 [SET SHOWPLAN_XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-showplan-xml-transact-sql.md)   
 [SET STATISTICS XML &#40;Transact-SQL&#41;](../../t-sql/statements/set-statistics-xml-transact-sql.md)  
  
  
