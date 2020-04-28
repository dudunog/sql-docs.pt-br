---
title: Restaurar um backup de banco de dados (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.locatebackupfileazure.f1
- sql12.swb.specifybackup.f1
helpviewer_keywords:
- full backups [SQL Server]
- database restores [SQL Server], full backups
- backing up databases [SQL Server], full backups
- database backups [SQL Server], full backups
- restoring databases [SQL Server], full backups
ms.assetid: 24b3311d-5ce0-4581-9a05-5c7c726c7b21
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 521fc35b8ada4b1eb6c62e75fed4e1d9f99d21c4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "70154785"
---
# <a name="restore-a-database-backup-sql-server-management-studio"></a>Restaurar um backup de banco de dados (SQL Server Management Studio)
  Este tópico explica como restaurar um backup de banco de dados completo.  
  
> [!IMPORTANT]  
>  No modelo de recuperação completo ou bulk-logged, antes de poder restaurar um banco de dados no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], é necessário fazer backup do log de transações ativas (conhecido como a parte final do log). Para obter mais informações, veja [Fazer backup de um log de transações &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)). Para restaurar um banco de dados criptografado, é necessário ter acesso ao certificado ou à chave assimétrica usada para criptografar o banco de dados. Sem o certificado ou a chave assimétrica, o banco de dados não pode ser restaurado. Como resultado, o certificado usado para criptografar a chave de criptografia do banco de dados deverá ser retido enquanto o backup for necessário. Para obter mais informações, consulte [SQL Server Certificates and Asymmetric Keys](../security/sql-server-certificates-and-asymmetric-keys.md).  
  
 Observe que se você restaurar um banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ou superior no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], o banco de dados será atualizado automaticamente. Normalmente, o banco de dados se torna disponível imediatamente. No entanto, se o banco de dados do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] tiver índices de texto completo, o processo de atualização importará, redefinirá ou recriará esses índices, dependendo da configuração da propriedade de servidor **Opção de Atualização de Texto Completo** . Se a opção de atualização for definida como **Importar** ou **Recriar**, os índices de texto completo permanecerão indisponíveis durante a atualização. Dependendo da quantidade de dados a serem indexados, a importação poderá levar várias horas e a recriação poderá ser até dez vezes mais demorada. Observe também que, quando a opção de atualização for definida como **importar**, se um catálogo de texto completo não estiver disponível, os índices de texto completo associados serão recriados. Para obter informações sobre como exibir ou alterar a configuração da propriedade **Full-Text Upgrade Option** , veja [Gerenciar e monitorar a pesquisa de texto completo para uma instância de servidor](../search/manage-and-monitor-full-text-search-for-a-server-instance.md).  
  
### <a name="to-restore-a-full-database-backup"></a>Para restaurar um backup de banco de dados completo  
  
1.  Depois de se conectar à instância apropriada do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], no Pesquisador de objetos, clique no nome do servidor para expandir a árvore de servidores.  
  
2.  Expanda os **Bancos de dados**. Dependendo do banco de dados, selecione um banco de dados de usuário ou expanda os **Bancos de dados do sistema**e selecione um banco de dados do sistema.  
  
3.  Clique com o botão direito do mouse no banco de dados, aponte para **tarefas**, aponte para **restaurar**e clique em **banco de dados**, que abre a caixa de diálogo **restaurar banco de dados** .  
  
