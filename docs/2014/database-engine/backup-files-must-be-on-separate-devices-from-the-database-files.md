---
title: Os arquivos de backup devem estar em dispositivos separados dos arquivos de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 7039bebb-1f25-4cf3-81f1-393dfb78da12
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: d5eff9cb3139e1e1043f99ba63d11160b1010c27
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936141"
---
# <a name="backup-files-must-be-on-separate-devices-from-the-database-files"></a>Arquivos de backup devem estar em dispositivos separados dos arquivos de banco de dados
  Esta regra verifica se os arquivos de banco de dados estão em dispositivos separados dos arquivos de backup. Se os arquivos de banco de dados e os arquivos de backup estiverem no mesmo dispositivo e o dispositivo falhar, o banco de dados e os backups não estarão disponíveis. Além disso, colocar arquivos de banco de dados e de backup em dispositivos separados otimiza o desempenho de E/S para o uso de produção do banco de dados e a gravação de backups.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 É extremamente recomendável que você coloque o banco de dados e os backups em dispositivos de backup separados.  
  
> [!NOTE]  
>  Essa política não pode detectar dispositivos físicos separados por pontos de montagem.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Dispositivos de backup &#40;SQL Server&#41;](../relational-databases/backup-restore/backup-devices-sql-server.md)  
  
 [Fazer backup e restaurar bancos de dados do SQL Server](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor práticas recomendadas usando o Gerenciamento Baseado em Políticas](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
