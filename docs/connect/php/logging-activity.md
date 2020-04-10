---
title: Registro de atividades em log | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- logging activity
ms.assetid: a777b3d9-2262-4e82-bc82-b62ad60d0e55
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5486f32894b04a211be26bd7c55d58294ad36367
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922853"
---
# <a name="logging-activity"></a>Registrando atividades em log
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Por padrão, os erros e avisos gerados pelos [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] não são registrados em log. Este tópico discute como configurar o registro de atividades em log.  
  
## <a name="logging-activity-using-the-pdo_sqlsrv-driver"></a>Registrando atividades em log usando o driver PDO_SQLSRV  
A única configuração disponível para o driver PDO_SQLSRV é a entrada pdo_sqlsrv.log_severity no arquivo php.ini.  
  
Adicione o seguinte ao final do arquivo php.ini:  
  
```  
[pdo_sqlsrv]  
pdo_sqlsrv.log_severity = <number>  
```  
  
**log_severity** pode ser um dos seguintes valores:  
  
|Valor|DESCRIÇÃO|  
|---------|---------------|  
|0|O registro em log está desabilitado (é o padrão se nada estiver definido).|  
|-1|Especifica que erros, avisos e notificações são registrados em log.|  
|1|Especifica que os erros serão registrados em log.|  
|2|Especifica que os avisos serão registrados em log.|  
|4|Especifica que as notificações serão registradas em log.|  
  
Informações de registro em log são adicionadas ao arquivo phperrors.log.  
  
O PHP lê o arquivo de configuração na inicialização e armazena os dados em um cache. Ele também fornece uma API para atualizar essas configurações e usar imediatamente, e é gravado no arquivo de configuração. Essa API permite que os scripts de aplicativo alterem as configurações, mesmo após a inicialização do PHP.  
  
## <a name="logging-activity-using-the-sqlsrv-driver"></a>Registrando a  atividade em log usando o driver SQLSRV  
Para ativar o registro em log, você pode usar a função [sqlsrv_configure](../../connect/php/sqlsrv-configure.md) ou alterar o arquivo php.ini. Você pode registrar em log a atividade de inicializações, conexões, instruções ou funções de erro. Você também pode especificar se deseja registrar em log erros, avisos, notificações ou todos os três.  
  
> [!NOTE]  
> Você pode configurar o local do arquivo de log no arquivo php.ini.  
  
### <a name="turning-logging-on"></a>Ativando o registro em log  
Você pode ativar o registro em log usando a função [sqlsrv_configure](../../connect/php/sqlsrv-configure.md) para especificar um valor para a configuração **LogSubsystems**. Por exemplo, a seguinte linha de código configura o driver para registrar em log a atividade de conexões:  
  
`sqlsrv_configure("LogSubsystems", SQLSRV_LOG_SYSTEM_CONN);`  
  
A tabela a seguir descreve as constantes que podem ser usadas como o valor para a configuração **LogSubsystems** :  
  
|Valor (inteiro equivalente entre parênteses)|DESCRIÇÃO|  
|-----------------------------------------------|---------------|  
|SQLSRV_LOG_SYSTEM_ALL (-1)|Ativa o registro em log de todos os subsistemas.|  
|SQLSRV_LOG_SYSTEM_OFF (0)|Desativa o registro em log. Esse é o padrão.|  
|SQLSRV_LOG_SYSTEM_INIT (1)|Ativa o registro em log da atividade de inicialização.|  
|SQLSRV_LOG_SYSTEM_CONN (2)|Ativa o registro em log da atividade de conexão.|  
|SQLSRV_LOG_SYSTEM_STMT (4)|Ativa o registro em log da atividade de instrução.|  
|SQLSRV_LOG_SYSTEM_UTIL (8)|Ativa o registro em log da atividade de funções de erro (como handle_error e handle_warning).|  
  
Você pode definir mais de um valor por vez para a configuração **LogSubsystems** usando o operador lógico OR (|). Por exemplo, a linha de código a seguir ativa o registro em log da atividade de conexões e instruções:  
  
