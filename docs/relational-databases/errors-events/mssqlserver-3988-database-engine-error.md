---
description: MSSQLSERVER_3988
title: MSSQLSERVER_3988
ms.custom: ''
ms.date: 12/25/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 3988 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 46070023b397f949971cf35a7c6ced936fc91e6d
ms.sourcegitcommit: d819173fb91af6f20ca6ee59686c35c71b060fbc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/28/2020
ms.locfileid: "97797761"
---
# <a name="mssqlserver_3988"></a>MSSQLSERVER_3988
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|3988|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|XACT_UNSUPPORT_PARALLEL_TRAN2|
|Texto da mensagem|Não são permitidas novas transações porque há outros threads em execução na sessão.|
||

## <a name="explanation"></a>Explicação

Esse erro ocorre quando você executa uma consulta distribuída que une várias tabelas hospedadas por instâncias remotas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] enquanto a configuração de sessão `XACT_ABORT` é **ON**. Uma mensagem de erro semelhante à seguinte é relatada ao usuário:

> Mensagem 3988, Nível 16, Estado 1, Linha nº  
Não são permitidas novas transações porque há outros threads em execução na sessão.

## <a name="cause"></a>Causa

Há algumas limitações de design na maneira como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processa as DQs (consultas distribuídas) quando as seguintes condições são verdadeiras:

- O SQL Server une várias tabelas de uma fonte de dados remota do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
- A sessão que emite a consulta não está inscrita em uma transação distribuída.

Nessa situação, uma tentativa de executar a consulta pode gerar um dos dois erros mencionados na seção **Explicação**.

## <a name="user-action"></a>Ação do usuário

Para resolver o problema, coloque a consulta distribuída em uma instrução 'begin distributed transaction':

```sql
BEGIN DISTRIBUTED TRANSACTION <Distributed Query> COMMIT TRANSACTION
```
