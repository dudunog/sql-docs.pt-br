---
title: Restaurar banco de dados (página Arquivos) | Microsoft Docs
description: Enquanto restaura um banco de dados no SQL Server, use a página Arquivos da caixa de diálogo Restaurar Banco de Dados para gerenciar os arquivos específicos escolhidos para restaurar no banco de dados.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.restoredb.files.f1
- sql13.swb.restoredb.files.f1 in the code
ms.assetid: 714c36ea-a9f9-43a4-99f9-a6f73d1baf8e
author: cawrites
ms.author: chadam
ms.openlocfilehash: d94a143eae321f7ea01f97a54b351d72f8142ad6
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96129156"
---
# <a name="restore-database-files-page"></a>Restaurar banco de dados (página de arquivos)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Use a página **Arquivos** da caixa de diálogo **Restaurar Banco de Dados** para gerenciar os arquivos específicos escolhidos para restaurar no banco de dados.  
  
## <a name="options"></a>Opções  
  
### <a name="restore-database-files-as"></a>Restaurar os arquivos do banco de dados como  
 Use atribuir e gerenciar o novo caminho de arquivo para os arquivos restaurados.  
  
 **Realoque todos os arquivos para pasta**  
 Realoque os arquivos restaurados.  
  
|Opção|Descrição|  
|------------|-----------------|  
|**Pasta Arquivo de dados**|Insira ou procure o nome de pasta de arquivo de dados para o qual o arquivo de dados restaurado ou arquivos devem ser realocados.|  
|**Pasta Arquivo de log**|Insira ou procure o arquivo de log ou pasta de arquivos para o qual o arquivo de log deve ser realocado.|  
  
 **Nome do Arquivo Lógico**  
 Exibe uma linha para cada arquivo de banco de dados a ser restaurado.  
  
 **Tipo de arquivo**  
 Exibe o tipo do arquivo.  
  
 **Nome do arquivo original**  
 Exibe o caminho do arquivo original para o arquivo restaurado.  
  
 **Restaurar Como**  
 Lista os nomes de arquivos que renomearão os arquivos restaurados. Insira ou procure o nome de arquivo apropriado.  
  
## <a name="see-also"></a>Consulte Também  
 [Restaurar banco de dados &#40;página Geral&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)   
 [Restaurar banco de dados &#40;página Opções&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)   
 [Argumentos de RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-arguments-transact-sql.md)   
 [Definir um dispositivo de backup lógico para uma unidade de fita &#40;SQL Server&#41;](../../relational-databases/backup-restore/define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)  
  
  
