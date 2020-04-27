---
title: Movendo os bancos de dados do servidor de relatório para outro computador (modo nativo do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 44a9854d-e333-44f6-bdc7-8837b9f34416
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a92fea73d84bc28f09951120e763b602586e7069
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66103716"
---
# <a name="moving-the-report-server-databases-to-another-computer-ssrs-native-mode"></a>Movendo os bancos de dados do servidor de relatório para outro computador (modo nativo do SSRS)
  Você pode mover os bancos de dados do servidor de relatório que são usados em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] uma instalação do para uma instância do que está em um computador diferente. Os bancos de dados reportserver e reportservertempdb devem ser movidos ou copiados juntos. Uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] requer os dois bancos de dados; o banco de dados reportservertempdb deve ser relacionado por nome ao banco de dados reportserver primário que está sendo movido.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]Modo nativo.  
  
 A movimentação de um banco de dados não afeta as operações agendadas que estão definidas atualmente para itens de servidor de relatório.  
  
-   As agendas serão recriadas na primeira vez em que o serviço do servidor de relatório for reiniciado.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent que são usados para acionar uma agenda serão recriados na nova instância do banco de dados. Não é necessário mover os trabalhos para o novo computador, mas você pode excluir os trabalhos que não serão mais usados.  
  
-   Assinaturas, relatórios em cache e instantâneos são preservados no banco de dados movido. Se um instantâneo não estiver capturando dados atualizados depois que o banco de dados for movido, desmarque as opções de instantâneo no Gerenciador de Relatórios, clique em **Aplicar** para salvar as alterações, recrie o agendamento e clique em **Aplicar** novamente para salvar as alterações.  
  
-   Os dados do relatório temporário e da sessão de usuário que são armazenados em reportservertempdb são mantidos quando o banco de dados é movido.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece várias abordagens para mover bancos de dados, inclusive backup e restauração, anexação e desanexação e cópia. Nem todas as abordagens são apropriadas para realocar um banco de dados existente em uma nova instância do servidor. A abordagem que deve ser usada para mover o banco de dados do servidor de relatório varia dependendo dos requisitos de disponibilidade do sistema. O modo mais fácil para mover os bancos de dados do servidor de relatório é anexá-los e desanexá-los. No entanto, esta abordagem requer que o servidor de relatório fique offline enquanto o banco de dados é desanexado. O backup e a restauração são a melhor opção se você desejar minimizar as interrupções de serviço, mas é necessário executar os comandos [!INCLUDE[tsql](../../includes/tsql-md.md)] para efetuar as operações. A cópia do banco de dados não é recomendada (principalmente se o Assistente para Copiar Banco de Dados for utilizado); as configurações de permissão não são preservadas no banco de dados.  
  
> [!IMPORTANT]  
>  As etapas descritas neste tópico são recomendadas quando a realocação do banco de dados do servidor de relatório for a única alteração feita na instalação existente. A migração de uma instalação inteira do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (ou seja, a movimentação do banco de dados e a alteração da identidade do serviço Windows do Servidor de Relatório que usa o banco de dados) exige a reconfiguração da conexão e a redefinição de uma chave de criptografia.  
  
## <a name="detaching-and-attaching-the-report-server-databases"></a>Desanexando e anexando os bancos de dados do servidor de relatório  
 Se conseguir colocar o servidor de relatório offline, você poderá desanexar os bancos de dados para movê-los para a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser usada. Esta abordagem preserva as permissões nos bancos de dados. Se você estiver usando um banco de dados do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , mova-o para outra instância do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Depois de mover os bancos de dados, reconfigure a conexão do servidor de relatório com o banco de dados. Se você estiver executando uma implantação de expansão, deverá reconfigurar a conexão do banco de dados do servidor de relatório para cada servidor de relatório da implantação.  
  
 Realize as etapas a seguir para mover os bancos de dados:  
  
1.  Faça backup das chaves de criptografia para o banco de dados do servidor de relatório que deseja mover. Você pode usar a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para fazer backup das chaves.  
  
2.  Pare o serviço do servidor de relatório. Você pode usar a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para parar o serviço.  
  
3.  Inicie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e abra uma conexão com a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância que hospeda os bancos de dados do servidor de relatório.  
  
4.  Clique com o botão direito do mouse no banco de dados do servidor de relatório, aponte para Tarefas e clique em **Desanexar**. Repita esta etapa para o banco de dados temporário do servidor de relatório.  
  
5.  Copie ou mova os arquivos .mdf e .ldf para a pasta Dados da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que deseja usar. Como dois bancos de dados estão sendo movidos, certifique-se de mover ou copiar os quatro arquivos.  
  
