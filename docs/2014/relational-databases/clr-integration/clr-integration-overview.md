---
title: Visão geral da integração do CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], about CLR integration
- extended stored procedures [SQL Server], vs. managed code
- objects [CLR integration]
- Transact-SQL vs. managed code
- managed code [SQL Server], vs. Transact-SQL
- managed code [SQL Server], vs. extended stored procedures
- execution at client vs. execution at server [CLR integration]
ms.assetid: 5aa176da-3652-4afa-a742-4c40c77ce5c3
author: rothja
ms.author: jroth
ms.openlocfilehash: 29c6c0195b8a6be73e70542a6b995f46ccaff51b
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84953616"
---
# <a name="overview-of-clr-integration"></a>Visão geral da integração CLR
  O CLR (Common Language Runtime) é o centro do Microsoft .NET Framework; ele fornece o ambiente de execução para todo o código do .NET Framework. O código executado no CLR é chamado de código gerenciado. O CLR fornece diversas funções e serviços necessários para a execução de programas, incluindo a compilação JIT (Just-In-Time), alocação e gerenciamento de memória, imposição de segurança de tipos, tratamento de exceções, gerenciamento de threads e segurança.  Consulte o SDK do .NET Framework para obter mais informações.  
  
 Com o CLR hospedado no Microsoft SQL Server (a chamada integração CLR), você pode criar procedimentos armazenados, gatilhos, funções definidas pelo usuário, tipos definidos pelo usuário e agregações definidas pelo usuário no código gerenciado. Como o código gerenciado é compilado em código nativo antes da execução, você pode obter aumentos significativos de desempenho em alguns cenários.  
  
 O código gerenciado usa a CAS (segurança de acesso do código) para impedir que os assemblies executem determinadas operações. O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa a CAS para ajudar a proteger o código gerenciado e evitar o comprometimento do sistema operacional ou do servidor de banco de dados.  
  
## <a name="advantages-of-clr-integration"></a>Vantagens da integração CLR  
 O [!INCLUDE[tsql](../../../includes/tsql-md.md)] foi especificamente projetado para a manipulação e o acesso direto a dados no banco de dados. Embora o [!INCLUDE[tsql](../../../includes/tsql-md.md)] se destaque no gerenciamento e no acesso a dados, ele não é uma linguagem de programação totalmente desenvolvida. Por exemplo, o [!INCLUDE[tsql](../../../includes/tsql-md.md)] não oferece suporte a matrizes, coleções, loops for-each, deslocamento de bit ou classes. Embora algumas dessas construções possam ser simuladas no [!INCLUDE[tsql](../../../includes/tsql-md.md)], o código gerenciado oferece suporte integrado a elas. Dependendo do cenário, esses recursos podem representar um motivo convincente para implementar determinada funcionalidade de banco de dados no código gerenciado.  
  
 O Microsoft Visual Basic .NET e o Microsoft Visual C# oferecem recursos orientados a objeto, como encapsulamento, herança e polimorfismo. Agora, o código relacionado pode ser facilmente organizado em classes e namespaces. Ao trabalhar com grandes quantidades de código de servidor, isso permite organizar e manter seu código de forma mais fácil.  
  
 O código gerenciado é mais adequado do que o [!INCLUDE[tsql](../../../includes/tsql-md.md)] para cálculos e lógica de execução complicada, além de oferecer suporte amplo a diversas tarefas complexas, incluindo o tratamento de cadeias de caracteres e as expressões regulares. Com a funcionalidade que se encontra na Biblioteca do .NET Framework, você tem acesso a milhares de classes e rotinas pré-criadas. Elas podem ser acessadas facilmente de qualquer procedimento armazenado, gatilho ou função definida pelo usuário. A BCL (Base Class Library) inclui classes que fornecem funcionalidade para manipulação de cadeias de caracteres, operações matemáticas avançadas, acesso a arquivos, criptografia e outros.  
  
