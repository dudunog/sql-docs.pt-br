---
description: MSSQLSERVER_1785
title: MSSQLSERVER_1785
ms.custom: ''
ms.date: 12/25/2020
ms.prod: sql
ms.reviewer: ramakoni1, pijocoder, suresh-kandoth, vencher, tejasaks, docast
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 1785 (Database Engine error)
ms.assetid: ''
author: suresh-kandoth
ms.author: ramakoni
ms.openlocfilehash: 0ee5aedf0d0f893552559540e25e18b11b19beac
ms.sourcegitcommit: d819173fb91af6f20ca6ee59686c35c71b060fbc
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/28/2020
ms.locfileid: "97797758"
---
# <a name="mssqlserver_1785"></a>MSSQLSERVER_1785
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

## <a name="details"></a>Detalhes

|Atributo|Valor|
|---|---|
|Nome do Produto|SQL Server|
|ID do evento|1785|
|Origem do Evento|MSSQLSERVER|
|Componente|SQLEngine|
|Nome simbólico|CRTFKINVTOPO|
|Texto da mensagem|A introdução da restrição FOREIGN KEY '%.ls' na tabela '%. ls' pode causar ciclos ou vários caminhos em cascata. Especifique ON DELETE NO ACTION ou ON UPDATE NO ACTION, ou modifique outras restrições FOREIGN KEY.|
||

## <a name="explanation"></a>Explicação

Você recebe essa mensagem de erro porque, no SQL Server, uma tabela não pode aparecer mais de uma vez em uma lista de todas as ações referenciais em cascata que são iniciadas por uma instrução `DELETE` ou `UPDATE`. A árvore de ações referenciais em cascata precisa ter apenas um caminho para uma tabela específica na árvore de ações referenciais em cascata.

Uma mensagem de erro semelhante à seguinte é relatada ao usuário:

> Servidor:  Mensagem 1785, Nível 16, Estado 1, Linha 1 A introdução da restrição FOREIGN KEY 'fk_two' na tabela 'table2 ' pode causar ciclos ou vários caminhos em cascata. Especifique ON DELETE NO ACTION ou ON UPDATE NO ACTION, ou modifique outras restrições FOREIGN KEY. Servidor:  Mensagem 1750, Nível 16, Estado 1, Linha 1 Não foi possível criar a restrição. Confira os erros anteriores

## <a name="user-action"></a>Ação do usuário

Para resolver esse problema, crie uma chave estrangeira que criará um só caminho para uma tabela em uma lista de ações referenciais em cascata.

Imponha a integridade referencial de várias maneiras. A DRI (integridade referencial declarativa) é a maneira mais básica, mas também é a menos flexível. Caso precise obter mais flexibilidade, mas ainda queira ter alto grau de integridade, use gatilhos.

## <a name="more-information"></a>Mais informações

O seguinte código de exemplo é um exemplo de uma tentativa de criação de FOREIGN KEY que gera a mensagem de erro:

```sql
USE tempdb
GO

CREATE TABLE table1 (user_ID INTEGER NOT NULL PRIMARY KEY, user_name
CHAR(50) NOT NULL)
GO

CREATE TABLE table2 (author_ID INTEGER NOT NULL PRIMARY KEY, author_name
CHAR(50) NOT NULL, lastModifiedBy INTEGER NOT NULL, addedby INTEGER NOT NULL)
GO

ALTER TABLE table2 ADD CONSTRAINT fk_one FOREIGN KEY (lastModifiedby)
REFERENCES table1 (user_ID) ON DELETE CASCADE ON UPDATE cascade
GO

ALTER TABLE table2 ADD CONSTRAINT fk_two FOREIGN KEY (addedby)
REFERENCES table1(user_ID) ON DELETE NO ACTION ON UPDATE cascade
GO
--this fails with the error because it provides a second cascading path to table2.

ALTER TABLE table2 ADD CONSTRAINT fk_two FOREIGN KEY (addedby)
REFERENCES table1 (user_ID) ON DELETE NO ACTION ON UPDATE NO ACTION
GO
-- this works.
```

### <a name="see-also"></a>Consulte também

[Integridade referencial em cascata](/sql/relational-databases/tables/primary-and-foreign-key-constraints#referential-integrity)
