---
title: Caixa de diálogo Tabelas e Colunas
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- vdt.dlgbox.tablesandcolumns
ms.assetid: 8cf27be1-e66d-4735-a428-9ab4b33af4f5
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 342a7701b0b33482e5c83f0703121e3522654866
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75256151"
---
# <a name="tables-and-columns-dialog-box-visual-database-tools"></a>Caixa de dialogo Tabelas e Colunas (Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Use esta caixa de diálogo para mapear uma chave primária em uma tabela para uma chave estrangeira em outra. Para acessar essa caixa de diálogo, no menu **Designer de Tabela** , clique em **Relações**. Na caixa de diálogo **Relações de Chave Estrangeira**, clique no campo **Especificação das Tabelas e Colunas** e, em seguida, clique nas reticências **(…)** à direita da propriedade.  
  
> [!NOTE]  
> Se a tabela for publicada para replicação, você precisará fazer alterações no esquema usando a instrução Transact-SQL [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) ou o SMO (SQL Server Management Objects). Ao fazer alterações no esquema com o Criador de Tabelas ou com o Criador do Diagrama de Banco de Dados, ele tenta descartar e recriar a tabela. Não é possível descartar objetos publicados, portanto, haverá falha na alteração de esquema.  
  
## <a name="options"></a>Opções  
**Nome da Relação**  
Mostra o nome da relação.  
  
**Tabela de Chaves Primárias**  
Lista as tabelas no banco de dados Selecione a tabela que estará no lado da chave primária da relação.  
  
**Tabela de Chaves Estrangeiras**  
Mostra a tabela no lado da chave estrangeira da relação. Essa é a tabela selecionada atualmente no Designer de Tabela.  
  
**Grade abaixo da Tabela de Chaves Primárias**  
Lista as colunas da tabela selecionada na lista da **Tabela de Chaves Primárias** . Insira as colunas que contribuam para a chave primária daquela tabela.  
  
**Grade abaixo da Tabela de Chaves Estrangeiras**  
Lista as colunas da tabela selecionada na lista da **Tabela de Chaves Estrangeiras** . Insira a coluna das chaves estrangeiras da tabela das chaves estrangeiras que corresponde à coluna das chaves primárias.  
  
> [!NOTE]  
> As colunas selecionadas para a chave estrangeira devem ter o mesmo tipo de dados das colunas primárias às quais elas correspondem. Deve haver um número igual de colunas em cada uma das chaves. Por exemplo, se a chave primária da tabela no lado primário da relação estiver composta de duas colunas, será necessário coincidir cada uma dessas colunas com uma coluna na tabela no lado da chave estrangeira da relação.  
  
## <a name="see-also"></a>Consulte Também  
[Como: criar relações entre tabelas(https://msdn.microsoft.com/867a54b8-5be4-46e6-9702-49ae6dabf67c)  
  
