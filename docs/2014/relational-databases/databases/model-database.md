---
title: Modelo de banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 10/02/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- template databases [SQL Server]
- model database [SQL Server], about model databases
- model database [SQL Server]
ms.assetid: 4e4f739b-fd27-4dce-8be6-3d808040d8d7
author: stevestein
ms.author: sstein
ms.openlocfilehash: 298723c5031299b1b105f686e188e1e27cfd758c
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965860"
---
# <a name="model-database"></a>Banco de dados modelo
  O banco de dados **modelo** é usado como modelo para todos os bancos de dados criados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Como **tempdb** é criado toda vez que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é iniciado, o banco de dados **modelo** deve sempre existir em um sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Todo o conteúdo do banco de dados **modelo** , incluindo as opções, é copiado para o novo banco de dados. Algumas configurações do **modelo** também são usadas para criar um novo **tempdb** durante a inicialização, de modo que um banco de dados **modelo** sempre deve existir em um sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Bancos de dados de usuários recém-criados usam o mesmo [modelo de recuperação](../backup-restore/recovery-models-sql-server.md) do banco de dados modelo. O padrão é configurável pelo usuário. Para saber mais sobre o modelo de recuperação atual do modelo, veja [Exibir ou alterar o modelo de recuperação de um banco de dados &#40;SQL Server&#41;](../backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
> [!IMPORTANT]  
>  Se você modificar o banco de dados **model** com informações de modelo específicas do usuário, recomendamos que faça backup de **modelo**. Para obter mais informações, consulte [Fazer backup e restaurar bancos de dados do sistema &#40;SQL Server&#41;](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
## <a name="model-usage"></a>Uso do modelo  
 Quando uma instrução CREATE DATABASE é emitida, a primeira parte do banco de dados é criada por meio de cópia do conteúdo do banco de dados **modelo** . O restante do novo banco de dados é então preenchido com páginas vazias.  
  
 Se o banco de dados **modelo** for modificado, todos os bancos de dados criados posteriormente herdarão as mudanças. Por exemplo, você poderia definir permissões ou opções de banco de dados, ou adicionar objetos, como tabelas, funções ou procedimentos armazenados. Propriedades de arquivo do banco de dados **modelo** são uma exceção e são ignoradas, exceto o tamanho inicial do arquivo de dados.  
  
## <a name="physical-properties-of-model"></a>Propriedades físicas de modelo  
 A tabela a seguir lista os valores iniciais de configuração dos dados do **modelo** e dos arquivos de log. Os tamanhos desses arquivos podem variar ligeiramente das diferentes edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Arquivo|Nome lógico|Nome físico|Aumento do arquivo|  
|----------|------------------|-------------------|-----------------|  
|Dados primários|modeldev|model.mdf|Aumento automático de 10 por cento até que o disco fique cheio.|  
|Log|modellog|modellog.ldf|Aumento automático de 10 por cento para um máximo de 2 terabytes.|  
  
 Para mover o banco de dados **model** ou os arquivos de log, veja [Mover bancos de dados do sistema](system-databases.md).  
  
### <a name="database-options"></a>Opções de banco de dados  
 A tabela a seguir lista o valor padrão de cada opção de banco de dados no banco de dados **modelo** e se a opção pode ser modificada. Para exibir as configurações atuais dessas opções, use a exibição de catálogo [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) .  
  
|Opção de banco de dados|Valor padrão|Pode ser modificado|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|Sim|  
|ANSI_NULL_DEFAULT|OFF|Sim|  
|ANSI_NULLS|OFF|Sim|  
|ANSI_PADDING|OFF|Sim|  
|ANSI_WARNINGS|OFF|Sim|  
|ARITHABORT|OFF|Sim|  
|AUTO_CLOSE|OFF|Sim|  
|AUTO_CREATE_STATISTICS|ATIVADO|Sim|  
|AUTO_SHRINK|OFF|Sim|  
|AUTO_UPDATE_STATISTICS|ATIVADO|Sim|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|Sim|  
|CHANGE_TRACKING|OFF|Não|  
|CONCAT_NULL_YIELDS_NULL|OFF|Sim|  
|CURSOR_CLOSE_ON_COMMIT|OFF|Sim|  
|CURSOR_DEFAULT|GLOBAL|Sim|  
|Opções de disponibilidade de banco de dados|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|Não<br /><br /> Sim<br /><br /> Sim|  
|DATE_CORRELATION_OPTIMIZATION|OFF|Sim|  
|DB_CHAINING|OFF|Não|  
|ENCRYPTION|OFF|Não|  
|NUMERIC_ROUNDABORT|OFF|Sim|  
|PAGE_VERIFY|CHECKSUM|Sim|  
|PARAMETERIZATION|SIMPLES|Sim|  
|QUOTED_IDENTIFIER|OFF|Sim|  
|READ_COMMITTED_SNAPSHOT|OFF|Sim|  
|RECOVERY|Depende da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] edição<sup>1</sup>|Sim|  
|RECURSIVE_TRIGGERS|OFF|Sim|  
|Opções do Service Broker|DISABLE_BROKER|Não|  
|TRUSTWORTHY|OFF|Não|  
  
 <sup>1</sup> para verificar o modelo de recuperação atual do banco de dados, confira [Exibir ou alterar o modelo de recuperação de um banco de dados &#40;SQL Server&#41;](../backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md) ou [sys. databases &#40;&#41;do Transact-SQL ](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql).  
  
 Para obter uma descrição dessas opções de banco de dados, veja [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql).  
  
## <a name="restrictions"></a>Restrições  
 As operações a seguir não podem ser executadas no banco de dados **modelo** :  
  
-   Adicionando arquivos ou grupos de arquivos.  
  
-   Alteração de ordenação. A ordenação padrão é a ordenação do servidor.  
  
-   Alteração do proprietário do banco de dados. **modelo** pertence a **sa**.  
  
-   Descartando o banco de dados.  
  
-   Descartando o usuário **convidado** do banco de dados.  
  
-   Habilitação do Change Data Capture.  
  
-   Participação no espelhamento de banco de dados.  
  
-   Remoção do grupo de arquivos primário, arquivo de dados primário ou arquivo de log.  
  
-   Renomeação do banco de dados ou grupo de arquivos primário.  
  
-   Definindo o banco de dados como OFFLINE.  
  
-   Definindo o banco de dados ou grupo de arquivos primário como READ_ONLY.  
  
-   Criando procedimentos, exibições ou gatilhos que usam a opção WITH ENCRYPTION. A chave de criptografia é associada ao banco de dados no qual o objeto é criado. Objetos criptografados criados no banco de dados **modelo** só podem ser usados em **modelo**.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Bancos de dados do sistema](system-databases.md)  
  
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
 [Mover arquivos de banco de dados](move-database-files.md)  
  
  
