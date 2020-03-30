---
title: Recomendações de índice columnstore no DTA (Assistente de Otimização do Mecanismo de Banco de Dados)
ms.custom: seo-dt-2019
ms.date: 01/09/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine Tuning Advisor, columnstore index
- Database Engine Tuning Advisor, columnstore and rowstore indexes
ms.assetid: 9fba1139-82cb-4244-a41f-4337a7d0c132
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 1d0086a6698c45d5c24d89f8e6a681d14051e11f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "74166000"
---
# <a name="columnstore-index-recommendations-in-database-engine-tuning-advisor-dta"></a>Recomendações de índice columnstore no DTA (Orientador de Otimização do Mecanismo de Banco de Dados)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

 
  As cargas de trabalho de data warehousing e de análise podem se beneficiar muito dos [índices columnstore](../../t-sql/statements/create-columnstore-index-transact-sql.md), bem como os índices rowstore tradicionais. A escolha de quais índices columnstore e rowstore criar para seu banco de dados depende da carga de trabalho do aplicativo. No SQL Server 2016, o [DTA (Orientador de Otimização do Mecanismo de Banco de Dados)](../../relational-databases/performance/database-engine-tuning-advisor.md) pode analisar sua carga de trabalho e recomendar uma combinação apropriada de índices columnstore e rowstore para criar no banco de dados. 
  
 Esse recurso está disponível no SQL Server Management Studio versão **16.4** ou superior. 
  
## <a name="how-to-enable-columnstore-index-recommendations-in-database-engine-tuning-advisor-gui"></a>Como habilitar as recomendações de índice columnstore na GUI do Orientador de Otimização do Mecanismo de Banco de Dados

  
  1. Inicie o Orientador de Otimização do Mecanismo de Banco de Dados e abra uma nova sessão de otimização.
  
  2. Selecione os bancos de dados e a carga de trabalho para otimização no painel **Geral**.
  
  3. No painel Opções de otimização, marque a caixa de seleção **Recomendar índices columnstore** (veja a figura abaixo).
  ![Opção de otimização de índices columnstore do DTA](../../relational-databases/performance/media/dta-columnstore-indexes-tuning-option.gif)
 
  4. Selecione outras opções de otimização e clique no botão **Iniciar Análise**.
  
  5. Quando a otimização estiver completa, exiba todas as recomendações incluindo os índices columnstore no painel **Recomendações** (veja a figura abaixo).      
  ![Recomendação de índice columnstore do DTA](../../relational-databases/performance/media/dta-columnstore-index-recommendation.gif)
  
  6. Clique no hiperlink **Definição** para exibir a instrução DDL (linguagem de definição de dados) do SQL que pode criar o índice recomendado. Por padrão, o DTA usa o sufixo **col** no nome dos índices columnstore para facilitar a identificação dos índices columnstore (veja a figura abaixo).
  ![Definição de índice columnstore do DTA](../../relational-databases/performance/media/dta-columnstore-index-definition.gif) 
  
  
  ## <a name="how-to-enable-columnstore-index-recommendations-in-dtaexe-utility"></a>Como habilitar as recomendações de índice columnstore no utilitário dta.exe

Para habilitar as recomendações de columnstore ao usar o utilitário de linha de comando dta.exe, use o parâmetro de linha de comando **-fc**.

Para obter mais informações sobre o utilitário de linha de comando dta.exe, consulte [Utilitário dta](../../tools/dta/dta-utility.md)

## <a name="see-also"></a>Consulte Também
[Guia de Índices Columnstore](../../relational-databases/indexes/columnstore-indexes-overview.md)       
[Orientador de Otimização do Mecanismo de Banco de Dados](../../relational-databases/performance/database-engine-tuning-advisor.md)      
[Tutorial: Orientador de Otimização do Mecanismo de Banco de Dados](Tutorial:%20Database%20Engine%20Tuning%20Advisor.md)



  

