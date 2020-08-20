---
description: Criando programas SMO
title: Criando programas SMO | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- Visual Basic [SMO]
- Visual C# [SMO]
- programming [SMO]
- SQL Server Management Objects, programming
- SMO [SQL Server], programming
ms.assetid: 7d2f0bcf-f1ae-45b8-bc3f-7aea4fae7e45
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b55530e34a77878c551dc8ea4ff0fa2936325755
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88490431"
---
# <a name="creating-smo-programs"></a>Criando programas SMO
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  A programação geral de objetos do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO) inclui as áreas comuns compartilhadas por todos os objetos, como a execução de métodos, a configuração de propriedades e a manipulação de coleções.  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Conectando-se a uma instância do SQL Server](../../../relational-databases/server-management-objects-smo/create-program/connecting-to-an-instance-of-sql-server.md)|O programa SMO mais básico que estabelece uma conexão com uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Demonstra a Autenticação do Windows e a Autenticação do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Também inclui exemplos que mostram a conexão com um local e uma instância remota do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Desconectando de uma instância do SQL Server](../../../relational-databases/server-management-objects-smo/create-program/disconnecting-from-an-instance-of-sql-server.md)|Um programa que demonstra como se desconectar da instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[Chamando métodos](../../../relational-databases/server-management-objects-smo/create-program/calling-methods.md)|Esta seção descreve a abordagem geral de chamada de métodos. Mostra o uso de parâmetros e como tratar tabelas de dados retornadas em um objeto <xref:System.Data.DataTable>. Também inclui um exemplo de como chamar um construtor de objeto e como chamar o método **clone** .|  
|[Configurar propriedades – SMO](../../../relational-databases/server-management-objects-smo/create-program/setting-properties-smo.md)|Esta seção descreve como definir diferentes tipos de propriedades. Mostra como definir e obter propriedades de objetos. Também inclui exemplos que definem propriedades de objetos quando o objeto é criado e como iterar por todas as propriedades de um objeto.|  
|[Usando coleções](../../../relational-databases/server-management-objects-smo/create-program/using-collections.md)|Vários programas que discutem as técnicas usadas com coleções de objetos. Mostra como referenciar um objeto usando coleções. Também inclui um exemplo de como iterar pelos membros de uma coleção.|  
|[Manipulando eventos SMO](../../../relational-databases/server-management-objects-smo/create-program/handling-smo-events.md)|Esta seção descreve como configurar e tratar eventos no SMO. Inclui um exemplo de como configurar um manipulador de eventos e como configurar uma assinatura de evento.|  
|[Manipulando exceções SMO](../../../relational-databases/server-management-objects-smo/create-program/handling-smo-exceptions.md)|Esta seção descreve como interceptar exceções no SMO. Inclui exemplos de como capturar uma exceção e como exibir uma exceção interna.|  
|[Trabalhando com tipos de dados](../../../relational-databases/server-management-objects-smo/create-program/working-with-data-types.md)|Esta seção descreve como trabalhar com diferentes tipos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Descreve como construir um tipo de dados com a especificação do construtor de objeto. Também inclui um exemplo de como criar um tipo de dados usando o construtor padrão.|  
|[Usando transações](../../../relational-databases/server-management-objects-smo/create-program/using-transactions.md)|Esta seção descreve como implementar o processamento de transações em um programa SMO. Inclui um exemplo de como usar transações em um programa SMO.|  
|[Usando modo de captura](../../../relational-databases/server-management-objects-smo/create-program/using-capture-mode.md)|Esta seção descreve como registrar a saída do programa SMO. O exemplo registra o programa SMO como instruções [!INCLUDE[tsql](../../../includes/tsql-md.md)] enviadas à instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para execução posterior.|  
  
  
