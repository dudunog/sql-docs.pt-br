---
title: Backup desatualizado | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 307a4ad0-675a-4f97-9a3c-cedd61bdfae5
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 929262bc559730b99407415a9b907091a479289f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68087030"
---
# <a name="outdated-backup"></a>Backup desatualizado
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Esta regra verifica se um banco de dados possui backups recentes. Programar backups regulares é importante para proteger os bancos de dados contra perda de dados de muitas falhas diferentes. A frequência apropriada para fazer backup de dados depende do modelo de recuperação do banco de dados, dos requisitos do negócio sobre uma possível perda de dados e da frequência em que o banco de dados é atualizado. Em um banco de dados atualizado frequentemente, a exposição à perda de trabalho aumenta rapidamente entre backups.  
  
## <a name="best-practices-recommendations"></a>Práticas Recomendadas  
 Recomendamos que você execute backups com frequência para proteger os bancos de dados contra perda de dados.  
  
 O modelo de recuperação simples e modelo de recuperação completa exigem backups de dados. Para qualquer modelo de recuperação, é possível complementar os backups completos com backups diferenciais para reduzir com eficiência o risco de perda de dados.  
  
 Para um banco de dados que usa o modelo de recuperação completa, recomendamos que faça backups de log frequentes. Para um banco de dados de produção que contém dados muito importantes, os backups de log normalmente são feitos em intervalos de um a quinze minutos.  
  
> [!NOTE]  
>  O método recomendado para agendar backups é um plano de manutenção de banco de dados.  
  
## <a name="for-more-information"></a>Para obter mais informações  
 [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)  
  
 [Modelos de recuperação &#40;SQL Server&#41;](../../relational-databases/backup-restore/recovery-models-sql-server.md)  
  
 [Criar um backup diferencial de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
 [Criar um backup completo de banco de dados &#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
 [Planos de manutenção](../../relational-databases/maintenance-plans/maintenance-plans.md)  
  
 [Backups de log de transações &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e impor melhores práticas usando o gerenciamento baseado em políticas](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