6.  No [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], abra uma conexão com a nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospedará os bancos de dados do servidor de relatório.  
  
7.  Clique com o botão direito do mouse no nó Bancos de dados e clique em **Anexar**.  
  
8.  Clique em **Adicionar** para selecionar os arquivos .mdf e .ldf do banco de dados do servidor de relatórios que deseja anexar. Repita esta etapa para o banco de dados temporário do servidor de relatório.  
  
9. Depois que os bancos de dados forem anexados, verifique `RSExecRole` se o é uma função de banco de dados no banco de dados do servidor de relatório e no banco de dados temporário. `RSExecRole`é necessário ter permissões de selecionar, inserir, atualizar, excluir e referenciar nas tabelas de banco de dados do servidor de relatório e permissões de execução nos procedimentos armazenados. Para mais informações, veja [Criar o RSExecRole](../security/create-the-rsexecrole.md).  
  
10. Inicie a ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e abra uma conexão com o servidor de relatório.  
  
11. Na página Banco de dados, selecione a nova instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e clique em **Conectar**.  
  
12. Selecione o banco de dados do servidor de relatório que acaba de ser movido e clique em **Aplicar**.  
  
13. Na página Chaves de Criptografia, clique em Restaurar. Especifique o arquivo que contém a cópia de backup das chaves e a senha para desbloquear o arquivo.  
  
14. Reinicie o serviço Servidor de Relatório.  
  
## <a name="backing-up-and-restoring-the-report-server-databases"></a>Fazendo backup e restaurando os bancos de dados do servidor de relatório  
 Se não for possível colocar o servidor de relatório offline, use o recurso de backup e restauração para realocar os bancos de dados do servidor de relatório. Você deve usar instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] para fazer o backup e a restauração. Depois de restaurar os bancos de dados, configure o servidor de relatório para usar o banco de dados na nova instância do servidor. Para obter mais informações, consulte as instruções no final deste tópico.  
  
### <a name="using-backup-and-copy_only-to-backup-the-report-server-databases"></a>Usando BACKUP e COPY_ONLY para fazer backup dos bancos de dados do servidor de relatório  
 Ao fazer backup dos bancos de dados, defina o argumento COPY_ONLY. Faça backup dos bancos de dados e dos arquivos de log.  
  
```  
-- To permit log backups, before the full database backup, alter the database   
-- to use the full recovery model.  
USE master;  
GO  
ALTER DATABASE ReportServer  
   SET RECOVERY FULL  
  
-- If the ReportServerData device does not exist yet, create it.   
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerData',   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\BACKUP\ReportServerData.bak'  
  
-- Create a logical backup device, ReportServerLog.  
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerLog',   
'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\BACKUP\ReportServerLog.bak'  
  
-- Back up the full ReportServer database.  
BACKUP DATABASE ReportServer  
   TO ReportServerData  
   WITH COPY_ONLY  
  
-- Back up the ReportServer log.  
BACKUP LOG ReportServer  
   TO ReportServerLog  
   WITH COPY_ONLY  
  
-- To permit log backups, before the full database backup, alter the database   
-- to use the full recovery model.  
USE master;  
GO  
ALTER DATABASE ReportServerTempdb  
   SET RECOVERY FULL  
  
-- If the ReportServerTempDBData device does not exist yet, create it.   
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerTempDBData',   
'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\BACKUP\ReportServerTempDBData.bak'  
  
-- Create a logical backup device, ReportServerTempDBLog.  
USE master  
GO  
EXEC sp_addumpdevice 'disk', 'ReportServerTempDBLog',   
'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\BACKUP\ReportServerTempDBLog.bak'  
  
-- Back up the full ReportServerTempDB database.  
BACKUP DATABASE ReportServerTempDB  
   TO ReportServerTempDBData  
   WITH COPY_ONLY  
  
-- Back up the ReportServerTempDB log.  
BACKUP LOG ReportServerTempDB  
   TO ReportServerTempDBLog  
   WITH COPY_ONLY  
```  
  
### <a name="using-restore-and-move-to-relocate-the-report-server-databases"></a>Usando RESTORE e MOVE para realocar os bancos de dados do servidor de relatório  
 Ao restaurar os bancos de dados, inclua o argumento MOVE para especificar um caminho. Use o argumento NORECOVERY para executar a restauração inicial; isso mantém o banco de dados no estado RESTORING, permitindo que você tenha tempo de revisar os backups de log para determinar qual deve ser restaurado. A etapa final repete a operação RESTORE com o argumento RECOVERY.  
  
 O argumento MOVE usa o nome lógico do arquivo de dados. Para localizar o nome lógico, execute a seguinte instrução: `RESTORE FILELISTONLY FROM DISK='C:\ReportServerData.bak';`  
  
 O exemplo a seguir inclui o argumento FILE para especificar a posição do arquivo de log a ser restaurado. Para localizar a posição do arquivo, execute a seguinte instrução: `RESTORE HEADERONLY FROM DISK='C:\ReportServerData.bak';`  
  
 Ao restaurar o banco de dados e os arquivos de log, execute cada operação RESTORE separadamente.  
  
