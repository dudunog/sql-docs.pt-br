---
title: ODBC Jet SQLConfigDataSource (driver do Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Excel Driver
- Excel driver [ODBC], SqlConfigDataSource
ms.assetid: 885b3bea-f4b6-4902-b994-f78a912b612f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a76482acd1182d900336d7ac9826b16968e00caa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81293006"
---
# <a name="odbc-jet-sqlconfigdatasource-excel-driver"></a>ODBC Jet SQLConfigDataSource (Driver do Excel)
> [!NOTE]  
>  Este tópico fornece informações específicas do driver do Excel. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 A função **SQLConfigDataSource** que é usada para adicionar, modificar ou excluir uma fonte de dados usa dinamicamente as seguintes palavras-chave.  
  
|Palavra-chave|Descrição|  
|-------------|-----------------|  
|DBQ|Para o driver do Microsoft Excel ao acessar arquivos do Microsoft Excel 5,0 ou posterior, o nome do arquivo de pasta de trabalho.<br /><br /> Isso define a mesma opção que o **banco de dados** na caixa de diálogo de instalação.|  
|DEFAULTDIR|A especificação de caminho para o diretório.<br /><br /> Isso define a mesma opção de **Selecionar diretório** ou **Selecionar pasta de trabalho** na caixa de diálogo de instalação.|  
|DESCRIPTION|Uma descrição dos dados na fonte de dados.<br /><br /> Isso define a mesma opção que a **Descrição** na caixa de diálogo de instalação.|  
|DRIVER|A especificação de caminho para a DLL do driver.|  
|DRIVERid|Uma ID de inteiro para o driver.<br /><br /> 534 (Microsoft Excel 3,0)<br /><br /> 278 (Microsoft Excel 4,0)<br /><br /> 22 (Microsoft Excel 5.0/7.0)<br /><br /> 790 (Microsoft Excel 97-2003)|  
|FIL|Tipo de arquivo, por exemplo, Excel 3,0, Excel 4,0, Excel 5,0, Excel 7,0, Excel 97, Excel 2000 ou Excel 2003.|  
|FIRSTROWHASNAMES|Indica se as células da primeira linha do intervalo contêm os nomes de coluna da tabela (1) ou não (0).|  
|MAXSCANROWS|O número de linhas a serem examinadas ao definir o tipo de dados de uma coluna com base nos dados existentes.<br /><br /> Um número de 1 a 16 pode ser inserido para as linhas a serem verificadas. O valor padrão é 8; Se for definido como 0, todas as linhas serão verificadas. (Um número fora do limite retornará um erro.)<br /><br /> Isso define a mesma opção que as **linhas a serem verificadas** na caixa de diálogo de instalação.|  
|READONLY|TRUE para tornar o arquivo somente leitura; FALSE para tornar o arquivo não somente leitura.<br /><br /> Isso define a mesma opção como **somente leitura** na caixa de diálogo de instalação.|  
|THREADS|O número de threads em segundo plano a ser usado pelo mecanismo. Para o driver do Microsoft Access, esse valor usa como padrão 3, mas pode ser alterado. Para o dBASE, MicrosoftExceldriver esse valor é 3 e não pode ser alterado.<br /><br /> Isso define a mesma opção que os **threads** na caixa de diálogo de instalação.|
