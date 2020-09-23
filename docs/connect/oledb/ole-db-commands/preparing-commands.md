---
title: Preparando comandos (driver do OLE DB)
description: Para um único comando executado várias vezes, o Driver do OLE DB para SQL Server dá suporte à preparação de comandos para melhorar o desempenho.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, commands
- prepared statements [OLE DB Driver for SQL Server]
- commands [OLE DB]
- command preparation [OLE DB Driver for SQL Server]
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5b2bb5f167361ad5fec4a5580c49378144cbbf26
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88862421"
---
# <a name="preparing-commands"></a>Preparando comandos
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  O OLE DB Driver for SQL Server dá suporte à preparação de comando para várias execuções otimizadas de um único comando. No entanto, a preparação de comando gera sobrecarga e um consumidor não precisa preparar um comando para executá-lo mais de uma vez. Em geral, um comando deverá ser preparado se for executado mais de três vezes.  
  
 Por razões de desempenho, a preparação é adiada até que o comando seja executado. Esse é o comportamento padrão. Não são conhecidos erros no comando que está sendo preparada até que ele seja executado ou uma operação de metapropriedade seja executada. Definir a propriedade SSPROP_DEFERPREPARE do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como FALSE pode desativar esse comportamento padrão.  
  
 No [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], quando um comando é executado diretamente (sem prepará-lo primeiro), um plano de execução é criado e armazenado em cache. Caso a instrução SQL seja executada novamente, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conta com um algoritmo eficiente que compara a nova instrução com o plano de execução existente no cache e reutiliza o plano nessa instrução.  
  
 Em comandos preparados, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fornece suporte nativo à preparação e à execução das instruções de comando. Quando você prepara uma instrução, o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cria um plano de execução, o armazena em cache e retorna um identificador desse plano para o provedor. Em seguida, o provedor usa esse identificador para executar a instrução repetidamente. Não é criado nenhum procedimento armazenado. Como o identificador aponta diretamente o plano de execução de uma instrução SQL, e não a correspondência entre a instrução e o plano de execução no cache (como acontece com a execução direta), é mais eficiente preparar uma instrução do que executá-la diretamente, caso você saiba que ela será executada mais de uma vez.  
  
 No [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], as instruções preparadas não podem ser usadas para criar objetos temporários e referenciar procedimentos armazenados do sistema que criam objetos temporários, como tabelas temporárias. Esses procedimentos devem ser executados diretamente.  
  
 Alguns comandos jamais devem ser preparados. Por exemplo, os comandos que especificam a execução de procedimento armazenado ou incluem texto tendo em vista a criação do procedimento armazenado do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] jamais devem ser preparados.  
  
 Caso um procedimento armazenado temporário seja criado, o OLE DB Driver for SQL Server o executará, retornando resultados como se a instrução propriamente dita fosse executada.  
  
 A criação do procedimento armazenado temporário é controlada pela propriedade de inicialização SSPROP_INIT_USEPROCFORPREP, específica do OLE DB Driver for SQL Server. Caso o valor da propriedade seja SSPROPVAL_USEPROCFORPREP_ON ou SSPROPVAL_USEPROCFORPREP_ON_DROP, o OLE DB Driver for SQL Server tentará criar um procedimento armazenado durante a preparação de um comando. A criação do procedimento armazenado tem êxito caso o usuário do aplicativo tenha permissões suficientes no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 Para clientes que não costumam se desconectar, a criação de procedimentos armazenados temporários pode exigir recursos significativos de **tempdb**, o banco de dados do sistema do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], no qual os objetos temporários são criados. Quando o valor de SSPROP_INIT_USEPROCFORPREP é SSPROPVAL_USEPROCFORPREP_ ON, os procedimentos armazenados temporários criados pelo OLE DB Driver for SQL Server só são descartados quando a sessão que criou o comando perde a conexão com a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Caso essa conexão seja a padrão criada na inicialização da fonte de dados, o procedimento armazenado temporário só é descartado quando a fonte de dados deixa de ser inicializada.  
  
 Quando o valor de SSPROP_INIT_USEPROCFORPREP é SSPROPVAL_USEPROCFORPREP_ON_DROP, os procedimentos armazenados temporários do OLE DB Driver for SQL Server são removidos quando ocorre uma das seguintes condições:  
  
-   O consumidor usa **ICommandText::SetCommandText** para indicar um novo comando.  
  
-   O consumidor usa **ICommandPrepare::Unprepare** para indicar que deixou de exigir o texto de comando.  
  
-   O consumidor libera todas as referências ao objeto de comando que usa o procedimento armazenado temporário.  
  
 Um objeto de comando tem, no máximo, um procedimento armazenado temporário em **tempdb**. Qualquer procedimento armazenado temporário existente representa o texto de comando atual de um objeto de comando específico.  
  
## <a name="see-also"></a>Consulte Também  
 [Comandos](../../oledb/ole-db-commands/commands.md)  
  
  
