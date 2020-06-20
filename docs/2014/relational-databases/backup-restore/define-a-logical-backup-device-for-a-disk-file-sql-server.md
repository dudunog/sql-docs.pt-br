---
title: Definir um dispositivo de backup lógico para um arquivo de disco (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- backup devices [SQL Server], defining
- backup devices [SQL Server], disks
- disk backup devices [SQL Server]
- database backups [SQL Server], disks
- backing up databases [SQL Server], disks
ms.assetid: 86331d43-c738-4523-ae3d-7d6700348ed1
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8aa92296da81f984f260deace887c15f13443b95
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84958696"
---
# <a name="define-a-logical-backup-device-for-a-disk-file-sql-server"></a>Definir um dispositivo de backup lógico para um arquivo de disco (SQL Server)
  Este tópico descreve como definir um dispositivo de backup lógico para uma arquivo de disco no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Um dispositivo lógico é um nome definido pelo usuário que aponta para um dispositivo de backup físico específico (um arquivo de disco ou uma unidade de fita).  A inicialização do dispositivo físico acontece depois, quando um backup é gravado no dispositivo de backups.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para definir um dispositivo de backup lógico para um arquivo de disco, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   O nome de dispositivo lógico deve ser exclusivo entre todos os dispositivos de backup lógicos na instância do servidor. Para exibir os nomes de dispositivo lógicos existentes, consulte a exibição de catálogo [sys.backup_devices](/sql/relational-databases/system-catalog-views/sys-backup-devices-transact-sql) .  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Nós recomendamos que um disco de backup seja diferente dos discos de banco de dados e de log. Isso é necessário para garantir que será possível acessar os backups se houver falha no disco de dados ou de log.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer associação na função de servidor fixa **diskadmin** .  
  
 Requer permissão para gravar no disco.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-define-a-logical-backup-device-for-a-disk-file"></a>Para definir um dispositivo de backup lógico para um arquivo de disco  
  
1.  Depois de se conectar à instância apropriada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], em Pesquisador de Objetos, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Objetos de Servidor**e clique com o botão direito do mouse em **Dispositivos de Backup**.  
  
3.  Clique em **Novo Dispositivo de Backup**. A caixa de diálogo **Dispositivo de Backup** é aberta.  
  
4.  Coloque um nome de dispositivo.  
  
5.  Para o destino, clique em **Arquivo** e especifique o caminho completo do arquivo.  
  
6.  Para definir o dispositivo novo, clique em **OK**.  
  
 Para fazer backup neste novo dispositivo, adicione-o ao campo **Fazer backup em:** na caixa de diálogo **Backup de Banco de dados** (**Geral**). Para obter mais informações, veja [Criar um backup completo de banco de dados &#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md).  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-define-a-logical-backup-for-a-disk-file"></a>Para definir um backup lógico para um arquivo de disco  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. Este exemplo mostra como usar [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql) para definir um dispositivo de backup lógico para um arquivo de disco. O exemplo adiciona o dispositivo de backup em disco denominado `mydiskdump`, com o nome físico `c:\dump\dump1.bak`.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_addumpdevice 'disk', 'mydiskdump', 'c:\dump\dump1.bak' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Dispositivos de backup &#40;SQL Server&#41;](backup-devices-sql-server.md)   
 [sys.backup_devices &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-backup-devices-transact-sql)   
 [sp_addumpdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)   
 [sp_dropdevice &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropdevice-transact-sql)   
 [Definir um dispositivo de backup lógico para uma unidade de fita &#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)   
 [Exibir as propriedades e o conteúdo de um dispositivo de backup lógico &#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
  
