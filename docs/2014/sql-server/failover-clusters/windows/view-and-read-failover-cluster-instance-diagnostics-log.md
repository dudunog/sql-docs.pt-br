---
title: Exibir e ler o log de diagnóstico da instância do cluster de failover | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 68074bd5-be9d-4487-a320-5b51ef8e2b2d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 774dc4ec4a02c72420d004909cb7e6ee1b31f3a7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85046072"
---
# <a name="view-and-read-failover-cluster-instance-diagnostics-log"></a>Exibir e ler o log de diagnóstico da instância do cluster de failover
  Todos os erros críticos e eventos de aviso para a DLL de Recursos do SQL Server são gravados no log de eventos do Windows. Um log em execução das informações de diagnóstico específicas do SQL Server é capturado pelo procedimento armazenado do sistema [sp_server_diagnostics &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql) e gravado nos arquivos de log de diagnóstico do cluster de failover do SQL Server (também conhecidos como logs *SQLDIAG*).  
  
-   **Antes de começar:**  [Recomendações](#Recommendations), [Segurança](#Security)  
  
-   **Para exibir o Log de Diagnóstico, usando:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
-   **Para configurar definições do Log de Diagnóstico, usando:** [Transact-SQL](#TsqlConfigure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
 Por padrão, o SQLDIAG é armazenado em uma pasta de LOG local do diretório da instância do SQL Server, por exemplo, ' C\Program Files\Microsoft SQL Server\MSSQL12. \<InstanceName> \MSSQL\LOG ' do nó proprietário da FCI (instância de cluster de failover) do AlwaysOn. O tamanho de cada arquivo de log de SQLDIAG é fixo em 100 MB. Dez arquivos de log desse tipo são armazenados no computador antes de serem reciclados para novos logs.  
  
 Os logs usam o formato de arquivo de eventos estendidos. A função do sistema **sys.fn_xe_file_target_read_file** pode ser usada para leitura dos arquivos criados por Eventos Estendidos. É retornado um evento, em formato XML, por linha. Consulte a exibição do sistema para analisar os dados XML como um conjunto de resultados. Para obter mais informações, veja [sys.fn_xe_file_target_read_file &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql).  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 A permissão VIEW SERVER STATE é necessária para executar **fn_xe_file_target_read_file**.  
  
 Abra o SQL Server Management Studio como administrador  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
 **Para exibir os arquivos de log de diagnóstico:**  
  
1.  No menu **Arquivo** , selecione **Abrir**, **Arquivo**e escolha o arquivo de log de diagnóstico a ser exibido.  
  
2.  Os eventos são exibidos como linhas no painel direito e, por padrão, **nome**e **carimbo de data/hora** são as únicas duas colunas exibidas.  
  
     Isso também ativa o menu **ExtendedEvents** .  
  
3.  Para ver mais colunas, vá até o menu **ExtendedEvents** e marque **Selecionar Colunas**.  
  
     Uma caixa de diálogo é aberta com as colunas disponíveis que lhe permitem selecionar as colunas para exibição.  
  
4.  Você pode filtrar e classificar os dados de evento usando o menu **ExtendedEvents** e selecionando a opção **Filtrar** .  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
 **Para exibir os arquivos de log de diagnóstico:**  
  
 Para exibir todos os itens do log no arquivo de log SQLDIAG, use a seguinte consulta:  
  
```  
SELECT  
xml_data.value('(event/@name)[1]','varchar(max)') AS 'Name'  
,xml_data.value('(event/@package)[1]','varchar(max)') AS 'Package'  
,xml_data.value('(event/@timestamp)[1]','datetime') AS 'Time'  
,xml_data.value('(event/data[@name=''state'']/value)[1]','int') AS 'State'  
,xml_data.value('(event/data[@name=''state_desc'']/text)[1]','varchar(max)') AS 'State Description'  
,xml_data.value('(event/data[@name=''failure_condition_level'']/value)[1]','int') AS 'Failure Conditions'  
,xml_data.value('(event/data[@name=''node_name'']/value)[1]','varchar(max)') AS 'Node_Name'  
,xml_data.value('(event/data[@name=''instancename'']/value)[1]','varchar(max)') AS 'Instance Name'  
,xml_data.value('(event/data[@name=''creation time'']/value)[1]','datetime') AS 'Creation Time'  
,xml_data.value('(event/data[@name=''component'']/value)[1]','varchar(max)') AS 'Component'  
,xml_data.value('(event/data[@name=''data'']/value)[1]','varchar(max)') AS 'Data'  
,xml_data.value('(event/data[@name=''info'']/value)[1]','varchar(max)') AS 'Info'  
FROM  
 ( SELECT object_name AS 'event'  
  ,CONVERT(xml,event_data) AS 'xml_data'  
  FROM sys.fn_xe_file_target_read_file('C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Log\SQLNODE1_MSSQLSERVER_SQLDIAG_0_129936003752530000.xel',NULL,NULL,NULL)   
)   
AS XEventData  
ORDER BY Time;  
  
```  
  
> [!NOTE]  
>  Você pode filtrar os resultados para componentes específicos ou um estado usando a cláusula WHERE.  
  
##  <a name="using-transact-sql"></a><a name="TsqlConfigure"></a> Usando o Transact-SQL  
 **Para configurar as propriedades de log de diagnóstico**  
  
> [!NOTE]  
>  Para obter um exemplo desse procedimento, veja [Exemplo (Transact-SQL)](#TsqlExample), mais adiante nesta seção.  
  
 Usando a instrução DDL (linguagem de definição de dados), `ALTER SERVER CONFIGURATION` você pode iniciar ou parar o log de dados de diagnóstico capturados pelo [sp_server_diagnostics &#40;procedimento de&#41;TRANSACT-SQL](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql) e definir parâmetros de configuração de log SQLdiag, como a contagem de sobreposição do arquivo de log, o tamanho do arquivo de log e o local do arquivo. Para obter detalhes da sintaxe, consulte [Setting diagnostic log options](/sql/t-sql/statements/alter-server-configuration-transact-sql#Diagnostic).  
  
###  <a name="examples-transact-sql"></a><a name="ConfigTsqlExample"></a> Exemplos (Transact-SQL)  
  
####  <a name="setting-diagnostic-log-options"></a><a name="TsqlExample"></a>Definindo opções de log de diagnóstico  
 Os exemplos desta seção mostram como definir os valores para a opção de log de diagnóstico.  
  
##### <a name="a-starting-diagnostic-logging"></a>a. Iniciando o log de diagnóstico  
 O exemplo a seguir inicia o log de dados de diagnóstico.  
  
```  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG ON;  
```  
  
##### <a name="b-stopping-diagnostic-logging"></a>B. Interrompendo o log de diagnóstico  
 O exemplo a seguir interrompe o log de dados de diagnóstico.  
  
```  
ALTER SERVER CONFIGURATION SET DIAGNOSTICS LOG OFF;  
```  
  
##### <a name="c-specifying-the-location-of-the-diagnostic-logs"></a>C. Especificando o local dos logs de diagnóstico  
 O exemplo a seguir define o local dos logs de diagnóstico como o caminho do arquivo especificado.  
  
```  
ALTER SERVER CONFIGURATION  
SET DIAGNOSTICS LOG PATH = 'C:\logs';  
```  
  
##### <a name="d-specifying-the-maximum-size-of-each-diagnostic-log"></a>D. Especificando o tamanho máximo de cada log de diagnóstico  
 O exemplo a seguir define o tamanho máximo de cada log de diagnóstico como 10 megabytes.  
  
```  
ALTER SERVER CONFIGURATION   
SET DIAGNOSTICS LOG MAX_SIZE = 10 MB;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Política de failover para instâncias de cluster de failover](failover-policy-for-failover-cluster-instances.md)  
  
  
