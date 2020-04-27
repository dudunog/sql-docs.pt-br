---
title: Fazer backup do log de transações quando o banco de dados estiver danificado (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- databases [SQL Server], damaged
- backing up [SQL Server]. damaged database
- transaction log backups [SQL Server], damaged databases
ms.assetid: 9b8873cc-df54-4336-ab9b-8f525132c2b0
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 69e887cc2a8f35710a0c7c910e0e912d6a4a0a61
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62922837"
---
# <a name="back-up-the-transaction-log-when-the-database-is-damaged-sql-server"></a>Fazer backup do log de transações quando o banco de dados está danificado (SQL Server)
  Este tópico descreve como fazer backup de um log de transações quando o banco de dados está danificado no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Recomendações](#Recommendations)  
  
     [Segurança](#Security)  
  
-   **Para fazer backup do log de transações quando o banco de dados está danificado, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   A instrução BACKUP não é permitida em uma transação explícita ou implícita.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Recomendações  
  
-   Para um banco de dados que usa o modelo de recuperação total ou bulk-logged, geralmente você precisa fazer backup do final do log antes de iniciar a restauração do banco de dados. Você também deve fazer backup do final do log do banco de dados primário antes de efetuar o failover de uma configuração de envio de logs. A restauração do backup do final do log como o backup do log final antes de recuperar o banco de dados evita perda de trabalho após uma falha. Para obter mais informações sobre backups da parte final do log, veja [Backups da parte final do log &#40;SQL Server&#41;](tail-log-backups-sql-server.md).  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 As permissões BACKUP DATABASE e BACKUP LOG usam como padrão os membros da função de servidor fixa **sysadmin** e as funções de banco de dados fixas **db_owner** e **db_backupoperator** .  
  
 Os problemas de propriedade e permissão no arquivo físico do dispositivo de backup podem interferir em uma operação de backup. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve ser capaz de ler e gravar no dispositivo; a conta sob a qual o serviço do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] executa deve ter permissões de gravação. No entanto, [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql), que adiciona uma entrada para um dispositivo de backup nas tabelas do sistema, não verifica permissões de acesso a arquivos. Esses problemas no arquivo físico do dispositivo de backup podem não aparecer até que o recurso físico seja acessado quando o backup ou restauração é tentado.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-back-up-the-tail-of-the-transaction-log"></a>Para fazer backup do final do log de transações  
  
1.  Depois de se conectar à instância apropriada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], em Pesquisador de Objetos, clique no nome do servidor para expandir a árvore do servidor.  
  
2.  Expanda **Bancos de Dados**e, dependendo do banco de dados, selecione um banco de dados de usuário ou expanda **Bancos de Dados do Sistema** e selecione um banco de dados do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados, aponte para **Tarefas**e clique em **Backup**. Será exibida a caixa de diálogo **Backup de Banco de Dados** .  
  
4.  Na caixa de listagem **Banco de Dados** , verifique o nome do banco de dados. Você pode, como opção, selecionar um banco de dados diferente da lista.  
  
5.  Verifique se o modelo de recuperação é **FULL** ou **BULK_LOGGED**.  
  
6.  Na caixa de listagem **Tipo de Backup** , selecione **Log de Transações**.  
  
7.  Deixe a opção **Copiar Somente Backup** desmarcada.  
  
8.  Na área **Conjunto de backup** , aceite o nome do conjunto de backup padrão sugerido na caixa de texto **Nome** ou digite um nome diferente para o conjunto de backup.  
  
9. Na caixa de texto **Descrição** , insira uma descrição para o backup da parte final do log.  
  
10. Especifique quando o conjunto de backup irá expirar:  
  
    -   Para que o conjunto de backup expire depois de um número específico de dias, clique em **Depois** (a opção padrão) e digite quantos dias depois da criação do conjunto ele deve expirar. Esse valor pode ser de 0 a 99999 dias; 0 dia significa que o conjunto de backup nunca vai expirar.  
  
         O valor padrão é definido na opção **Retenção de mídia de backup padrão (em dias)** da caixa de diálogo **Propriedades do Servidor** (página**Configurações do Banco de Dados** ). Para acessar essa caixa de diálogo, clique com o botão direito do mouse no nome do servidor no Pesquisador de Objetos, selecione propriedades e a página **Configurações do Banco de Dados** .  
  
    -   Para que o conjunto de backup expire em uma data específica, clique no campo **Em**e digite a data de expiração do conjunto.  
  
11. Escolha o tipo do destino de backup clicando em **Disco** ou **Fita**. Para selecionar os caminhos de até 64 unidades de disco ou fita que contêm um único conjunto de mídia, clique em **Adicionar**. Os caminhos selecionados são exibidos na caixa de listagem **Backup** .  
  
     Para remover um destino de backup, selecione-o e clique em **Remover**. Para exibir o conteúdo de um destino de backup, selecione-o e clique em **Conteúdo**.  
  
12. Na página **Opções** , selecione uma opção **Substituir Mídia** , clicando em uma das opções a seguir:  
  
    -   **Fazer backup no conjunto de mídias existente**  
  
         Para essa opção, clique em **Anexar ao conjunto de backup existente** ou **Substituir todos os conjuntos de backup existentes**.  
  
         Opcionalmente, selecione **Verificar nome do conjunto de mídias e validade do conjunto de backup** para que a operação de backup verifique a data e a hora em que o conjunto de mídias e de backup expiram.  
  
         Como opção, digite um nome na caixa de texto **Nome do conjunto de mídias** . Se nenhum nome for especificado, um conjunto de mídias com um nome em branco será criado. Se você especificar um nome de conjunto de mídias, a mídia (fita ou disco) é verificada para ver se o nome real corresponde ao nome digitado.  
  
         Se você deixar o nome da mídia em branco e marcar a caixa para verificar a mídia, a verificação terá sucesso se o nome da mídia também estiver em branco na mídia.  
  
    -   **Fazer backup em um novo conjunto de mídias e apagar todos os conjuntos de backup existentes**  
  
         Para essa opção, digite um nome na caixa de texto **Nome do novo conjunto de mídias** e, opcionalmente, descreva o conjunto de mídias na caixa de texto **Descrição do novo conjunto de mídias** .  
  
     Para obter mais informações sobre as opções de conjuntos de mídias, veja [Conjuntos de mídias, famílias de mídia e conjuntos de backup &#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md).  
  
13. Na seção **Confiabilidade** , como opção, marque:  
  
    -   **Verificar backup quando concluído**  
  
    -   **Executar soma de verificação antes de gravar na mídia**.  
  
    -   **Continuar em erro de soma de verificação**  
  
     Para obter informações sobre somas de verificação, veja [Erros de mídia possíveis durante backup e restauração &#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md).  
  
14. Na seção **Log de transações** , marque **Fazer backup da parte final do log e deixar o banco de dados no estado de restauração**.  
  
     Isso é equivalente a especificar a instrução [BACKUP](/sql/t-sql/statements/backup-transact-sql) a seguir:  
  
     `BACKUP LOG <database_name> TO <backup_device> WITH NORECOVERY`  
  
    > [!IMPORTANT]  
    >  Na hora da restauração, a caixa de diálogo Restaurar Banco de dados exibe o tipo de um backup da parte final do log como **Log de Transações (Copiar Somente)** .  
  
15. Se o backup estiver sendo feito em uma unidade de fita (conforme especificado na seção **Destino** da página **Geral** ), a opção **Descarregar a fita após o backup** estará ativa. Clicar nessa opção ativa a opção **Rebobinar a fita antes de descarregar** .  
  
16. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] e posteriores dão suporte para [compactação de backup](backup-compression-sql-server.md). Por padrão, a compactação de um backup depende do valor da opção de configuração de servidor **padrão de compactação de backup**. Porém, independentemente do padrão atual do nível do servidor, é possível compactar um backup, marcando a opção **Compactar backup**e evitar a compactação marcando **Não compactar o backup**.  
  
     **Para exibir o padrão de compactação de backup atual**  
  
    -   [Exibir ou configurar a opção de configuração de servidor backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-create-a-backup-of-the-currently-active-transaction-log"></a>Para criar um backup do log de transações atualmente ativas  
  
1.  Execute a instrução BACKUP LOG para fazer backup do log de transações atualmente ativas, especificando:  
  
    -   O nome do banco de dados ao qual o log de transações cujo backup será feito pertence.  
  
    -   O dispositivo de backup onde o backup de log de transações será gravado.  
  
    -   A cláusula NO_TRUNCATE.  
  
         Essa cláusula permite fazer backup da parte ativa do log de transações mesmo se o banco de dados estiver inacessível, contanto que o arquivo de log de transações esteja acessível e sem-danos.  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> Exemplo (Transact-SQL)  
  
> [!NOTE]  
>  Este exemplo usa o [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], que usa o modelo de recuperação simples. Para permitir backups de log, antes de fazer um backup de banco de dados completo, o banco de dados foi definido para usar o modelo de recuperação completa. Para obter mais informações, veja [Exibir ou alterar o modelo de recuperação de um banco de dados &#40;SQL Server&#41;](view-or-change-the-recovery-model-of-a-database-sql-server.md).  
  
 Este exemplo faz o backup do log da transação ativa no momento quando um banco de dados é danificado e está inacessível, se o log de transação não estiver danificado e estiver acessível.  
  
```scr  
BACKUP LOG AdventureWorks2012  
   TO MyAdvWorks_FullRM_log1  
   WITH NO_TRUNCATE;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Restaurar um backup de log de transações &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)   
 [Restaurar um banco de dados do SQL Server em um ponto específico &#40;Modelo de recuperação completa&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)   
 [Fazer backup do banco de dados &#40;página Opções de Backup&#41;](back-up-database-backup-options-page.md)   
 [Fazer backup do banco de dados &#40;página Geral&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)   
 [Aplicar backups de log de transações &#40;SQL Server&#41;](transaction-log-backups-sql-server.md)   
 [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [Restaurações de arquivos &#40;Modelo de recuperação simples&#41;](file-restores-simple-recovery-model.md)   
 [Restaurações de arquivo &#40;Modelo de recuperação completa&#41;](file-restores-full-recovery-model.md)  
  
  
