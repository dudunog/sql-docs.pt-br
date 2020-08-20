---
description: Resumo de funções de DLL do instalador
title: Resumo da função DLL do instalador | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], installer DLL functions
- installer DLL [ODBC]
ms.assetid: 666c09d3-1e10-4d89-9b42-eda2957a87f0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3666808659abb29a1f5a1eb1e8be62e8cf0507f6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461228"
---
# <a name="installer-dll-function-summary"></a>Resumo de funções de DLL do instalador
A tabela a seguir descreve as funções na DLL do instalador. Para obter mais informações sobre a sintaxe e a semântica para cada função, consulte [instalador DLL API Reference](../../../odbc/reference/syntax/installer-dll-api-reference-function.md).  
  
|Tarefa|Nome da função|Finalidade|  
|----------|-------------------|-------------|  
|Instalando o ODBC|[SQLConfigDriver](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|Carrega a DLL de instalação específica do driver.|  
||[SQLGetInstalledDrivers](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)|Retorna uma lista de drivers instalados.|  
||[SQLInstallDriverEx](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|Adiciona um driver às informações do sistema.|  
||[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|Retorna o diretório de destino para o Gerenciador de driver.|  
||[SQLInstallerError](../../../odbc/reference/syntax/sqlinstallererror-function.md)|Retorna informações de erro ou status para as funções do instalador.|  
||[SQLInstallTranslatorEx](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|Adiciona um tradutor às informações do sistema.|  
||[SQLPostInstallerError](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)|Permite que uma biblioteca de instalação de driver ou tradutor Relate erros.|  
||[SQLRemoveDriver](../../../odbc/reference/syntax/sqlremovedriver-function.md)|Remove um driver das informações do sistema.|  
||[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|Remove os componentes principais do ODBC das informações do sistema.|  
||[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|Remove o tradutor das informações do sistema.|  
|Configurando fontes de dados|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|Chama a DLL de instalação específica do driver.|  
||[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|Exibe uma caixa de diálogo para adicionar uma fonte de dados.|  
||[SQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|Recupera o modo de configuração que indica onde os valores de DSN de listagem de Odbc.ini de entrada estão nas informações do sistema.|  
||[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|Grava um valor nas informações do sistema.|  
||[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|Exibe uma caixa de diálogo para selecionar um tradutor.|  
||[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|Exibe uma caixa de diálogo para configurar fontes de dados e drivers.|  
||[SQLReadFileDSN](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|Lê informações de DSNs de arquivo.|  
||[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|Remove a fonte de dados padrão.|  
||[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|Remove uma fonte de dados.|  
||[SQLSetConfigMode](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|Define o modo de configuração que indica onde os valores de DSN de listagem de Odbc.ini de entrada estão nas informações do sistema.|  
||[SQLValidDSN](../../../odbc/reference/syntax/sqlvaliddsn-function.md)|Verifica o comprimento e a validade do nome da fonte de dados.|  
||[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|Adiciona uma fonte de dados.|  
||[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|Grava informações em DSNs de arquivo.|  
||[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|Obtém um valor das informações do sistema.|
