---
description: Conectar a um banco de dados de origem Oracle
title: Conectar a um banco de dados de origem Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- oraDb
ms.assetid: 220cf555-0db2-443c-8f87-8e413f3ca731
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c0d888548f8d3dd4bc0f2615db7f7435dc6b5414
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88496227"
---
# <a name="connect-to-an-oracle-source-database"></a>Conectar a um banco de dados de origem Oracle

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Use a página do Oracle de origem para fornecer as informações necessárias para conectar-se ao banco de dados de origem Oracle. A instância CDC lerá os logs de refazer do banco de dados Oracle aos quais você está conectado.  
  
 **Cadeia de conexão do Oracle**  
 Insira a cadeia de conexão do Oracle ao computador com o banco de dados Oracle que você está usando. A cadeia de conexão é gravada de um dos seguintes modos:  
  
 `host[:port][/service name]`  
  
 A cadeia de conexão também pode especificar um descritor de conexão do Oracle Net, por exemplo, `(DESCRIPTION=(ADDRESS=(PROTOCOL=tcp) (HOST=erp.contoso.com) (PORT=1521)) (CONNECT_DATA=(SERVICE_NAME=orcl)))`  
  
 Se estiver usando um servidor de diretório ou tnsnames, a cadeia de conexão pode ser o nome da conexão.  
  
 **Autenticação de mineração de logs da Oracle**  
 Para inserir as credenciais para o usuário de banco de dados Oracle que está autorizado para mineração de logs, siga um destes procedimentos:  
  
-   **Autenticação do Windows**: selecione isto para usar as credenciais de domínio atuais do Windows. Você só poderá usar esta opção se o banco de dados Oracle estiver configurado para funcionar com autenticação do Windows.  
  
-   **Autenticação do Oracle**: se você selecionou esta opção, deve digitar o **Nome de usuário** e **Senha** para o usuário no banco de dados Oracle ao qual você está se conectando.  
  
> [!NOTE]
>  Um usuário deve ter os privilégios a seguir concedidos no banco de dados Oracle para ser um usuário da mineração de logs.  
> 
>  -   SELECT em \<any-captured-table>  
> -   SELECT ANY TRANSACTION  
> -   EXECUTE em DBMS LOGMNR  
> -   SELECT em V$LOGMNR CONTENTS  
> -   SELECT em V$ARCHIVED LOG  
> -   SELECT em V$LOG  
> -   SELECT em V$LOGFILE  
> -   SELECT em V$DATABASE  
> -   SELECT em V$THREAD  
> -   SELECT em ALL INDEXES  
> -   SELECT em ALL OBJECTS  
> -   SELECT em DBA OBJECTS  
> -   SELECT em ALL TABLES  
> 
>  Se algum destes privilégios não puder ser concedido a um V$xxx, conceda a eles o V_S$xxx.  
  
 **Testar Conexão**  
 Clique em **Testar Conexão** para determinar se você estabeleceu uma conexão com o computador remoto que tem o banco de dados Oracle. Uma caixa de diálogo é aberta para informá-lo se a conexão teve êxito.  
  
> [!IMPORTANT]  
>  Devido a uma problema conhecido, a conexão ao banco de dados de origem Oracle poderá falhar se o Designer do CDC não for executado como administrador. Se a conexão falhar, feche e reinicie o Designer de CDC usando a opção **Executar como administrador** .  
  
 Depois de terminar de inserir informações nesta página, clique em **Avançar** para [Select Oracle Tables and Columns](../../integration-services/change-data-capture/select-oracle-tables-and-columns.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Como criar a instância de banco de dados de alteração do SQL Server](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [Editar propriedades da instância](../../integration-services/change-data-capture/edit-instance-properties.md)  
  
  
