---
title: Espaço em disco do log de transações para operações de índice | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- index disk space [SQL Server]
- space [SQL Server], indexes
- transaction logs [SQL Server], disk space
- disk space [SQL Server], transaction logs
- space [SQL Server], transaction logs
ms.assetid: 4f8a4922-4507-4072-be67-c690528d5c3b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 986f464752f631d55b994469b733a3374a1926a5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63161825"
---
# <a name="transaction-log-disk-space-for-index-operations"></a>Espaço em disco de log de transações para operações de índice
  Operações de índice de larga escala podem gerar grandes carregamentos de dados que podem fazer com que o log da transação seja preenchido rapidamente. Para assegurar a reversão da operação de índice, o log da transação não pode ser truncado até que a operação de índice se complete. Durante a operação, no entanto, poderá ser feito backup do log. Portanto, o log de transações deve ter espaço suficiente para armazenar as transações da operação de índice e todas as transações simultâneas de usuário pelo período da operação de índice. Isso é verdade para operações de índice offline e online. Como as tabelas subjacentes não podem ser acessadas durante a operação de índice offline, pode haver poucas transações de usuário e o log pode não crescer na mesma proporção. As operações de índice online não impedem atividades simultâneas de usuário. Por isso, as operações de índice online de larga escala, combinadas com transações simultâneas significativas de usuário, podem causar o crescimento contínuo do log de transações sem opção para truncar o log.  
  
## <a name="recommendations"></a>Recomendações  
 Durante a execução de operações de índice de grande escala, considere estas recomendações:  
  
1.  Verifique se foi feito o backup do log de transações e se ele foi truncado antes de executar as operações de índice online de grande escala, e se o log tem espaço suficiente para armazenar o índice projetado e as transações do usuário.  
  
2.  Considere definir a opção SORT_IN_TEMPDB como ON para a operação de índice. Isso separará as transações de índice das transações de usuário simultâneas. As transações de índice serão armazenadas no log de transações **tempdb** , e as transações de usuário simultâneas serão armazenadas no log de transações do banco de dados de usuário. Isso permitirá que o log de transações do banco de dados de usuário seja truncado durante a operação de índice, se necessário. Além disso, se o log **tempdb** não estiver no mesmo disco do log de banco de dados de usuário, os dois logs não estarão competindo pelo mesmo espaço em disco.  
  
    > [!NOTE]  
    >  Confirme se o banco de dados **tempdb** e o log de transações têm espaço em disco suficiente para controlar a operação de índice. O log de transações **tempdb** não pode ser truncado até que a operação de índice seja concluída.  
  
3.  Use um modelo de recuperação de banco de dados que permita o registro mínimo da operação de índice. Isso poderá reduzir o tamanho do log e impedir que o log preencha o espaço de log.  
  
4.  Não execute a operação de índice online em uma transação explícita. O log não será truncado até que a transação explícita termine.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Requisitos de espaço em disco para operações de DDL de índice](disk-space-requirements-for-index-ddl-operations.md)  
  
 [Exemplo de espaço em disco de índice](index-disk-space-example.md)  
  
  
