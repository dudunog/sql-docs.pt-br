---
description: MSSQLSERVER_3989
title: MSSQLSERVER_3989
ms.custom: ''
ms.date: 12/25/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3989 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 11862d9f21556dd5039024c225b58f5f0f05f9a4
ms.sourcegitcommit: d819173fb91af6f20ca6ee59686c35c71b060fbc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/28/2020
ms.locfileid: "97797746"
---
# <a name="mssqlserver_3989"></a>MSSQLSERVER_3989
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|3989|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|XACT_UNSUPPORT_PARALLEL_TRAN3|
|Texto da mensagem|Não é permitido iniciar uma nova solicitação porque ela deve ter um descritor de transação válido.|
||

## <a name="explanation"></a>Explicação

Esse erro ocorre quando você executa uma consulta distribuída que une várias tabelas hospedadas por instâncias remotas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enquanto a configuração de sessão `XACT_ABORT` é **ON**. Uma mensagem de erro semelhante à seguinte é relatada ao usuário:

> Mensagem 3989, Nível 16, Estado 1, Linha nº  
Não é permitido iniciar uma nova solicitação porque ela deve ter um descritor de transação válido.

## <a name="cause"></a>Causa

Há algumas limitações de design na maneira como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processa as DQs (consultas distribuídas) quando as seguintes condições são verdadeiras:

- O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] une várias tabelas de uma fonte de dados remota do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
- A sessão que emite a consulta não está inscrita em uma transação distribuída.

Nessa situação, uma tentativa de executar a consulta pode gerar um dos dois erros mencionados na seção **Explicação**.

## <a name="user-action"></a>Ação do usuário

Para resolver o problema, coloque a consulta distribuída em uma instrução 'begin distributed transaction':

```sql
BEGIN DISTRIBUTED TRANSACTION <Distributed Query> COMMIT TRANSACTION
```