4.  Na página **Geral** , use a seção **Origem** para especificar a origem e o local dos conjuntos de backup a serem restaurados. Selecione uma das seguintes opções:  
  
    -   **Backup de banco de dados**  
  
         Selecione o banco de dados a ser restaurado na lista suspensa. A lista contém apenas os bancos de dados dos quais foi feito um backup de acordo com o histórico de backup do **msdb** .  
  
    > [!NOTE]  
    >  Se o backup foi obtido de um servidor diferente, o servidor de destino não terá informações de histórico de backup para o banco de dados especificado. Nesse caso, selecione **Dispositivo** para especificar manualmente o arquivo ou o dispositivo a ser restaurado.  
  
    -   **Dispositivo**  
  
         Clique no botão procurar (**...**) para abrir a caixa de diálogo **selecionar dispositivos de backup** . Na caixa **Tipo de mídia de backup** , selecione um dos tipos de dispositivo listados. Para selecionar um ou mais dispositivos da caixa **Mídia de backup** , clique em **Adicionar**.  
  
         Após adicionar os dispositivos desejados à caixa de listagem **Mídia de backup** , clique em **OK** para voltar à página **Geral** .  
  
         Na caixa de listagem **Origem: Dispositivo: Banco de Dados** , selecione o nome do banco de dados que deve ser restaurado.  
  
        > [!NOTE]  
        >  Essa lista estará disponível apenas quando **Dispositivo** for selecionado. Apenas os bancos de dados que têm backups no dispositivo selecionado estarão disponíveis.  
  
         **Mídia de backup**  
         Selecione o meio para a operação de restauração: **arquivo**, **fita**, **URL**ou **dispositivo de backup**. A opção **Fita** só aparece se houver uma unidade de fita montada no computador, e a opção **Dispositivo de backup** só aparece se houver, no mínimo, um dispositivo de backup.  
  
         **Local do backup**  
         Exibir, adicionar ou remover mídia para a operação de restauração. A lista pode conter até 64 arquivos, fitas ou dispositivos de backup.  
  
         **Adicionar**  
         Adiciona o local de um dispositivo de backup à lista **local de backup** . Dependendo do tipo de mídia selecionado no campo **Mídia do backup** , clicar **em Adicionar** abre uma das caixas de diálogo a seguir.  
  
        |Típo de mídia|Caixa de diálogo|DESCRIÇÃO|  
        |----------------|----------------|-----------------|  
        |**Arquivo**|**Localizar o arquivo de backup**|Nessa caixa de diálogo, você pode selecionar um arquivo local da árvore ou pode especificar um arquivo remoto que use o seu nome totalmente qualificado da UNC (Convenção Universal de Nomenclatura). Para obter mais informações, consulte [Dispositivos de backup &#40;SQL Server&#41;](backup-devices-sql-server.md).|  
        |**Dispositivo**|**Selecionar dispositivo de backup**|Nessa caixa de diálogo você pode selecionar em uma lista de dispositivos lógicos de backup, definida na instância de servidor.|  
        |**Fita**|**Selecionar fita de backup**|Nessa caixa de diálogo você pode selecionar em uma lista de unidades de fita conectadas fisicamente ao computador que executa a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
        |**URL**|Isso inicia duas caixas de diálogo na seguinte ordem:<br /><br /> 1) **conectar-se ao armazenamento do Azure**<br /><br /> 2) **localizar arquivo de backup no Azure**|Na caixa de diálogo **conectar ao armazenamento do Azure** , selecione uma credencial SQL existente que armazena o nome da conta de armazenamento do Azure e informações de chave de acesso, ou crie uma nova credencial do SQL especificando o nome da conta de armazenamento e informações de chave de acesso de armazenamento. Para obter mais informações, consulte [conectar-se ao armazenamento do Azure &#40;restaurar&#41;](connect-to-microsoft-azure-storage-restore.md).<br /><br /> Na caixa de diálogo de **Localizar Arquivo de Backup** , você pode selecionar um arquivo da lista de contêineres exibidos no quadro esquerdo.|  
  
         Se a lista estiver cheia, o botão **Adicionar** ficará indisponível.  
  
         **Remover**  
         Remove um ou mais arquivos, fitas ou dispositivos de backup lógicos selecionados.  
  
         **Conteúdo**  
         Exibe o conteúdos da mídia de um arquivo, fita ou dispositivo de backup lógico selecionado.  
  
5.  Na seção **Destino** , a caixa **Banco de Dados** é preenchida automaticamente com o nome do banco de dados a ser restaurado. Para alterar o nome do banco de dados, digite o novo nome na caixa **Banco de Dados** .  
  
6.  Na caixa **Restaurar para** , deixe o padrão como **Para o último backup obtido** ou clique em **Linha do tempo** para acessar a caixa de diálogo **Linha do Tempo de Backup** para selecionar manualmente um momento determinado a fim de interromper a ação de recuperação. Para obter mais informações sobre como designar um momento específico, consulte [Backup Timeline](backup-timeline.md).  
  
7.  Na grade **Conjuntos de backup a serem restaurados** , selecione os backups a serem restaurados. Essa grade exibe os backups disponíveis para o local especificado. Por padrão, um plano de recuperação é sugerido. Para substituir o plano de recuperação sugerido, você pode alterar as seleções na grade. Backups que dependem da restauração de um backup anterior têm a seleção automaticamente cancelada quando a seleção do backup anterior é cancelada. Para obter informações sobre as colunas da grade **Conjuntos de backup a serem restaurados** , veja [Restaurar banco de dados &#40;página Geral&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)).  
  
8.  Opcionalmente, clique em **Arquivos** no painel **Selecionar uma página** para acessar a caixa de diálogo **Arquivos de Banco de Dados** . Daqui, você pode restaurar o banco de dados em um novo local, com a especificação de um novo destino de restauração para cada arquivo na grade **Restaurar os arquivos de banco de dados como** . Para obter mais informações sobre essa grade, veja [Restaurar banco de dados &#40;Página Arquivos&#41;](restore-database-files-page.md).  
  
9. Para exibir ou selecionar as opções avançadas, na página **Opções** , no painel **Opções de restauração** , você pode selecionar qualquer uma das seguintes opções, de acordo com sua situação:  
  
    1.  Opções `WITH` (não necessárias):  
  
        -   **Substituir o banco de dados existente (com REPLACE)**  
  
        -   **Preservar as configurações de replicação (com KEEP_REPLICATION)**  
  
        -   **Restringir o acesso ao banco de dados restaurado (com RESTRICTED_USER)**  
  
    2.  Selecione uma opção para a caixa **Estado de recuperação** . Essa caixa determina o estado do banco de dados após a operação de restauração.  
  
        -   **RESTORE WITH RECOVERY** é o comportamento padrão que deixa o banco de dados pronto para uso revertendo as transações não confirmadas. Os logs de transações adicionais não podem ser restaurados. Selecione essa opção se você estiver restaurando todos os backups necessários agora.  
  
        -   **RESTORE WITH NORECOVERY** deixa o banco de dados não operacional e não reverte as transações não confirmadas. Os logs de transações adicionais podem ser restaurados. Só é possível usar o banco de dados depois que ele é recuperado.  
  
        -   **RESTORE WITH STANDBY** deixa o banco de dados no modo somente leitura. Ele desfaz as transações não confirmadas, mas salva as ações de desfazer em um arquivo em espera para que os efeitos da recuperação possam ser revertidos.  
  
    3.  **Fazer backup da parte final do log antes da restauração** será selecionada se for necessário para o momento determinado que você selecionou. Você não precisa modificar essa configuração, mas poderá escolher o backup da parte final do log até mesmo se não for necessário. nome de arquivo aqui? Se o primeiro conjunto de backup na página **geral** estiver no Azure, o backup do log final também será feito no mesmo contêiner de armazenamento.  
  
    4.  As operações de restauração poderão falhar se houver conexões ativas com o banco de dados. Marque a opção **Fechar conexões existentes** para assegurar que todas as conexões ativas entre o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] e o banco de dados sejam fechadas. Essa caixa de seleção define o banco de dados no modo de usuário único antes de executar as operações de restauração e define o banco de dados no modo de vários usuários ao concluir.  
  
    5.  Selecione **Perguntar antes de restaurar cada backup** para que você seja solicitado entre cada operação de restauração. Isso normalmente só é necessário quando o banco de dados é grande e você deseja monitorar o status da operação de restauração.  
  
     Para obter mais informações sobre essas opções de restauração, veja [Restaurar banco de dados &#40;página Opções&#41;](restore-database-options-page.md)).  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Consulte Também  
 [Fazer backup de um log de transações &#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)   
 [Criar um &#40;de backup de banco de dados completo SQL Server&#41;](create-a-full-database-backup-sql-server.md)   
 [Restaurar um banco de dados em um novo local &#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)   
 [Restaurar um backup de log de transações &#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)   
 [RESTORE &#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Página restaurar opções de &#40;de banco de dados&#41;](restore-database-options-page.md)   
 [Restaurar banco de dados &#40;página Geral&#41;](../../integration-services/general-page-of-integration-services-designers-options.md)  
  
  
