---
title: Adicionar arquivos de dados ou de log a um banco de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], files
- adding data files
- adding files
- adding log files
- file additions [SQL Server], steps
- files [SQL Server], adding
- data additions [SQL Server]
ms.assetid: 8ead516a-1334-4f40-84b2-509d0a8ffa45
author: stevestein
ms.author: sstein
ms.openlocfilehash: f72e00f9dab422652237b4b85579c544d0cda9fb
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84952346"
---
# <a name="add-data-or-log-files-to-a-database"></a>Adicionar arquivos de dados ou de log a um banco de dados
  Este tópico descreve como adicionar um arquivo de dados ou de log a um banco de dados no [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Limitações e restrições](#Restrictions)  
  
     [Segurança](#Security)  
  
-   **Para adicionar arquivos de dados ou de log a um banco de dados existente usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitações e restrições  
  
-   Você não pode adicionar ou remover um arquivo enquanto uma instrução BACKUP está em execução.  
  
-   Um máximo de 32.767 arquivos e 32.767 grupos de arquivos pode ser especificado para cada banco de dados.  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Requer a permissão ALTER no banco de dados.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-add-data-or-log-files-to-a-database"></a>Para adicionar arquivos de dados ou de log a um banco de dados existente  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] e expanda-a.  
  
2.  Expanda **Bancos de Dados**, clique com o botão direito do mouse no banco de dados ao qual deseja adicionar os arquivos e clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do Banco de Dados** , selecione a página **Arquivos** .  
  
4.  Para adicionar arquivos de dados ou de log de transação, clique em **Adicionar**.  
  
5.  Na grade **Arquivos do Banco de Dados** , digite um nome lógico para o arquivo. O nome do arquivo deve ser exclusivo no banco de dados.  
  
6.  Selecione o tipo de arquivo, de dados ou de log.  
  
7.  Para um arquivo de dados, selecione o grupo de arquivos no qual o arquivo deve ser incluído na lista ou selecione **\<new filegroup>** para criar um novo grupo de arquivos. Logs de transações não podem ser colocados em grupos de arquivos.  
  
8.  Especifique o tamanho inicial do arquivo. Deixe os arquivos de dados tão grandes quanto possível, com base na quantidade máxima de dados que você espera ter no banco de dados.  
  
9. Para especificar como o arquivo deve se expandir, clique em ( **…** ) na coluna **Aumento Automático**. Selecione entre as seguintes opções:  
  
    1.  Para permitir que o arquivo selecionado aumente conforme mais espaço de dados se fizer necessário; marque a caixa de seleção **Habilitar Aumento Automático** e depois selecione entre as seguintes opções:  
  
    2.  Para especificar que o arquivo deve aumentar em incrementos fixos, selecione **Em Megabytes** e especifique um valor.  
  
    3.  Para especificar que o arquivo deve aumentar em uma porcentagem do tamanho atual do arquivo, selecione **Em Porcentagem** e especifique um valor.  
  
10. Para especificar o limite máximo de tamanho do arquivo, selecione entre as seguintes opções:  
  
    1.  Para especificar o tamanho máximo até o qual o arquivo pode se expandir, selecione **Expansão de Arquivo Restrita (MB)** e especifique um valor.  
  
    2.  Para permitir que o arquivo aumente conforme o necessário, selecione **Aumento de Arquivo Irrestrito**.  
  
    3.  Para impedir o aumento do arquivo, desmarque a caixa de seleção **Habilitar Aumento Automático** . O tamanho do arquivo não se expandirá além do valor especificado na coluna **Tamanho Inicial (MB)** .  
  
    > [!NOTE]  
    >  O tamanho máximo do banco de dados é determinado pela quantidade disponível de espaço em disco e dos limites de licença determinados pela versão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em uso.  
  
11. Especifique o caminho para o local do arquivo. O caminho especificado deve existir antes de adicionar o arquivo.  
  
    > [!NOTE]  
    >  Por padrão, os logs de transação e os dados são colocados na mesma unidade e caminho para acomodar sistemas em um único disco, mas essa pode não ser a melhor opção para ambientes de produção. Para obter mais informações, consulte [Database Files and Filegroups](database-files-and-filegroups.md).  
  
12. Clique em **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usando o Transact-SQL  
  
#### <a name="to-add-data-or-log-files-to-a-database"></a>Para adicionar arquivos de dados ou de log a um banco de dados existente  
  
1.  Conecte-se ao [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Na barra Padrão, clique em **Nova Consulta**.  
  
3.  Copie e cole o exemplo a seguir na janela de consulta e clique em **Executar**. O exemplo adiciona um grupo de arquivos com dois arquivos a um banco de dados. O exemplo cria o grupo de arquivos `Test1FG1` no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] e adiciona dois arquivos de 5 MB ao grupo de arquivos.  
  
 [!code-sql[DatabaseDDL#AlterDatabase2](../../snippets/tsql/SQL14/tsql/databaseddl/transact-sql/alterdatabase.sql#alterdatabase2)]  
  
 Para obter mais exemplos, consulte [Opções de arquivo e grupos de arquivos ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options).  
  
## <a name="see-also"></a>Consulte Também  
 [Database Files and Filegroups](database-files-and-filegroups.md)   
 [Excluir arquivos de dados ou de log de um banco de dados](delete-data-or-log-files-from-a-database.md)   
 [Aumentar o tamanho de um banco de dados](increase-the-size-of-a-database.md)  
  
  
