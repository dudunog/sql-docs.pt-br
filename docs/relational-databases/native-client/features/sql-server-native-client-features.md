---
title: Recursos
description: Além de expor os recursos dos componentes de acesso a dados do Windows, SQL Server Native Client implementa outros recursos para expor SQL Server funcionalidade.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- MDAC [SQL Server]
- SQL Server Native Client ODBC driver, about SQL Server Native Client ODBC driver
- SQLNCLI, about SQL Server Native Client
- data access [SQL Server Native Client], features
ms.assetid: 7bb32865-5afb-41ab-98b4-3fa545ee8953
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: ec878229524d048969acbf3ca1af7cca4e318084
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008997"
---
# <a name="sql-server-native-client-features"></a>Recursos do SQL Server Native Client
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Além de expor os recursos do WDAC (Windows (anteriormente Microsoft) Data Access Components), o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client também implementa vários outros recursos para expor a funcionalidade do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>Nesta seção  
 [Alteração de comportamento do driver ODBC ao lidar com conversões de caracteres](../../../relational-databases/native-client/features/odbc-driver-behavior-change-when-handling-character-conversions.md)  
 Discute uma alteração de comportamento a partir do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 2012 Native Client.  
  
 [Usando o espelhamento de banco de dados](../../../relational-databases/native-client/features/using-database-mirroring.md)  
 Discute como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o Native Client dá suporte ao uso de bancos de dados espelhados, que é a capacidade de manter uma cópia, ou espelho, de um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados em um servidor em espera.  
  
 [Executando operações assíncronas](../../../relational-databases/native-client/features/performing-asynchronous-operations.md)  
 Aborda como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oferece suporte a operações assíncronas, o que possibilita o retorno imediato sem bloqueio no thread que fez a chamada.  
  
 [Usando MARS &#40;Multiple Active Result Sets&#41;](../../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)  
 Aborda como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oferece suporte a MARS (vários conjuntos de resultados ativos). Os MARS permitem executar e receber vários conjuntos de resultados por meio de uma única conexão de banco de dados.  
  
 [Usando tipos de dados XML](../../../relational-databases/native-client/features/using-xml-data-types.md)  
 Aborda como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oferece suporte ao tipo de dados XML, um tipo de dados baseado em XML que pode ser usado como um tipo de coluna, um tipo de variável, um tipo de parâmetro ou um tipo de retorno de função.  
  
 [Usando tipos definidos pelo usuário](../../../relational-databases/native-client/features/using-user-defined-types.md)  
 Discute como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o Native Client dá suporte a UDT (tipos definidos pelo usuário), que estende o sistema de tipos SQL, permitindo que você armazene objetos e estruturas de dados personalizadas em um banco de dado [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 [Usando tipos de valor grande](../../../relational-databases/native-client/features/using-large-value-types.md)  
 Aborda como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oferece suporte a tipos de dados de valor grande, que são tipos de dados LOB (objeto binário grande).  
  
 [Alterando senhas programaticamente](../../../relational-databases/native-client/features/changing-passwords-programmatically.md)  
 Aborda como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oferece suporte ao tratamento de senhas expiradas de forma que as senhas agora possam ser alteradas no cliente sem o envolvimento do administrador.  
  
 [Trabalhando com isolamento de instantâneo](../../../relational-databases/native-client/features/working-with-snapshot-isolation.md)  
 Aborda como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oferece suporte ao aprimoramento do controle de versão de linha que melhora o desempenho do banco de dados ao evitar cenários de bloqueio de leitor/gravador.  
  
 [Trabalhando com notificações de consulta](../../../relational-databases/native-client/features/working-with-query-notifications.md)  
 Aborda como o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client oferece suporte à notificação do consumidor na modificação do conjunto de linhas.  
  
 [Executando operações de cópia em massa](../../../relational-databases/native-client/features/performing-bulk-copy-operations.md)  
 Discute como [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o Native Client dá suporte a operações de cópia em massa que permitem a transferência de grandes quantidades de dados para dentro ou para fora de uma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabela ou exibição.  
  
 [Usando criptografia sem validação](../../../relational-databases/native-client/features/using-encryption-without-validation.md)  
 Aborda como usar o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para criptografar dados enviados para o servidor sem validar o certificado.  
  
 [Os parâmetros com valor de tabela &#40;SQL Server Native Client&#41;](../../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md)  
 Aborda o suporte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client aos parâmetros com valor de tabela.  
  
 [Tipos de dados CLR grandes definidos pelo usuário](../../../relational-databases/native-client/features/large-clr-user-defined-types.md)  
 Aborda o suporte a UDTs CLR (Common Language Runtime) grandes.  
  
 [Suporte a FILESTREAM](../../../relational-databases/native-client/features/filestream-support.md)  
 Discute [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o suporte de cliente nativo para o recurso de fluxo de recursos avançado.  
  
 [Suporte a SPN &#40;Nome da Entidade de Serviço&#41; em conexões com o cliente](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)  
 Aborda como o suporte a SPNs (nomes da entidade de serviço) foi estendido para possibilitar autenticação mútua em todos os protocolos.  
  
 [Suporte a colunas esparsas no SQL Server Native Client](../../../relational-databases/native-client/features/sparse-columns-support-in-sql-server-native-client.md)  
 Aborda o suporte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client a colunas esparsas.  
  
 [Melhorias de data e hora](../../../relational-databases/native-client/features/date-and-time-improvements.md)  
 Aborda o suporte adicionado ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para os novos tipos de dados de data e hora.  
  
 [Descoberta de metadados](../../../relational-databases/native-client/features/metadata-discovery.md)  
 Discute melhorias de descoberta de metadados que foram feitas no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Suporte a UTF-16 no SQL Server Native Client 11.0](../../../relational-databases/native-client/features/utf-16-support-in-sql-server-native-client-11-0.md)  
 Discute uma alteração no comportamento apresentada no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. Se você fornecer um buffer de comprimento fixo ao associar um resultado de coluna ou um parâmetro de saída e se o caractere **WCHAR** gravado no buffer antes do caractere de terminação for um ponto de código substituto alto de um par substituto, e se o próximo caractere **WCHAR** for um ponto de código substituto baixo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o Native Client não adicionará o ponto de código substituto alto ao buffer.  
  
 [Suporte do SQL Server Native Client à alta disponibilidade e recuperação de desastre](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
 Aborda como seu aplicativo pode ser configurado para aproveitar os recursos de alta disponibilidade e de recuperação de desastre adicionados no [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 [Acessando informações de diagnóstico no log de eventos estendidos](../../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)  
 Discute os aprimoramentos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client e o rastreamento de dados que fornece acesso a informações de diagnóstico no buffer de anel e no log de XEvents.  
  
 [Suporte do SQL Server Native Client para LocalDB](../../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md)  
 Discute o suporte do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ao recurso LocalDB.  
  
## <a name="see-also"></a>Consulte Também  
 [Programação de SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)   
 [Tópicos de instruções sobre ODBC](../../../relational-databases/native-client-odbc-how-to/odbc-how-to-topics.md)   
 [Tópicos de instruções sobre OLE DB](../../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)   
 [Instalando o SQL Server Native Client](../../../relational-databases/native-client/applications/installing-sql-server-native-client.md)  
  
  