```  
-- Restore the report server database and move to new instance folder   
RESTORE DATABASE ReportServer  
   FROM DISK='C:\ReportServerData.bak'  
   WITH NORECOVERY,   
      MOVE 'ReportServer' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer.mdf',   
      MOVE 'ReportServer_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer_Log.ldf';  
GO  
  
-- Restore the report server log file to new instance folder   
RESTORE LOG ReportServer  
   FROM DISK='C:\ReportServerData.bak'  
   WITH NORECOVERY, FILE=2  
      MOVE 'ReportServer' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer.mdf',   
      MOVE 'ReportServer_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServer_Log.ldf';  
GO  
  
-- Restore and move the report server temporary database  
RESTORE DATABASE ReportServerTempdb  
   FROM DISK='C:\ReportServerTempDBData.bak'  
   WITH NORECOVERY,   
      MOVE 'ReportServerTempDB' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServerTempDB.mdf',   
      MOVE 'ReportServerTempDB_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\REportServerTempDB_Log.ldf';  
GO  
  
-- Restore the temporary database log file to new instance folder   
RESTORE LOG ReportServerTempdb  
   FROM DISK='C:\ReportServerTempDBData.bak'  
   WITH NORECOVERY, FILE=2  
      MOVE 'ReportServerTempDB' TO   
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\ReportServerTempDB.mdf',   
      MOVE 'ReportServerTempDB_log' TO  
         'C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Data\REportServerTempDB_Log.ldf';  
GO  
  
-- Perform final restore  
RESTORE DATABASE ReportServer  
   WITH RECOVERY  
GO  
  
-- Perform final restore  
RESTORE DATABASE ReportServerTempDB  
   WITH RECOVERY  
GO  
```  
  
### <a name="how-to-configure-the-report-server-database-connection"></a>Como configurar a conexão do banco de dados do servidor de relatório  
  
1.  Inicie o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager e abra uma conexão com o servidor de relatório.  
  
2.  Na página Banco de Dados, clique em **Alterar Banco de Dados**. Clique em **Avançar**.  
  
3.  Clique em **Escolher um banco de dados existente do servidor de relatório**. Clique em **Avançar**.  
  
4.  Selecione o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que agora hospeda o banco de dados do servidor de relatório e clique em **Testar Conexão**. Clique em **Avançar**.  
  
5.  Em Nome do Banco de Dados, selecione o banco de dados do servidor de relatório que deseja usar. Clique em **Avançar**.  
  
6.  Em Credenciais, especifique as credenciais que o servidor de relatório usará para conectar-se ao banco de dados do servidor de relatório. Clique em **Avançar**.  
  
7.  Clique em **Avançar** e em **Concluir**.  
  
> [!NOTE]  
>  Uma instalação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] requer que a instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] inclua a função `RSExecRole`. A criação de funções, o registro de logon e as atribuições de função ocorrem quando a conexão do banco de dados do servidor de relatório é definida por meio da ferramenta Configuração do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Se você usar abordagens alternativas (especificamente, se usar o utilitário de prompt de comando rsconfig.exe) para configurar a conexão, o servidor de relatório não estará em um estado de funcionamento. Talvez seja necessário gravar o código WMI para disponibilizar o servidor de relatório. Para obter mais informações, consulte [Acessar o provedor WMI do Reporting Services](../tools/access-the-reporting-services-wmi-provider.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Criar o RSExecRole](../security/create-the-rsexecrole.md)   
 [Iniciar e parar o serviço Servidor de Relatório](start-and-stop-the-report-server-service.md)   
 [Configurar uma conexão de banco de dados do servidor de relatório &#40;Configuration Manager SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Configurar a conta de execução autônoma &#40;Configuration Manager do SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)   
 [Reporting Services Configuration Manager &#40;Modo Nativo&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Utilitário rsconfig &#40;SSRS&#41;](../tools/rsconfig-utility-ssrs.md)   
 [Configurar e gerenciar chaves de criptografia &#40;Configuration Manager SSRS&#41;](../install-windows/ssrs-encryption-keys-manage-encryption-keys.md)   
 [Banco de dados do servidor de relatório &#40;modo nativo do SSRS&#41;](report-server-database-ssrs-native-mode.md)  
  
  