> [!NOTE]  
>  Várias dessas classes estão disponíveis para uso a partir do código CLR no SQL Server, mas aquelas que não são apropriadas para uso do servidor (por exemplo, classes de janelas) não estão disponíveis. Para obter mais informações, consulte [bibliotecas de .NET Framework com suporte](database-objects/supported-net-framework-libraries.md).  
  
 Uma das vantagens do código gerenciado é a segurança de tipos ou a garantia de que o código acesse apenas os tipos de modos permitidos e bem definidos. Antes da execução do código gerenciado, o CLR verifica se o código é seguro. Por exemplo, o código é verificado para assegurar que nenhuma memória que não tenha sido gravada anteriormente seja lida. O CLR também pode ajudar garantir que o código não manipule a memória não gerenciada.  
  
 A integração CLR oferece a possibilidade de melhorar o desempenho. Para obter informações, consulte [desempenho da integração CLR](clr-integration-architecture-performance.md).  
  
## <a name="choosing-between-transact-sql-and-managed-code"></a>Escolhendo entre o Transact-SQL e o código gerenciado  
 Ao escrever procedimentos armazenados, gatilhos e funções definidas pelo usuário, você deve decidir se deseja usar o [!INCLUDE[tsql](../../../includes/tsql-md.md)] tradicional ou uma linguagem do .NET Framework, como Visual Basic .NET ou Visual C#. Use o [!INCLUDE[tsql](../../../includes/tsql-md.md)] quando o código executar o acesso a dados principalmente com pouca ou nenhuma lógica de procedimento. Use o código gerenciado para funções que utilizam intensamente a CPU e procedimentos que apresentam lógica complexa, ou quando desejar usar a BCL do .NET Framework.  
  
### <a name="choosing-between-execution-in-the-server-and-execution-in-the-client"></a>Escolhendo entre a execução no servidor e a execução no cliente  
 Outro fator que influencia sua decisão de usar o [!INCLUDE[tsql](../../../includes/tsql-md.md)] ou o código gerenciado é o local onde o código residirá: no computador servidor ou no computador cliente. Tanto o [!INCLUDE[tsql](../../../includes/tsql-md.md)] quanto o código gerenciado podem ser executados no servidor. Assim, o código e os dados ficam próximos, o que possibilita o aproveitamento do poder de processamento do servidor. Por outro lado, talvez você queira evitar colocar tarefas que utilizam intensamente o processador no servidor de banco de dados. Atualmente, a maioria dos computadores cliente tem uma capacidade grande, e talvez você queira aproveitar esse poder de processamento colocando a maior quantidade de código possível no cliente. O código gerenciado pode ser executado em um computador cliente, o que não ocorre com o [!INCLUDE[tsql](../../../includes/tsql-md.md)].  
  
## <a name="choosing-between-extended-stored-procedures-and-managed-code"></a>Escolhendo entre procedimentos armazenados estendidos e o código gerenciado  
 Os procedimentos armazenados estendidos podem ser criados de forma a executar funcionalidades que não são possíveis com os procedimentos armazenados do [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Porém, os procedimentos armazenados estendidos podem comprometer a integridade do processo do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o que não ocorre com o código gerenciado, que é verificado para assegurar que é fortemente tipado. Além disso, o gerenciamento da memória, o agendamento de threads e fibras, e os serviços de sincronização são integrados de forma mais aprofundada entre o código gerenciado do CLR e o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Com a integração CLR, você tem uma forma mais segura do que os procedimentos armazenados estendidos para gravar os procedimentos armazenados necessários à execução de tarefas que não são possíveis no [!INCLUDE[tsql](../../../includes/tsql-md.md)]. Para obter mais informações sobre integração CLR e procedimentos armazenados estendidos, consulte [desempenho da integração CLR](clr-integration-architecture-performance.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Instalando o .NET Framework](https://technet.microsoft.com/library/ms166014\(v=SQL.105\).aspx)   
 [Arquitetura da integração CLR](../../database-engine/dev-guide/architecture-of-clr-integration.md)   
 [Acesso a dados de objetos de banco de dado CLR](data-access/data-access-from-clr-database-objects.md)   
 [Introdução à integração CLR](database-objects/getting-started-with-clr-integration.md)  
  
  