`sqlsrv_configure("LogSubsystems", SQLSRV_LOG_SYSTEM_CONN | SQLSRV_LOG_SYSTEM_STMT);`  
  
Você também pode ativar o registro em log especificando um valor inteiro para a configuração **LogSubsystems** no arquivo php.ini. Por exemplo, se adicionar a seguinte linha à seção `[sqlsrv]` do arquivo php.ini, você ativará o registro em log da atividade de conexão:  
  
`sqlsrv.LogSubsystems = 2`  
  
Adicionando valores inteiros juntos, você pode especificar mais de uma opção por vez. Por exemplo, se adicionar a seguinte linha à seção `[sqlsrv]` do arquivo php.ini, você ativará o registro em log da atividade de conexão e de instrução:  
  
`sqlsrv.LogSubsystems = 6`  
  
### <a name="logging-errors-warnings-and-notices"></a>Registrando erros, avisos e notificações em log  
Depois de ativar o registro em log, você deve especificar o que registrar. Você pode registrar um ou mais dos seguintes: erros, avisos e notificações. Por exemplo, a linha de código a seguir especifica que somente os avisos são registrados em log:  
  
`sqlsrv_configure("LogSeverity", SQLSRV_LOG_SEVERITY_WARNING);`  
  
> [!NOTE]  
> A configuração padrão para **LogSeverity** é **SQLSRV_LOG_SEVERITY_ERROR**. Se o registro em log for ativado e nenhuma configuração de **LogSeverity** for especificada, somente erros serão registrados.  
  
A tabela a seguir descreve as constantes que podem ser usadas como o valor para a configuração **LogSeverity** :  
  
|Valor (inteiro equivalente entre parênteses)|DESCRIÇÃO|  
|-----------------------------------------------|---------------|  
|SQLSRV_LOG_SEVERITY_ALL (-1)|Especifica que erros, avisos e notificações são registrados em log.|  
|SQLSRV_LOG_SEVERITY_ERROR (1)|Especifica que os erros serão registrados em log. Esse é o padrão.|  
|SQLSRV_LOG_SEVERITY_WARNING (2)|Especifica que os avisos serão registrados em log.|  
|SQLSRV_LOG_SEVERITY_NOTICE (4)|Especifica que as notificações serão registradas em log.|  
  
Você pode definir mais de um valor por vez para a configuração **LogSeverity** usando o operador lógico OR (|). Por exemplo, a linha de código a seguir especifica que erros e avisos devem ser registrados em log:  
  
`sqlsrv_configure("LogSeverity", SQLSRV_LOG_SEVERITY_ERROR | SQLSRV_LOG_SEVERITY_WARNING);`  
  
> [!NOTE]  
> Especificar um valor para a configuração **LogSeverity** não ativa o registro em log. Você deve ativar o registro em log especificando um valor para a configuração **LogSubsystems** e depois especificar a severidade do que é registrado em log definindo um valor para **LogSeverity**.  
  
Você também pode especificar uma configuração para a configuração **LogSeverity** usando valores inteiros no arquivo php.ini. Por exemplo, se adicionar a seguinte linha à seção `[sqlsrv]` do arquivo php.ini, você habilitará o registro em log apenas de avisos:  
  
`sqlsrv.LogSeverity = 2`  
  
Adicionando valores inteiros juntos, você pode especificar mais de uma opção por vez. Por exemplo, se adicionar a seguinte linha à seção `[sqlsrv]` do arquivo php.ini, você habilitará o registro em log de erros e de avisos:  
  
`sqlsrv.LogSeverity = 3`  
  
## <a name="see-also"></a>Consulte Também  
[Guia de programação do Microsoft Drivers para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Constantes &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[sqlsrv_configure](../../connect/php/sqlsrv-configure.md)

[sqlsrv_get_config](../../connect/php/sqlsrv-get-config.md)

[Referência da API do driver SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)  
  
