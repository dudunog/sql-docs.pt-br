---
description: Importar dados para o Microsoft Excel de um banco de dados do Visual FoxPro
title: Importando dados para o Microsoft Excel a partir de um banco de dados do Visual FoxPro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Excel
- Visual FoxPro data [ODBC], Excel
- Visual FoxPro data [ODBC], importing
- Visual FoxPro ODBC driver [ODBC], Excel
ms.assetid: 3085bc4c-00a7-40e5-bffb-c3962cd3d509
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9a4bd1cf7983ed0a552de4f9d0f491960b48f0d7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500289"
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>Importar dados para o Microsoft Excel de um banco de dados do Visual FoxPro
Você pode importar dados do Visual FoxPro para sua planilha do Microsoft Excel se tiver definido uma fonte de dados para ele. Para obter informações sobre como criar uma fonte de dados do Visual FoxPro, consulte [acessando uma fonte de dados do Visual FoxPro do Microsoft Excel](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md).  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>Para importar dados do Visual FoxPro para uma planilha do Microsoft Excel  
  
1.  Abra uma planilha do Microsoft Excel.  
  
2.  No menu dados, escolha obter dados externos. O Microsoft Query é aberto.  
  
3.  Na caixa de diálogo selecionar fonte de dados, selecione uma fonte de dados do Visual FoxPro e clique em usar.  
  
4.  Se o banco de dados acessado pela sua fonte de dado incluir tabelas, selecione uma tabela na caixa de diálogo adicionar tabelas. O Microsoft Query exibe a tabela adicionada na metade superior do designer de consulta.  
  
    > [!NOTE]  
    >  A lista de proprietários não está disponível nesta caixa de diálogo porque o driver não oferece suporte a proprietários. A lista de banco de dados não está disponível porque o driver não oferece suporte a vários bancos de dados em uma fonte de dado.  
  
5.  Selecione os campos para sua consulta arrastando-os da tabela para a metade inferior do designer.  
  
6.  Feche o Microsoft Query. Os dados selecionados são importados para a planilha do Microsoft Excel.
